# 环境与版本

## 2026-10-27 视觉路线适配表（规划，未安装或复测）

| 项目 | 目标 / 核查内容 | 当前证据 |
|---|---|---|
| Ubuntu | 24.04；核对架构、图形加速、资源与网络 | 沿用下方历史记录，尚无本次系统输出 |
| ROS 2 | Jazzy；独立终端、独立 `~/vision_landing_ws` | 安装版本、RMW、overlay 待核验 |
| Gazebo | Harmonic，与 Jazzy 配套 | 旧 X500 跑通过，实际 Gazebo 版本仍待核验 |
| PX4 / px4_msgs | 按实际 PX4 release/commit 核对消息版本与话题 | PX4 commit 未取得，不能先指定已兼容 |
| Micro XRCE-DDS Agent | 与所选 PX4 client 版本相容 | 来源、版本、端口、通信待验收 |
| ros_gz | 图像、CameraInfo、时钟桥接；记录类型与方向 | 话题名、QoS、频率待测 |
| AprilTag / image_proc | 核查 Jazzy 包来源、组件插件与参数 | 版本、标签尺寸定义与输出 frame 待测 |
| Python / 数值依赖 | 核验系统 Python、NumPy、YAML 与包环境 | 不沿用上游 Python 3.10 假设 |
| 模型与 world | 独立存放；验证资源路径和 PX4 启动配置 | 不覆盖 PX4 内 models/worlds，不假定现成 make target 存在 |
| QGC / MAVSDK | 保留旧环境与 V1.0 记录 | 本次未升级、未重装、未修改源码 |

参考项目基于 Ubuntu 22.04/Humble/Garden，不能只替换名字就认为适配完成。官方选型依据见 [REP-2000](https://github.com/ros-infrastructure/rep/blob/master/rep-2000.rst)、[ROS/Gazebo 配套](https://gazebosim.org/docs/harmonic/ros_installation/)、[PX4 ROS 2 指南](https://docs.px4.io/main/en/ros2/user_guide)。

版本冻结至少记录：系统与架构、PX4 commit 与本地差异、px4_msgs commit、Agent 版本、ROS/Gazebo/ros_gz/检测器包版本、模型与配置版本、依赖来源。先只读盘点，再决定适配；不以重装或全局修改环境变量代替定位。

新的只读核验建议与资源隔离原则见 [视觉计划](docs/VISION_LANDING_PLAN.md)。下方环境验收是 V1.0 保留条目；其中 MAVSDK 双接收不作为视觉课的硬性前置。

## 2026-10-16 实验环境补充（优先于下方初始规划）

| 项目 | 本次事实 | 尚缺证据 |
|---|---|---|
| Ubuntu / 架构 | 用户展示 Ubuntu x86_64；安装截图显示 Ubuntu 24.04 的 MAVSDK 包安装成功 | 完整 os-release、内核、硬件与图形信息 |
| PX4 / Gazebo | SITL + X500 编译、启动成功 | PX4 标签/提交号、Gazebo 实际版本（Harmonic 仍为规划值） |
| QGroundControl | 连接成功，Preflight Check OK | 版本、安装来源 |
| MAVSDK | libmavsdk-dev v4.0.1 amd64 安装成功 | 包来源和完整安装清单 |
| lesson_01 | ~/px4_ws/mavsdk_study/lesson_01；main.cpp + CMakeLists.txt 编译链接成功 | 原始源码待同步；运行、系统发现及实际 UDP 配置待验证 |
| 网络问题 | OpticalFlow GitHub 下载曾因 127.0.0.1:7897 代理失败，修复后成功 | 具体修复命令未归档，不推测全局配置改动 |

证据来自用户聊天实验记录；本次 Codex 未在 Ubuntu 复测。源码读取尝试：已配置的 Ubuntu 地址一个 SSH 超时，另一个认证失败，因此未取得真实代码。旧 aarch64 记录不能代表本次 x86_64 环境。

## 初始化时已知与待确认（历史规划，以下非当前实测结论）

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
