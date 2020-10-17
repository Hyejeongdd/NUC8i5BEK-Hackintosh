

# NUC8i5BEK Big Sur Guide

## 前言
这不是一个万能的Q&A安装教程，需要根据自身的配置情况对配置文件的调整，不同的分辨率可能需要调节不同的参数，如果你还有很多疑惑，欢迎拜读 @weachy 撰写的黑苹果新手指南Q&A。

[黑苹果新手指南Q&A](https://zhuanlan.zhihu.com/p/165596210)

## 机型配置
机型的配置信息基本不会发生大的变化，仅有可能更新BIOS版本或更换显示器，对基础配置不太影响。

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
        <td>WD BLACK SN750 NVMe™ SSD 500GB </td>
   </tr>
   <tr>
        <td>显卡</td>
        <td>Intel Iris Plus Graphics 655</td>
   </tr>
   <tr>
        <td>显示器</td>
        <td>Dell UltraSharp U2718Q（3840 x 2160）</td>
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
        <td>BECFL357.86A.0083.2020.0730.1436（Version 0083）</td>
   </tr>
</table>

## 注意事项
内置的Intel无线网卡目前可以通过第三方的驱动使用，部分功能可能不可用或不稳定，因为我的机器已经硬改了苹果网卡并屏蔽了内置网卡，所以本篇文章不会围绕如何驱动内置的Intel无线进行讨论。

## 准备工具

- macOS 镜像 推荐 @黑果小兵 制作的Clover & OC 二合一版本
- Etcher 镜像制作工具
- DiskGenius 磁盘分区工具
- 一枚大于16GB的可移动磁盘
- 一台备用的电脑 可以进行修改plist和替换EFI的操作

## 调试工具

- Hackintool
- OpenCore Configuration
- ProperTree
- Intel Power Gadget

以上工具都是持续更新的状态 文件下载区不会提供某个版本的包下载 而是选择直链下载 部分下载地址在境外 可能需要自备梯子

## 镜像写入

镜像写入的方式有五花八门，Transmac、Etcher等工具都可以将镜像写入磁盘。

我这里示例使用的是@黑果小兵制作的镜像，使用Etcher工具写入安装的磁盘。

下载后记得使用工具校对MD5值，以免造成不必要的安装麻烦。

写入的方式也很简单，打开Etcher后选择镜像、选择磁盘，点击刷写即可完成苹果引导磁盘的制作。

<a href="https://img.hyejeong.cn/201015/X1.png">![](https://img.hyejeong.cn/201015/X1.png)</a>

## 安装前的调整

在开始安装之前，可能需要根据屏幕的分辨率对config.plist进行一定的修整。

如果你的操作电脑是macOS系统，可以使用OpenCore Configuration进行操作，为了全平台的兼容，本文中将以ProperTree进行示例操作。

- Config—NVRAM—Add-4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14
    UI-Scale的数值决定了UI的显示模式，如果你的显示器支持HIDPI的UI显示模式，请保持数值为02，否则修改为01
    <a href="https://img.hyejeong.cn/201015/X2.png">![](https://img.hyejeong.cn/201015/X2.png)</a>
    
- Config—UEFI-Output-Resolution
    Resolution的数值设置控制台的屏幕分辨率，如果你不确定显示器的分辨率，填入Max即可。
    <a href="https://img.hyejeong.cn/201015/X3.png">![](https://img.hyejeong.cn/201015/X3.png)</a>

## 替换EFI文件
在上述修改完成以后，就是对安装磁盘的EFI配置进行替换，如果你的操作电脑是macOS系统，可以使用OpenCore Configuration进行操作，Windows系统可以使用DiskGenius进行操作。

## BIOS配置
一些资料指出我们需要调整一些BIOS的设置以获得更好的macOS体验。
这里以0083版本的BIOS为基准版本，分享一些我个人对BIOS的修改配置。

Devices - Video
- IGD Minimum Memory 64MB
- IGD Aperture Size 256MB

Devices - Onboard Devices 
如果是经过硬改的版本 需要关掉板载的蓝牙和WLAN来避免冲突 同时需要打开SD Card的读写功能保证拆机卡的正常运行

- WLAN 关闭
- Bluetooth 关闭
- SD Card Read/Write 打开

Security - Security Features
- Inter® Virtualization Technology 打开
- Inter® VT for Directed I/O (VT-d) 关闭
- Inter® Software Guard Extension(SGX) 关闭

Power - Secondary Power Settings
- PCIe ASPM Support 打开

Boot - Boot Configuration - UEFI Boot
- Fast Boot 关闭

Boot - Secure Boot - Secure Boot Config
- Secure Boot 关闭

## 安装macOS
安装的过程这里就不再赘述了，详细的教程就可以拜读 @黑果小兵 撰写的详细教程

[黑苹果新手指南Q&A](https://blog.daliansky.net/MacOS-installation-tutorial-XiaoMi-Pro-installation-process-records.html)

## 三码补齐
Release版本包中为了避免冲突的问题，config.plist的序列号信息都被剔除，在登录ID前，还需要使用工具对遗漏三码进行补全，下文中我以OpenCore Configuration为示例进行演示。

开始之前你需要注意以下问题
1. 不配置该部分OpenCore会自动生成一串序列号，该序列号可能导致无法登陆iCloud
2. 没有正确配置三码可能会导致无法使用FaceTime、iMessage等功能

使用OpenCore Configuration打开config.plist后在左侧找到并选中「PlatformInfo-机型平台设置」，并点击上方的「DataHub - Generic - PlatformNVRAM」

![](https://img.hyejeong.cn/200723/X1.jpg)

![](https://img.hyejeong.cn/200723/X3.jpg)

在底下的箭头选择Macmini8,1 ，OpenCore Configuration会随机生成一套该机型的配置信息，选中右上角的「在config.plist里添加此部分内容」。

![](https://img.hyejeong.cn/200723/X4.jpg)

OpenCore Configuration生成的序列号可能会出现不可用或者不存在序列号的情况，如果需
要正确机型序列号，可能还需要多次进行摇号并验证。

## 工具下载
[OpenCore Configuration](https://mackie100projects.altervista.org/apps/opencoreconf/download-new-build.php?version=last)

[Hackintool](https://github.com/headkaze/Hackintool/releases/latest/download/Hackintool.zip)

[ProperTree](https://github.com/corpnewt/ProperTree)

[Intel Power Gadget](https://software.intel.com/content/www/us/en/develop/articles/intel-power-gadget.html#attachment-heading)

## 致谢
- 感谢 acidanthera 的团队为黑苹果研究做出的贡献
- 感谢 黑果小兵、宪武、xjn 等提供的教程和技术支持
- 感谢 weachy 提供的黑苹果新手指南Q&A
