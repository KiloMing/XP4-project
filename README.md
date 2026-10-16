# 基于 PX4 的无人机自主导航与光伏板清洁系统

当前阶段：V1.0 自主起降与单目标往返仿真。2026-10-16 已完成 PX4 SITL + Gazebo X500 启动、QGC 连接、commander 起降练习，以及 MAVSDK lesson_01 编译链接。**px4_connect 运行与发现飞控尚未验证**；下一步验证系统发现，再学习 Telemetry。

历史：当天初始化时处于规划阶段，尚未安装、构建或运行验证；后续实验见[当日记录](daily/2026-10-16.md)。

## V1.0 目标

Ubuntu 24.04 + PX4 SITL + Gazebo Harmonic + X500 + QGroundControl + MAVSDK C++：

起点 H → 安全检查 → 起飞约 3m → 固定目标 A → 独立平坦平台降落 → 确认着陆、解除武装及电机停转 → 等待至少 10 秒 → 再次安全检查 → 起飞 → 返回最初 H → 降落停转。

同一仿真会话至少连续成功 3 轮，正常流程无人工操控，并提供日志、错误处理及验收证据。

不包含 ROS 2、视觉、SLAM、多航点、清洁机构或清洁算法。不修改已有 ROS 2 工程。

## 阅读顺序

1. [当前进度](CURRENT.md)
2. [个性化学习计划](docs/LEARNING_PLAN.md)
3. [V1.0 实现规格](docs/V1_SPEC.md)
4. [测试与验收](docs/TEST_PLAN.md)
5. [教学流程](docs/TEACHING_PROTOCOL.md)
6. [环境与版本记录](ENVIRONMENT.md)
7. [掌握证据](MASTERY.md)
8. [开发记录](daily/2026-10-16.md)

## 仓库与运行环境

本仓库通过 SSH 关联 git@github.com:KiloMing/XP4-project.git。
本地 macOS 目录用于文档和版本管理；Ubuntu 是仿真实验环境；用户聊天展示 Ubuntu x86_64，MAVSDK 安装截图显示 Ubuntu 24.04 对应包安装成功，版本细节见 [ENVIRONMENT](ENVIRONMENT.md)。

后续源码目录：src/、include/、config/、simulation/、scripts/、tests/、exercises/。初始化提交只包含规划文档；本次补充实际学习记录。Ubuntu 中的真实 main.cpp、CMakeLists.txt 尚未取得，源码待同步，不以聊天示例代替。
