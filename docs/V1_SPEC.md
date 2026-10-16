# V1.0 实现规格

## 范围与架构

仅 Ubuntu 24.04、PX4 SITL、Gazebo Harmonic、QGC、MAVSDK C++、X500；单目标 A 与原始 H。无 ROS 2、视觉、SLAM、多航点或清洁功能。

配置 → C++ 状态机 → MAVSDK/MAVLink → PX4 ↔ Gazebo；QGC 观察/接管；日志模块记录命令、遥测、状态与结果。
采用 Action + Telemetry，不引入 Mission 航线或 Offboard 连续控制。PX4 负责底层飞行控制及飞控级故障保护。

## 状态机

CONNECT → PREFLIGHT → ARM → TAKEOFF_H → GO_A → SETTLE_A → LAND_A → VERIFY_STOP_A → WAIT_10S → RECHECK → REARM → TAKEOFF_A → GO_H → SETTLE_H → LAND_H → VERIFY_STOP_H → ROUND_DONE。

正常状态均可转入 FAULT；人工接管转为 ABORTED，终止自动命令。3 轮以外循环调度，每轮计数和入口标志重置，首次 H 保持不变。任何失败结束本次连续验收，修复后重新累计。

## 关键接口

- Mavsdk::add_any_connection() 与系统发现：验证实际地址、协议及端口。
- Action::arm()、set_takeoff_altitude()、takeoff()、goto_location()、land()；必要时 hold()。
- Telemetry 的 health、position、velocity_ned、landed_state、armed、in_air、battery、flight_mode、status_text 等；具体接口按锁定版本核对。
- 命令成功仅代表接受；状态推进依据新鲜遥测和持续条件。命令每状态入口只发一次，超时先核实状态，禁止盲目重复解锁/起飞。

## 坐标与场景

H 首次有效定位时保存，二次解锁不覆盖，不依赖可能更新的飞控 Home 实现返回。配置 A 可使用局部 ENU 米坐标，但必须通过明确的世界原点/地理参考转换为经纬度，验证轴向和单位。
goto_location 使用海拔绝对高度，不直接传 3。巡航平面为原始 H 地面上约 3m。第二次 takeoff 相对平台高度的语义按所选 PX4/MAVSDK 实测，随后用绝对高度验证。

初始场景无风无障碍、H/A 同高、距离约 10m、A 平台约 4m×4m，静态且有碰撞体。记录世界原点、平台位置尺寸、模型、地理参考与随机种子（若适用）。不使用视觉对准或避障。

## 安全判定

- 起飞前：有效连接、遥测新鲜、定位/home及相关健康项正常、电量达标、在地面且未解锁；安全阈值配置化。
- 到位：水平误差≤0.5m、高度误差≤0.5m、水平速度≤0.3m/s 连续2秒。
- 停转：OnGround、in_air=false、armed=false 连续稳定2秒，并有 Gazebo 各电机转速近零证据；具体转速接口与噪声阈值在阶段3测定并锁定。
- 等待：停转确认后以 steady_clock 计时≥10秒；遥测过期/仿真暂停禁止推进；恢复后重新验证条件。
- 再次起飞：重新执行完整安全检查；检查失败保持停机。

## 超时与异常

初始调试预算：连接30秒、健康检查60秒、起飞30秒、单段到位60秒、降落60秒、停转确认15秒、再次检查30秒。均是待测配置，不是通用安全常数；低实时率需区分仿真时间与墙钟时间，不以增大超时掩盖仿真故障。遥测新鲜度初值2秒，按实际频率复核。

地面失败不解锁；空中失败在定位与链路有效时请求保持并确认，按预先测试策略降落或交给人工。链路失效由 PX4 预先配置并实测的故障保护负责；不能假设应用还能发送命令。禁止空中强制解除武装。人工接管后不抢回控制；程序重启不自动续飞。

## 日志

每轮唯一 run_id/round_id；记录墙钟与单调时间、可用仿真时间、状态、事件、命令结果、位置/速度/高度、健康、数据年龄、武装/着陆、电池与失败原因。保存任务 JSONL、遥测 CSV、PX4 ULog 和 Gazebo 真值/转速。报告关联版本、参数及场景，程序不得把日志缺失记作通过。

## 后续目录

src/、include/、config/mission_v1.yaml、simulation/worlds/、simulation/models/、scripts/、tests/、exercises/、reports/、logs/、CMakeLists.txt。

## V2 接口预留

目标来源与状态机分离：V1配置提供单个 Target，V2地图选点仍提供同一单目标结构。字段含 id、frame、坐标、地理参考、平台高度、到达容差；明确单位、坐标系和有效性。V1 不实现地图界面或多目标队列。

参考：https://mavsdk.mavlink.io/main/en/cpp/api_reference/classmavsdk_1_1_action.html
https://mavsdk.mavlink.io/main/en/cpp/guide/telemetry.html
