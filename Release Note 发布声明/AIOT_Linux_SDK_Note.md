---
title:  AIOT Linux SDK Note
subtitle:
author: Allwinner
changelog:
- ver: 1.0
  date: 2024.01.22
  author: AWA1727
  desc: 初始版本。
- ver: 1.1
  date: 2024.06.22
  author: AWA0511
  desc: add V1.1 sdk note
- ver: 1.2
  date: 2024.08.02
  author: AWA0511
  desc: add V1.2 sdk note
- ver: 1.3
  date: 2024.11.22
  author: AWA0511
  desc: add V1.3 sdk note
- ver: 1.4
  date: 2024.12.30
  author: AWA0511
  desc: add V1.4 sdk note
- ver: 1.4.5
  date: 2025.3.27
  author: AWA0511
  desc: add V1.4.5 sdk note
- ver: 1.4.6
  date: 2025.6.09
  author: AWA0511
  desc: add V1.4.6 sdk note
- ver: 1.4.8
  date: 2025.9.30
  author: AWA0511
  desc: add V1.4.8 sdk note
- ver: 1.4.9
  date: 2026.3.30
  author: KPA0603
  desc: add V1.4.9 sdk note
- ver: 1.4.10
  date: 2026.5.6
  author: KPA0603
  desc: add V1.4.10 sdk note
- ver: 1.5.0
  date: 2026.7.13
  author: KPA0603
  desc: add V1.5.0 sdk note
---

# 前言

## 文档简介

通过本文档可了解AIOT Linux SDK 不同版本对应的文档版本、主要内容变化。

## 目标读者

面向使用AIOT Linux开发者，想了解全志AIOT LINUX SDK的开发者们。

## 适用范围

A523/A527/T527/A733/T736/A537/A333 AIOT Linux平台。

## 发布记录

- V1.5.0(alpha) Note

**公共部分**

**Buildroot 相关**

1. **重要：支持 Weston 完整硬件加速通路，包括 DE composite、G2D rotate、DE cursor 和 dmabuffer direct_display**
2. 支持 eudev 自动挂载 SD、mmcblk、NVMe 等设备
3. 修复 G2D sample 编译错误，并重构为 DMA-HEAP 分配方式
4. 修复 构建时 clean 无效的问题
5. 修复 GStreamer 部分 plugin 未编译的问题，支持更多音视频格式编解码
6. 修复 部分配置下 pulseaudio demo 未编译的问题

**Debian 相关**

1. **重要：支持 Xorg 完整硬件加速通路，包括 DE composite、G2D rotate、DE cursor 和 dmabuffer direct_display**
2. **注意：当前 Debian 下所有 GPU 为 Mali G57 的芯片（包括 A523/A527/T527/A537/A333）由默认使用开源通路（Mesa3D + panfrost）改为使用商用通路（Mali DDK + Valhall），此改动将带来约 25% 的 GPU 性能提升，但对 API 的支持情况可能会有些许差异，请知悉。**
3. 支持 图形系统 deb 包标准化，新增并拆分 xfwm4、Mali X11 GPU 包

**图形显示与多媒体**

1. **重要：支持 Cedar 解码库完整 AFBC 通路，最高支持 4K@60f 播放，具体参考芯片规格**
2. 支持 Uboot 下 Bootlogo 缩放和旋转显示
3. 修复 pulseaudio 配置问题，此问题曾导致部分平台下 gst 播放媒体时音频缺失。
4. 修复 gst-play 在快进时有小概率退出的问题
5. 修复 gst-play 在播放部分媒体时，快进将导致静音的问题
6. 优化 环境变量配置，增加常用变量缺省值，现在可以随意使用 gst-play、glmark 等命令而无需进行额外配置

**基础功能与稳定性**

1. 修复 部分编译配置下 autoconfig 会导致 rootfs 设置异常的问题，并优化 kernel patch 检查流程
2. 修复 DSI 中断风暴问题，提升运行稳定性
3. 修复 PCIe/PHY noirq 阶段唤醒异常问题，提升系统休眠唤醒可靠性
4. 修复 combo0 与 DP 共享场景下 USB u2only 配置异常问题
5. 修复 USB DMA 中断清除问题，降低 USB 传输异常风险
6. 修复 HDMI detect 冗余日志问题，减少系统日志干扰
7. 更新 AIC8800 驱动和固件，优化 Wi-Fi 和 Bluetooth 稳定性

**A733/T736 芯片系列**

