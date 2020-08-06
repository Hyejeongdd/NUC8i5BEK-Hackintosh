

# NUC8i5BEK Big Sur Guide

## 更新日志
- 2020/07/11 更新OpenCore 0.6.0 + 最新的Lilu + WEG + VSMC ，目前已支持Big Sur Beta 2 正常OTA更新安装
- 2020/07/12 更新AppleALC后声卡可正常使用
- 2020/07/18 日常更新OpenCore及Kext依赖
- 2020/07/23 修改config.plist配置支持Beta 3更新
- 2020/08/06 更新配置支持Beta 4版本

## 前言
这不是一个开箱即用的版本，需要根据自身的配置情况进行配置文件的调整，如果你还有很多疑惑 欢迎拜读 @weachy 撰写的黑苹果新手指南Q&A。

[黑苹果新手指南Q&A](https://www.jianshu.com/p/b298da6afef3)

## 机型配置

<table>
   <tr>
        <td>机型</td>
        <td>Intel NUC KIT NUC8I5BEK</td>
   </tr>
   <tr>
        <td>CPU</td>
        <td>Intel(R) Core(TM) i5-8259U CPU @ 2.30GHz</td>
   </tr>
   <tr>
        <td>内存</td>
        <td>十铨（Team） DDR4 2666 16G X 2</td>
   </tr>
   <tr>
        <td>硬盘</td>
        <td>海康威视 C2000 PRO 1T</td>
   </tr>
   <tr>
        <td>显卡</td>
        <td>Intel Iris Plus Graphics 655</td>
   </tr>
   <tr>
        <td>显示器</td>
        <td>Dell UltraSharp U2720QM（3840 x 2160）</td>
   </tr>
   <tr>
        <td>声卡</td>
        <td>Realtek ALC235</td>
   </tr>
   <tr>
        <td>无线网卡</td>
        <td>BCM94360CS2（1300Mbps + Bluetooth 4.0）</td>
   </tr>
   <tr>
        <td>BIOS</td>
        <td>BECFL357.86A.0078.2020.0309.1538（Version 0078）</td>
   </tr>
</table>

## 开始前需要准备的工具
* OpenCore Configurator
* Clover Configurator
* Hackintool

没有选择一些进阶性的工具是为了方便用户在最少的时间消耗以及最低的学习成本进行启动文件的配置。

## BIOS配置
一些资料指出我们需要调整一些BIOS的设置以获得更好的macOS体验
这里以0078版本的BIOS为基准版本 分享一些我个人对BIOS的修改配置

Devices - Video
- IGD Minimum Memory 64MB
- IGD Aperture Size 256MB

Devices - Onboard Devices 
如果是经过硬改的版本 需要关掉板载的蓝牙和WLAN来避免冲突 同时需要打开SD Card的读写功能保证拆机卡的正常运行

- WLAN 关闭
- Bluetooth 关闭
- SD Card Read/Write

Security - Security Features
- Inter® Virtualization Technology 打开
- Inter® VT for Directed I/O (VT-d) 关闭
- Inter® Software Guard Extension(SGX) Disabled

Power - Secondary Power Settings
- PCIe ASPM Support 打开

Boot - Boot Configuration - UEFI Boot
- Fast Boot 关闭

Boot - Secure Boot - Secure Boot Config
- Secure Boot 关闭

## 三码补齐
在Release版本上，为了避免冲突的问题，config.plist的序列号信息都被剔除，在使用前，您还需要使用工具对三码进行补全，下文中我以OpenCore Configuration为示例进行演示。

开始之前你需要注意以下问题
1. 不配置该部分OpenCore会自动生成一串序列号，该序列号可能导致无法登陆iCloud
2. 没有正确配置三码可能会导致无法使用FaceTime、iMessage等功能

使用OpenCore Configuration打开config.plist后在左侧找到并选中「PlatformInfo-机型平台设置」，并点击上方的「DataHub - Generic - PlatformNVRAM」

![](https://img.hyejeong.cn/200723/X1.jpg)

![](https://img.hyejeong.cn/200723/X3.jpg)

在底下的箭头选择Macmini8,1 ，Configuration会随机生成一套该机型的配置信息，选中右上角的「在config.plist里添加此部分内容」。

![](https://img.hyejeong.cn/200723/X4.jpg)


## 工具下载
[OpenCore Configuration](https://mackie100projects.altervista.org/apps/opencoreconf/download-new-build.php?version=last)

[Hackintool](https://github.com/headkaze/Hackintool/releases/latest/download/Hackintool.zip)

## 致谢
- 感谢 acidanthera 的团队为黑苹果研究做出的贡献
- 感谢 黑果小兵、宪武、Xjn、Sukka等提供的教程和技术支持
- 感谢 weachy 提供的黑苹果新手指南Q&A
