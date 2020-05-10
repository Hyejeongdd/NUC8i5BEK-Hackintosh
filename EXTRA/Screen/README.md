

# 显示器名称及图标自定义方案

## 前言
通过对EDID的修补，我们可以修改显示器样式名称以及添加缩放分辨率开启HIDPI。

这个章节主要是修补「系统偏好设置 - 显示器」以及「关于本机 - 显示器」内的图标显示及设备型号，纯粹为了强迫症进行的修改。

## 开始前需要准备的工具
* Hackintool
* ProperTree
* Finder


## 修改显示器名称
首先需要用Hackintool获取显示器的信息，并生成对应的EDID补丁。

> 不是一定要按照我图中的进行勾选，一些参数的设置可能会影响到显示器的一些功能 （在修补以后2720QM 丢失了高动态范围 选项

![](https://img.hyejeong.cn/200503/X1.png)

进行完导出的操作以后，会导出5个文件并存放在桌面，本章选择使用显示覆盖的方式进行修改，主要需要的文件是「DisplayVendorID-x」

打开「DisplayVendorID-x」文件夹内的「DisplayProductID-x」文件，这里存放了显示器的名称、设备ID、EDID等信息。

如果需要修改显示器的名称，修改DisplayProductName对应的Value值即可。

![](https://img.hyejeong.cn/200503/X2.png)

修改完成后，我们需要将该文件放入系统中以便生效。

如果当前的系统是10.15及以上版本，需要先执行以下命令让系统分区变为可读写
```
sudo mount -uw / && killall Finder
```

前往文件夹「/System/Library/Displays/Contents/Resources/Overrides」将桌面的「DisplayVendorID-x」文件夹拖入，如果出现弹窗，选择合并即可。

## 修改显示器图标

这里需要记录两个参数，接下来的配置中会使用到。
* DisplayVendorID-x 供应商ID
* DisplayProductID-x 设备ID

使用ProperTree打开「Icons.plist」，这里储存了系统预置的显示器图标信息。

查找「vendors」目录下是否有与显示器供应商相同的ID，如果没有，则手动创建一个Key值为供应商ID的目录。

如果找到了与显示器供应商相同的ID的目录，查找「products」目录下是否有与显示器设备相同的ID，如果没有，则手动创建一个Key值为设备ID的目录。

以我的本地为例，显示器的供应商ID为10ac，设备ID为41ba，在系统预设文件中没有对应的参数，手动创建了目录如下图。

![](https://img.hyejeong.cn/200503/X3.jpg)

其中设备目录下需要以下6个参数，其中对应的意义如下

| Key | Type | Value |
|-----|------|-------|
| display-icon | String | 关于本机-显示器 图标 一般后缀为.icns |
| display-resolution-preview-icon | String | 系统偏好设置-显示器 图标 一般后缀为.tiff |
| resolution-preview-height | Number | 图标的高度 |
| resolution-preview-width | Number | 图标的宽度 |
| resolution-preview-x | Number | 图标的x值 |
| resolution-preview-y | Number | 图标的y值 |

配置好以后保存重启即可生效，不同的显示器的宽度高度xy值都是不一样的，文末提供了我目前使用的显示器图标文件及配置文件。

## 文件下载
如果Github文件下载缓慢，可以通过下面的外链进行下载 <br/>
[Hackintool](https://hyejeong.cowtransfer.com/s/82a2c566479045)
[ProperTree](https://hyejeong.cowtransfer.com/s/057759912bf949)
[U2720QM Config](https://hyejeong.cowtransfer.com/s/8d599255a5b542)

## 致谢
- 感谢 黑果小兵 提供的显示器EDID修复教程
- 感谢 wyhtc 提供的图标文件