1. **重要：支持 Chrome 浏览器GPU硬件加速通路**
2. 商用版 GPU 库 支持 GLX 与 gallium swrast
3. 修复 Xorg(Debian) 下 glxinfo 异常返回的问题
4. 修复 UART 引脚配置错误
5. 修复 Buildroot 下 exFAT、NTFS 文件系统支持缺失的问题

**A523/A527/T527 芯片系列**

1. 修复 Mali-Valhall GPU 驱动在 Linux 5.15 和 6.6 内核下的兼容性问题
2. 修复 Weston 采用 GPU 渲染时的光标残影问题
3. 降低 GPU DVFS 控制台打印等级，减少冗余的日志输出

**A333/A537 芯片系列**

1. 新增 A333 系列芯片支持
2. 修复休眠唤醒后 xHCI 异常导致后续休眠失败的问题
3. 修复特定 reset 路径下 CPUIDLE 状态机异常问题

**未支持项(下一个版本或者补丁形式支持):**

1. VIN框架兼容v4l2标准调用方式 (规划中)

- V1.4.10(alpha) Note

**A733/T736芯片系列**

1. 修复 UART 引脚错误
2. 支持 HEVC 编码器（Debian & Buildroot）

**A537芯片系列（本次重点更新）**

1. **重要：新增A537芯片 BSP 支持**
2. 支持 Buildroot & Debian 基础构建
3. 支持硬件编解码功能
4. 支持 SPI-NAND 安全启动
5. 支持多种外设配置（UART、LRADC、GPADC、PWM、SPI-NG、IRRX、IRTX、LEDC 等）
6. 支持网络功能（GMAC、WiFi/蓝牙）
7. 支持显示功能（DRM、DRM_EDP、PPU）
8. 支持电源管理功能（HUSB311、AXP1530、待机、CPU频率、热插拔）
9. 支持存储功能（EXFAT/FAT、SDMMC、SPI-NAND）
10. 支持系统功能（HWSPINLOCK、MSGBOX、NSI、Timer、VE）
11. 支持多媒体功能（VIN、音频）
12. 支持启动引导功能（U-Boot NAND、时钟、boot0）
13. 支持安全功能（SMC、SID）
14. 支持 PCIe、CE 加密引擎等功能

**未支持项(下一个版本或者补丁形式支持):**

1. A333 系列芯片 BSP 支持（进行中）

- V1.4.9(alpha) Note

**公共部分**

1. 解决 uart-ng 低波特率传输错误问题
2. 解决 pmic usb 功率限制竞争条件和原子上下文问题
3. 解决 部分 avi 视频播放卡死问题
4. 解决 特定场景下 Gstreamer v4l2src 出现死锁的问题
5. 解决 weston 的 transform 失效问题 (Buildroot)
6. 解决 非首次构建时未自动清除配置的问题 (Debian)
7. 解决 卡启动失败问题
8. 解决 raw sensor 与 yuv sensor 混接时取图异常的问题
9. 新增支持 uart 模块 rs485 9bit 和 flow ctrl
10. 新增支持 dw pcie 驱动
11. 新增支持 nvme rootfs
12. 新增支持 双显下 bootlogo 单独创建 fb
13. 新增支持 deb 包标准化安装 (Debian)
14. 新增支持 Gstreamer v4l2src 从配置文件读取 ISP 参数
15. 新增支持 nand 存储介质下 rootfs 构建
16. 新增支持 Gstreamer waylandsink 显示延迟统计信息
17. 新增支持 spi-nand 启动
18. 新增支持 通过 spl-dts 选择 phykey 类型
19. 新增支持 通过 sys_config 配置 Debug 串口波特率
20. 优化 twi 外设兼容性
21. 优化 libcedarc 和 libcedarx 编解码性能
22. 优化 构建与打包工具

**A733/T736芯片系列**

1. 解决 部分不合理的异常打印
2. 解决 GPU 唤醒时的空指针/死锁问题
3. 解决 linux-6.6 的 nvme io 超时问题
4. 解决 UART 引脚配置错误问题
5. 新增支持 pstore 在系统崩溃时, 将错误日志转写到存储介质
6. 新增支持 spinand 物料 GD5F4GQ6UEY1G
7. 新增支持 spinor 安全启动
8. 新增支持 demo_aiot 板型
9. 优化 ddr 驱动性能
10. 优化 USB3.0 兼容性

**A523/A527/T527芯片系列**

