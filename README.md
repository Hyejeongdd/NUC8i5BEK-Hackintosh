

# NUC8i5BEK Catalina Guide

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
        <td>Dell U2718Q（3840 x 2160）</td>
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

没有选择一些进阶性的配置工具是为了方便用户在最少的时间消耗以及最低的学习成本进行启动文件的配置。

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

## 工具下载
[OpenCore Configuration](https://mackie100projects.altervista.org/apps/opencoreconf/download-new-build.php?version=last)

[Clover Configuration](https://mackie100projects.altervista.org/apps/cloverconf/download-new-build.php?version=global)

[Hackintool](https://github.com/headkaze/Hackintool/releases/latest/download/Hackintool.zip)

## 致谢
- 感谢 acidanthera 的团队为黑苹果研究做出的贡献
- 感谢 黑果小兵、宪武、Xjn、Sukka等提供的教程和技术支持
- 感谢 weachy 提供的黑苹果新手指南Q&A
