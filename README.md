# 基于 PX4 的无人机自主导航与光伏板清洁系统

当前阶段：V1.0 自主起降与单目标往返仿真。项目处于规划阶段，尚未安装、构建或运行验证。

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
本地 macOS 目录用于文档和版本管理；Ubuntu 才是计划中的仿真执行环境。尚未确认当前 Ubuntu 实测配置。

后续源码目录：src/、include/、config/、simulation/、scripts/、tests/、exercises/。本次只提交规划文档，不生成实现代码或假测试结果。