1. 解决 usb 重启压力测试下的复位超时问题
2. 解决 GPU 在特定场景下工作异常的问题
3. 解决 特定场景下 raw sensor 通过 v4l2src 取图失败的问题(Debian)
4. 新增支持 panfrost 架构GPU驱动
5. 新增支持 linux-6.6 内核 standby 功能
6. 新增支持 spi-nand 物料 XT26G01D 和 GD5F1GM7UEYIG
7. 新增支持 quick-config 进行 USB3.0 和 PCIE 配置切换
8. 新增支持 spinand 介质 buildroot rootfs 配置参考 (pro3_linux_aiot_nand)

**未支持项(下一个版本或者补丁形式支持):**

1. chrome浏览器加速支持 (A733/T736系列支持) (规划中)
2. 4K UI点对点方案支持 (规划中)
3. VIN框架兼容v4l2标准调用方式 (规划中)

- V1.4.8(alpha) Note

**公共部分**

1. 解决 运行部分程序后，weston显示异常的问题(Buildroot)
2. 解决 4线或9线 uart 在特定场景下导致系统卡死的问题
3. 解决 HDMI 启动后无信号的问题
4. 新增支持 Linux 6.6 LTS 内核版本
5. 新增支持 sdcard/nor启动下识别ufs设备
6. 新增支持 DPDK 方案
7. 新增支持 Gstreamer + CSI 框架 (带ISP效果)
8. 新增支持 UFS / EMMC 烧录同一固件
9. 新增支持 AW启动方式与extlinux启动方式兼容
10. 新增支持 OpenCL / GL 演示 Demo (Buildroot)
11. 新增支持 Tiger ISP 效果调试工具支持
12. 新增支持 DFS 动态调频 (默认关闭)
13. 新增支持dragonboard板卡测试套件（linux-6.6）
14. 新增debian NPU基础方案
15. 新增支持DP OUT功能支持
16. 新增weston版本升级至12.0.1(buildroot)
17. 优化 hdmi 接口兼容性
18. 优化deb包格式(debian系统)
19. 优化启动方式：兼容aw启动方式和extlinux启动方式

**A733/T736芯片系列**

1. 解决 特定 16G 及以上 LPDDR5 物料无法烧录启动的问题
2. 新增支持 Super Standby
3. 新增支持 dp out 显示输出
4. 新增支持 电池快充方案适配 (AXP517)
5. 优化 edp 接口兼容性
6. 优化 pcie 接口兼容性, 改善nvme识别成功率

**A523/A527/T527芯片系列**

1. 新增支持 RV, A55 核间通信(amp)方案(参考: T527 demo_linux_aiot_amp)


**未支持项(下一个版本或者补丁形式支持):**

1. AFBC完成通路支持(下一版本迭代)
2. 支持 xorg 使用 DE 合成(下一版本迭代)
3. chrome浏览器加速支持 (A733/T736系列支持)(规划中)
4. 4K UI点对点方案支持(规划中)

- V1.4.6(alpha) Note

**公共部分**

1. 解决ubuntu下Linux LiveSuit工具概率性烧录失败问题
2. 解决nvme概率性启动异常问题
3. 解决插着type-c启动，概率性进入充电模式问题
4. 新增支持ros2方案(debian)
5. 新增支持wifi/bt(debian)
6. 新增支持TP(debian：T527 demo/T736 demo方案)
7. 新增支持gstreamer适配CSI(demo sensor: imx319)
8. 新增支持boot支持双存储(nor+emmc/nor+ssd)
9. 新增支持boot支持NVME
10. 新增支持extlinux支持(与AW启动方式二选1)
11. 优化edp信号通信质量
12. 优化部分MMC读写速率
13. 优化PCIE通信速率
14. 优化音频策略

**A733/T736芯片系列**

1. 新增支持nor方案，参考(方案 T736 evb_nor)
2. 新增支持ufs自动烧写功能
3. 新增支持boot支持gmac
4. 新增支持安全烧写功能(默认关闭)
5. 新增支持G2D
6. 新增支持OTA方案(buildroot)
7. 新增支持gstreamer硬件解码功能
8. 新增支持ISP功能
9. 新增支持GPU硬件加速(默认方案：debian：X11/ buildroot:wayland)
10. 新增支持yocto方案(T736)
11. 优化dram驱动,增强(LPDDR5/LPDDR4)兼容性,dram版本升级至V0.601
12. 优化VF,增强CPU兼容性,VF版本升级至V0.9
13. 优化wifi(AIC8800)稳定性,驱动版本升级至20250410-008

