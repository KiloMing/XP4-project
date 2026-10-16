# 学习证据

L1：认识概念；L2：解释并跟随示例；L3：独立完成最小实现；L4：完成变式并定位问题。

## 初始化时的掌握记录（保留历史）

| 主题 | 当前状态 | 下一证据 |
|---|---|---|
| Linux/CMake/C++基础 | 有旧仓库学习记录，本项目未独立复测 | 最小CMake与回调/计时练习 |
| PX4状态与故障保护 | 待学习/核验 | 解释模式与实际起降日志 |
| MAVSDK遥测 | 待实施 | 独立只读程序及断连测试 |
| 坐标与高度 | 有机器人坐标经历，飞行坐标待验收 | 转换练习与真值对照 |
| 自动起降与往返 | 待实施 | 单轮及连续3轮报告 |
| 状态机与异常 | 待实施 | 超时状态、故障注入和独立排错 |

不因本次计划提交而提升掌握等级。

## 2026-10-16 实验与掌握证据更新

| 主题 | 已有实际证据 | 掌握边界与下一证据 |
|---|---|---|
| SITL / Gazebo / QGC | X500 启动，QGC 连接，Preflight Check OK | 已完成引导实践；需独立重启复现、解释组件分工 |
| 起降与状态 | commander takeoff/land；Landing detected、Disarmed by landing、in failsafe: no | 不等于 MAVSDK 自动控制或 V1.0 验收；需解释命令接受与动作完成 |
| uORB | vehicle_land_detected 的 landed:true、at_rest:true；读取 vehicle_local_position | 曾拼错话题名；需独立解释字段、坐标和单位；不能代替电机转速测量 |
| 网络排错 | OpticalFlow 下载的 127.0.0.1:7897 代理问题修复后编译成功 | 修复命令和独立诊断过程未归档，不标 L4 |
| CMake / MAVSDK 链接 | libmavsdk-dev v4.0.1 amd64；修正 cmake_minimum_required 拼写后 [100%] Built target px4_connect | 属于有指导的编译实践；真实源码待同步，独立重建待验证，不标 L3 |
| MAVSDK 系统发现 | 无运行或发现飞控证据 | 下一步执行 ./build/px4_connect 并记录实际结果 |
| MAVSDK Telemetry | 尚未实践 | 系统发现通过后开始订阅，再验证断连 |

本次进展按有指导的操作实践记录，不把操作成功直接等同于完整 L2 概念解释通过，更不升级为 L3/L4。原始截图未存入仓库；依据为用户聊天展示与本次确认的事实摘要，见 [daily](daily/2026-10-16.md)。
