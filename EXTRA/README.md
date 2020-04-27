

# EXTRA

## 简介
这个目录主要是存放一些增强性补丁，一些特定机型及特定补丁会存放在这个目录下

### Kexts
### AppleSSD.kext
这个Kext是一个空壳补丁，主要是将Generic SSD Controller修补为 Apple SSD Controller，只有装饰作用，对睡眠唤醒没有帮助，纯粹为了强迫症。

![](https://img.hyejeong.cn/200427/X1.jpg)

不同的固态硬盘的硬件信息也不一致，需要通过Hackintool获取供应商ID和设备ID。

![](https://img.hyejeong.cn/200427/X2.jpg)

打开Kexts - AppleSSD.kext - Info.plist ，把固态的硬盘的供应商ID和设备ID替换IOPCIMatch。

IOPCIMatch为 「0x + 设备ID + 制造商ID」
比如我的 设备ID是0x2262 制造商ID为0x126F 拼接后变成 0x2262126f

![](https://img.hyejeong.cn/200427/X3.jpg)