**A523/A527/T527芯片系列**

1. 新增GPU使用方式适配(vulkan/gbm+kms/wayland)
2. 新增支持chromium(适配硬件加速)(补丁方式提供)

**未支持项(下一个版本或者补丁形式支持):**

1. sdcard/nor启动下识别ufs设备(下一版本支持)
2. chrome浏览器加速支持 (A733/T736系列支持)(规划中)
3. AW启动方式与extlinux启动方式兼容(下一版本支持)
4. 4K UI点对点方案支持(规划中)
5. 方案丰富: OpenCL demo方案应用/Debian NPU方案应用/DP OUT方案应用/快充方案应用/多屏方案应用/DPDK方案应用等(下一版本迭代)

:::note
备注：板卡参考方案：

1. A523 pro3_linux_aiot

2. A527 pro2_linux_aiot

3. T527 demo_linux_aiot

4. A733 pro3

5. T736 demo_aiot

5. T736 evb_nor
:::


- V1.4.5(alpha) Note

**新增A733/T736 芯片方案支持(Linux5.15 LTS)**

1. 支持AI基础系统(基于buildroot)
2. 支持buildroot基础系统(buildroot 2022.05)
3. 支持debian基础系统(基于debian11)
4. 支持以太网(kernel)
5. 支持PCIE(kernel)
6. 支持显示完成方案(MIPI/LVDS/eDP/HDMI out)
7. 支持weston(buildroot, 默认)
8. 支持xfce(debian, 默认)
9. 支持boot U盘识别
10. boot支持PCIE
11. boot支持SSD
12. 支持EMMC/UFS
13.  支持alsa
14.  支持pulseaudio

**未支持项(下一个版本V1.4.8或者补丁形式支持):**

1. boot支持双存储
2. boot支持NVME
3. OTA(buildroot)
4. yocto支持
5. chrome浏览器加速支持
6. wayland方案支持
7. gstreamer适配CSI
8. gstreamer编解码
9. nor方案支持
10. extlinux支持

**针对A523/A527/T527平台做相应改进和问题修复**

1. 新增支持yocto(5.1)(默认T527参考方案)
2. 新增支持双存储方案支持(nor+EMMC/nor+SSD)
3. 新增支持NVME(boot)
4. 默认集成V1.4发布版本补丁
4.1. 更新/优化显示模块
4.2. 支持mipi video burst mode，改善mipi接口屏打静电时闪屏问题
5. 修复FB框架双buffer送显异常问题
6. 修复板型默认显示绑定关系异常
7. 修复weston通过gbm申请buffer报错问题

:::note
备注：板卡参考方案：

1. A523 pro3_linux_aiot

2. A527 pro2_linux_aiot

3. T527 demo_linux_aiot

4. A733 pro3

5. T736 demo_aiot
:::

- V1.4 Note

1. 新增：支持OTA(buildroot)
2. 新增：支持weston AFBC压缩特性(buildroot)
3. 新增：libuapi显示中间件支持对接libdrm显示
4. 新增：新增文档仓库，详情见docs目录
5. 新增：使能buildroot BR2_ROOTFS_OVERLAY 特性，支持板级预置板级配置文件；
6. 优化：优化buildrot编译效率，支持buildroot toplevel并行编译(配置BR2_PER_PACKAGE_DIRECTORIES启用)
7. 优化：优化buildroot demo代码结构(buildroot/package/auto demo)，兼容buildroot编译框架；
8. 优化：优化buildroot/config代码结构，配置文件按照platform/源码目录层级归纳分类；

7. 修复：时钟同步问题导致的DRM概率性超时问题
8. 修复：修复asound.conf中的场景通路，解决使用PlaybackSPK时无声报错问题

9. 不支持：vulkan完整方案，下一个版本V1.5迭代支持
10. 不支持：yocto构建方案，下一个版本V1.5迭代支持
11. 不支持：Gtreamer未适配CSI插件，下一个版本V1.5迭代支持

12. 新增demo：

```
多媒体支持list:
(1). audioenc_test(音频编码)
(2). encoder_test(yuv编码jpg)
(3). trecorderdemo(录像、录音)
(4). tplayerdemo(视频、音频播放)
(5). imagedecodedemo(图片软解)
(6). decoder_test(单路、多路解码功能)
(7). csi_test_usrptr(测试 csi sensor 拍照功能)
(8). usbcam_test(测试 usb sensor 拍照功能)
(9). recorder_demo(大小码流输出功能)
```

