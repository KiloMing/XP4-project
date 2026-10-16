# 环境与版本

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
