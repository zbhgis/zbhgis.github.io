# SNAP软件的下载、安装、更新、卸载与遇到的一些问题

## 前言

SNAP（Sentinel Application Platform）是欧洲空间局（ESA）开发的一款软件，主要用于处理和分析遥感数据，特别是来自其Sentinel卫星系列的数据。SNAP提供了多种工具和功能，支持用户进行数据的预处理、可视化、分析和产品生成。 

本文主要介绍SNAP软件的下砸、安装、更新与卸载步骤，软件来自于欧空局官网，文中使用的是Sentinel Toolbox V10.0版本，包含了esa-snap_sentinel_windows-10.0.0.exe，在Windows操作系统进行操作。

## 环境

Win 10

## 下载

可以直接在官网进行下载，建议使用最新版，因为SNAP旧版本对于部分数据产品的支持不是很友好。截止241031，最新版的是10.0版，我下载的是其中的Windows 

[SNAP Download – STEP](https://step.esa.int/main/download/snap-download/)

```
https://step.esa.int/main/download/snap-download/
```

进入以下网站，找到下载界面，根据自己的操作系统选择对应的版本。我下载的是Windows 对应的Sentinel Toolboxes 10.0版本。

![image-20241021121451331](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271025867.png)



## 安装

在安装之前建议完全卸载旧版本。卸载步骤见文末。

双击下载好的exe应用程序

![image-20241021110610334](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271025448.png)

点击【Next】

![image-20241021110646623](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026657.png)

此处为许可条款，默认即可。点击【Next】。

![image-20241021110756233](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026771.png)

此处为之前的安装残留，选择【Deleting all SNAP user data】

![image-20241021110815086](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026880.png)

此处为文件安装路径，选择路径之后，点击【Next】

![image-20241021110839407](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026875.png)

此处为组件选择，默认即可，点击【Next】

![image-20241021110907228](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026237.png)

此处为是否创建开始菜单文件夹，默认即可，点击【Next】

![image-20241021110929821](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026517.png)

此处为是否需要配置Python解释器，如果有需要进行二次开发的可以选择，否则默认即可。点击【Next】

![image-20241021111211880](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026550.png)

经过一段时间的安装之后，弹出以下界面，进行文件关联，默认即可。点击【Next】。

![image-20241021111521555](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026631.png)

取消勾选【Run SNAP Desktop】，点击【Finish】。

![image-20241021111617750](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026907.png)

## 更新

在桌面找到SNAP的快捷方式，点击打开。在以下的弹出界面中选择【Yes】。或者也可以在菜单栏中的【Help】选择【Update】检查更新。

![image-20241021112106345](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026764.png)



![image-20241021112132077](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026230.png)



![image-20241021112156519](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026149.png)



勾选之后，点击【Update】。

![](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026137.png)

在软件左下角会显示进度，下载速度较慢，需要耐心等待。

![image-20241021112427584](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026387.png)

## 卸载

一般来说，如果电脑上已经有旧版本的SNAP了的话，那么就需要进行卸载。

先将软件关闭，右击桌面快捷方式图标，打开【属性】，在属性中点击【打开文件所在位置】

![image-20241021115323091](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271026803.png)

双击打开其中的‘Uninstall.exe”。

![image-20241021121127864](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271027792.png)

## 注意点

1、在安装新版本之前建议完全卸载SNAP，以及根据提示清除对应的配置数据。

2、在安装SNAP之前，查看自己的电脑用户名是否为中文，如果为中文则安装SNAP之后可能无法正常打开哨兵等数据

3、在使用SNAP过程中，如果出现其他问题，可以在以下官方论坛寻找解决方案或者提问

[STEP Forum](https://forum.step.esa.int/)

```
https://forum.step.esa.int/
```
