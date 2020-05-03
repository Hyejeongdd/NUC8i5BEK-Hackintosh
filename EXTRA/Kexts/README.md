
## AppleSSD.kext
### 前言
这个Kext是一个空壳补丁，主要是将Generic SSD Controller修补为 Apple SSD Controller，只有装饰作用，对睡眠唤醒没有帮助，纯粹为了强迫症。

### 操作步骤
![](https://img.hyejeong.cn/200427/X1.jpg)

不同的固态硬盘的硬件信息也不一致，需要通过Hackintool获取供应商ID和设备ID。

![](https://img.hyejeong.cn/200427/X2.jpg)

打开Kexts - AppleSSD.kext - Info.plist ，把固态的硬盘的供应商ID和设备ID替换IOPCIMatch的值。

IOPCIMatch为 「0x + 设备ID + 制造商ID」
比如我的 设备ID是0x2262 制造商ID为0x126F 拼接后变成 0x2262126f

![](https://img.hyejeong.cn/200427/X3.jpg)

保存后的AppleSSD.kext文件放在OC - Kexts文件夹下 并在config.plist - Kernel 内添加并启用Kext

![](https://img.hyejeong.cn/200427/X4.jpg)

### 文件下载
[空壳文件AppleSSD.kext](https://hyejeong.cowtransfer.com/s/12349877e90f44) <br/>
[Hackintool](http://headsoft.com.au/download/mac/Hackintool.zip) <br/>
[ProperTree](https://github.com/corpnewt/ProperTree) <br/>

### 致谢
- 哞提供的空壳配置及IOPCIMatch的计算
- xjn提供的空壳驱动文件