:::note
板卡参考方案：

1. A523 pro3_linux_aiot

2. A527 pro2_linux_aiot

3. T527 demo_linux_aiot

:::

:::note

docs目录下的文档的更新可能存在延迟，即最新文档的获取，最新物料支持列表的获取，请通过全志客户服务平台(https://open.allwinnertech.com).

:::

- V1.3 Note

1. 新增：支持ext4(uboot)
2. 新增：支持pcie(uboot)
3. 新增：支持gmac0(uboot)
4. 新增：支持gstreamer编码功能
5. 新增：支持GPU：ddk+wayland方案
6. 新增：支持音频：PulseAudio
7. 新增：支持UI：LVGL (buildroot)
8. 新增：支持NPU基础方案(T527)
9. 新增：支持RV(FreeRtos)基础方案(T527)
10. 新增：支持Debian基础系统
11. 新增：支持docker基础方案
12. 新增：支持Buildroot:valhall + mali ddk+wayland(weston)(默认配置)
13. 新增：支持Buildroot:panfrost + mesa+wayland(weston)
14. 新增：支持Debian: panfrost + mesa + gnome(wayland)
15. 新增：支持Debian: panfrost + mesa + xfce/lxde(x11)(默认配置)
16. 新增：支持工具: mtop(带宽查看)
17. 新增：支持工具：cpu_monitor(cpu占用率和内存调试查看)
18. 优化：优化HDMI信号质量(A527/T527)
19. 优化：电源质量<新增dvm功能,以优化板卡供电方案对大电流场景的兼容性>
20. 优化：Bias电源设置策略<新增自动校正功能,防止误配置导致的IO功能异常>
21. 修复：HDMI输出概率性无信号问题
22. 修复：ACIN方案下：U盘概率性不识别
23. 不支持：AFBC完整方案，下一个版本V1.4迭代支持
24. 不支持：vulkan完整方案，下一个版本V1.4迭代支持
25. 不支持：yocto构建方案，规划支持中
26. 新增若干文档，详情见全志客户服务平台工具:https://open.allwinnertech.com

:::note
板卡参考方案：

1. A523  pro3_linux_aiot

2. A527  pro2_linux_aiot

3. T527  demo_linux_aiot
:::

- V1.2 Note

1. 新增：支持完整DRM功能(lvds/edp/rgb/mipi(单/双)/HDMI-OUT(A527/T527)) (基于Linux-5.15)；
2. 新增：支持bootlogo显示功能(基于Linux-5.15)；
4. 新增：支持快充方案(A527 D10参考方案)(基于Linux-5.15)；
5. 新增：支持SDIO细调功能(基于Linux-5.15)；
6. 新增：支持CSI ISP功能(基于Linux-5.15)；
7. 修复：休眠重启问题(基于Linux-5.15)；
8. 修复：过温(软件)不关机问题(基于Linux-5.15)；
9. 修复：使用RV情况下，ARM端:GPIO中断概率性不生效问题(T527)(基于Linux-5.15)；
10. 修复：GPU内存溢出问题(基于Linux-5.15)；
11. 不支持：DP OUT功能，下一个版本迭代支持

:::note
板卡参考方案：

1. A523 pro3_linux_aiot

2. A527 pro2_linux_aiot

3. T527 demo_linux_aiot
:::

- V1.1 Note

1. 新增：支持A523/A527/T527 bsp/buildroot(基础系统)
2. 新增：可支持A523/A527 ubuntu-22.04系统(基础系统)
2. 新增：支持T527 HDMI OUT功能
3. 新增：支持usb ncm/rndis
4. 修复：休眠唤醒屏幕概率性不亮
5. 修复：休眠唤醒屏幕概率性闪烁问题
6. 不支持：A523/A527 不支持bootlogo, 下一个版本迭代支持
7. 不支持：A527 不支持HDMI OUT功能, 下一个版本迭代支持

- V1.0 Note

1. 可支持ubuntu-22.04文件系统；
2. 支持linux-5.15.147内核版本；
3. 支持同编同解，多编多解，大小码流编码等；
4. 支持DRM显示框架；
5. 支持Panfrost驱动；
6. 支持支持Mesa；
7. 支持Xorg；
8. 支持glamor加速；
9. 支持Gstreamer接口；
10. 支持网络浏览器播放视频
