# 基于 PX4 的无人机自主导航与光伏板清洁系统

历史基线：V1.0 自主起降与单目标往返仿真。2026-10-16 已完成 PX4 SITL + Gazebo X500 启动、QGC 连接、commander 起降练习，以及 MAVSDK lesson_01 编译链接。**px4_connect 运行与发现飞控尚未验证**；恢复该路线时先验证系统发现，再学习 Telemetry。

历史：当天初始化时处于规划阶段，尚未安装、构建或运行验证；后续实验见[当日记录](daily/2026-10-16.md)。

## 当前学习主线：静态 AprilTag 视觉降落

2026-10-27 新增 [八阶段、24 课视觉降落计划](docs/VISION_LANDING_PLAN.md)：Ubuntu 24.04 + ROS 2 Jazzy + Gazebo Harmonic + PX4 SITL，从通信、相机和坐标变换逐步学到对准、下降、任务状态机与重复实验。

2026-10-28：第 03 课单轮起降记录保留；第 04 课已完成命令行通信，以及 C++ `px4_state_monitor` 包中 `position_monitor` 的编译、启动和连续位置/速度接收，控制输入话题也已确认存在。详见 [当天学习记录](daily/2026-10-28.md)。节点源码位于 Ubuntu `~/vision_landing_ws`，尚未同步到本仓库；订阅路径记录差异、30 秒日志、断连检测和独立重启仍待核对或补测。**下一阶段 ROS 2 Offboard 离板控制尚未完成**，示范代码讨论不计为运行或飞行成果；相机和视觉降落仍待验收。

MAVSDK V1.0 作为历史路线保留，尚未完成的任务继续如实记录。视觉路线不要求先完成 MAVSDK 往返任务；两套控制程序不能同时控制同一仿真机。参考项目：[px4_vision_landing_staticTag](https://github.com/09priyamgupta/px4_vision_landing_staticTag)。

## V1.0 目标（保留）

Ubuntu 24.04 + PX4 SITL + Gazebo Harmonic + X500 + QGroundControl + MAVSDK C++：

起点 H → 安全检查 → 起飞约 3m → 固定目标 A → 独立平坦平台降落 → 确认着陆、解除武装及电机停转 → 等待至少 10 秒 → 再次安全检查 → 起飞 → 返回最初 H → 降落停转。

同一仿真会话至少连续成功 3 轮，正常流程无人工操控，并提供日志、错误处理及验收证据。

V1.0 原范围不包含 ROS 2、视觉、SLAM、多航点、清洁机构或清洁算法；本次新增的视觉课程单独验收，不追溯改变 V1.0 规格。不修改已有 ROS 2 工程。

## 阅读顺序

1. [当前进度](CURRENT.md)
2. [静态标记视觉降落计划（当前主线）](docs/VISION_LANDING_PLAN.md)
3. [MAVSDK 个性化学习计划（历史路线）](docs/LEARNING_PLAN.md)
4. [V1.0 实现规格](docs/V1_SPEC.md)
5. [测试与验收](docs/TEST_PLAN.md)
6. [教学流程](docs/TEACHING_PROTOCOL.md)
7. [环境与版本记录](ENVIRONMENT.md)
8. [掌握证据](MASTERY.md)
9. [开发记录](daily/2026-10-16.md)

## 仓库与运行环境

远端仓库为 KiloMing/XP4-project；SSH 地址为 `git@github.com:KiloMing/XP4-project.git`。
本地 macOS 目录用于文档和版本管理；Ubuntu 是仿真实验环境；用户聊天展示 Ubuntu x86_64，MAVSDK 安装截图显示 Ubuntu 24.04 对应包安装成功，版本细节见 [ENVIRONMENT](ENVIRONMENT.md)。

后续源码目录：src/、include/、config/、simulation/、scripts/、tests/、exercises/。初始化提交只包含规划文档；2026-10-16 补充学习记录，2026-10-27 补充视觉课程与适配待办。Ubuntu 中的真实 main.cpp、CMakeLists.txt 尚未取得，源码待同步，不以聊天示例代替。
