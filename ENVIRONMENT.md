# 环境与版本

## 已知与待确认

| 项目 | 事实或计划 | 证据边界 |
|---|---|---|
| 规划与版本管理 | macOS 本地目录 /Users/a1-6/Desktop/XP4_project | 本次可访问 |
| Ubuntu | 目标 24.04 | 当前执行环境待核验 |
| 虚拟化与架构 | 旧学习仓库记录 Parallels / aarch64 | 历史记录，不代替本次检测 |
| PX4 | 支持目标组合的稳定发布标签 | 具体标签与提交号待兼容测试后锁定 |
| Gazebo | Harmonic | 已安装版本、包来源待确认 |
| MAVSDK C++ | 固定发布版本 | ARM64 包或源码构建路径待确认 |
| QGroundControl | 适配实际架构的稳定版本 | 安装方式待确认 |
| 编译环境 | CMake、C++ 编译器、Git及版本所需依赖 | 版本待检测 |

旧仓库记录的 Ubuntu 小版本等信息未经本次验证，不直接写成当前事实。

## 环境验收

1. 记录系统、架构、CPU/内存、图形加速与可用磁盘。
2. 核查 PX4/Gazebo/MAVSDK/QGC 的版本与架构兼容。
3. 在独立终端与目录运行，不全局改写旧 ROS 2 工作区或删除其依赖。
4. 简单 X500 场景连续运行至少 10 分钟，记录实时率和资源占用。
5. QGC 和 MAVSDK 同时接收遥测，记录实际 UDP 地址/端口及主机、虚拟机网络关系。
6. 完整重启后重复启动，保存命令和输出。
7. 冻结版本、安装来源、PX4 提交号、模型版本和参数差异。

环境适配预算 4～8 小时；若遇架构/图形阻塞，先定位再调整运行环境，不反复盲目重装。不把支持 Ubuntu 24.04 等同于 ARM 虚拟机组合已验证。

参考：https://docs.px4.io/main/en/dev_setup/dev_env_linux
https://docs.px4.io/v1.17/en/sim_gazebo_gz/index
https://docs.qgroundcontrol.com/en/getting_started/download_and_install.html
