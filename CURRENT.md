# 当前进度

更新时间：2026-10-28（Asia/Shanghai）

## 当前主线：第 04 课，C++ 状态接收已通，Offboard 待完成

- 环境已确认：Ubuntu 24.04.4 LTS / x86_64 / ROS 2 Jazzy / Gazebo Sim 8.15.0 / PX4 v1.17.0，详见 [环境表](ENVIRONMENT.md)。Agent、px4_msgs 的实际 commit 仍待核对。
- 第 03 课单轮起降通过；第 04 课已用 `ros2 topic echo` 读到 `/fmu/out/vehicle_local_position_v1`，详见 [当天排错与复现记录](daily/2026-10-28.md)。
- 晚间已编译并运行 `px4_state_monitor` 包的 `position_monitor`，从等待数据转为连续位置/速度反馈；控制输入话题及 ACK 话题存在。Ubuntu `~/vision_landing_ws` 中的真实源码尚未同步，订阅路径存在记录差异，详见当天日志。
- 下一步补至少 30 秒状态归档、有效位与频率核对、停源后的过期/断连检测及独立重启。ROS 2 Offboard 仅学习了消息分工和心跳要求，尚未完成发布器、控制命令、模式切换、解锁或起降验收。
- 相机桥接、AprilTag、TF、ROS Offboard 和视觉降落尚未验收，继续按 [24 课计划](docs/VISION_LANDING_PLAN.md) 学习。
- 本次 Codex 只整理文档和 Git；没有在 Ubuntu 复测，也没有修改 PX4、MAVSDK 或旧 ROS 工程。旧 MAVSDK 进度保留如下。

## MAVSDK V1.0 已有实际进度（2026-10-16 后续实验）

- Ubuntu x86_64；截图显示 Ubuntu 24.04 的 MAVSDK 包安装成功。
- PX4 SITL + Gazebo X500 编译、启动成功；OpticalFlow 下载因 127.0.0.1:7897 代理失败，修复后继续成功。
- QGroundControl 连接，Preflight Check OK；commander takeoff/land 完成，见 Landing detected、Disarmed by landing、in failsafe: no。
- 读取 uORB vehicle_land_detected（landed:true、at_rest:true）与 vehicle_local_position；初次话题名拼写错误已纠正。
- libmavsdk-dev v4.0.1 amd64 安装成功；~/px4_ws/mavsdk_study/lesson_01 编译链接至 [100%] Built target px4_connect。
- 证据来自用户聊天展示及本次明确补充，非此次 Codex 重新运行；详见 [当日记录](daily/2026-10-16.md)。

## MAVSDK V1.0 未完成与恢复入口

1. 保持 PX4 SITL 运行，在 Ubuntu 的 lesson_01 目录执行 `./build/px4_connect`，记录退出状态、连接配置和实际发现结果。**目前没有已运行或已发现飞控的证据。**
2. 发现 PX4 后再进入 MAVSDK Telemetry：连接、位置、高度、飞行模式、解锁及着陆状态，随后验证断连。
3. 同步 Ubuntu 真实 main.cpp 与 CMakeLists.txt；当前无法读取 Ubuntu 源码，未提交替代代码。
4. 补齐环境版本、PX4 提交号、独立重启复现及日志；自动起降、单目标往返、连续 3 轮、异常测试与电机停转验收均待完成。

## 初始化时的历史记录（以下已由上方进度更新）

### 当时已完成

- 确定 V1.0 范围、学习路径、系统结构及验收方案。
- 只读查看 LINUX-STUDY 的 CURRENT、MASTERY、ENVIRONMENT、TEACHING_PROTOCOL 与 CMake 记录。
- 确认本地 XP4_project 原为空目录，远端为空仓库。
- SSH 认证账号为 KiloMing；本仓库提交邮箱为 3402684841@qq.com。
- 将计划和记录纳入独立项目；没有修改旧 ROS 2 工程。

### 当时尚未完成

Ubuntu 环境核验、依赖安装、版本锁定、PX4 编译、X500 启动、MAVSDK 编程与全部飞行测试。文档中的阈值是待验证的设计值，不是实测结果。

### 当时下一课

核验 Ubuntu 版本、CPU 架构、Gazebo 版本、图形加速、内存和网络；检查现有软件及环境变量。先形成兼容矩阵，再启动最简单的 X500。

### 初始化小测试（仍待回答）

用自己的话说明 PX4、Gazebo、QGroundControl、MAVSDK 的分工，以及“命令接受”和“动作完成”的区别。
