# ENVI6.0试用版（180天）详细安装教程，附安装包链接和一些常见问题

[TOC]



## 前言

如标题所示，这个只是试用版，180天的期限，仅适用于个人学习。下面是我帮朋友安装过程的简单记录，因为之前就有使用过ENVI5.6.3版本，下载流程跟这次的类似，这次安装特地记录一下以及自己遇见的奇葩问题。当然这个版本的相关提供链接可能随时更新，需要及时关注官方博客，不过以下的安装教程和一些常见问题可以提供参考。

## 环境

联想轻薄本+Win11

## 来源

软件来源于ENVI技术殿堂提供的ENVI6.0版本，具体见以下官方文章和官方提供的链接（截止2424.05.23仍可用）

官方博客：[ENVI 6.0 自助试用许可开放申请 - ENVI-IDL技术殿堂 - 博客园 (cnblogs.com)](https://www.cnblogs.com/enviidl/p/16275745.html)

官方提供的网盘链接：https://pan.baidu.com/s/1bW3TY4jo4GjHLFNuMJoCVg?pwd=envi

## 安装

1、打开网盘链接，找到exe和sav文件进行下载

![image-20240523215232120](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271011972.png)

![image-20240523215238247](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271011711.png)

2、下载好之后，双击下载好的exe文件，进入以下界面，点击【Next】继续

![image-20240523215500933](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271011132.png)

3、点击【I accept the agreement】按钮，之后点击【Next】

![image-20240523215545961](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271011365.png)

4、选择安装目录之后，点击【Next】

![image-20240523215619376](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271011876.png)

5、安装内容保持默认，点击【Next】

![image-20240523215709513](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012281.png)

6、安装信息确认好之后，点击【Install】

![image-20240523215734443](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012834.png)

7、等待5分钟左右

![image-20240523215857058](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012035.png)

8、这个时候，根据需要选择是否重启电脑，如果接受直接重启的话，就选择【Yes，...】,反之选【No，...】，自己之后自行重启

![image-20240523215901883](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012145.png)

9、点击【是】，启动许可管理中心

![image-20240523220035917](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012092.png)

10、找到刚刚设置的安装目录，右键打开【属性】，找到【安全】下的【编辑】

![image-20240523221553129](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012658.png)

![image-20240523221540466](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012437.png)

11、选择User后将权限改为【完全控制】，点击【确定】

![image-20240523221709832](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012718.png)

![image-20240523221748319](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012819.png)

12、将电脑重启后，打开ENVI 6.0，ENVI6.0的快捷方式可以在通过【win】键调出程序目录，找到ENVI 6.0

![image-20240523220302324](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012747.png)

13、双击打开，此时可以看到还没有激活，会报错

![image-20240523220420666](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012928.png)

![image-20240523220424710](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271012578.png)

## 激活

1、打开下载的sav文件

![image-20240523221837426](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013437.png)

2、点击【Click to continue】

![image-20240523221846858](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013416.png)

3、一般情况下，这个时候会出现异常，可以按照提示允许应用通过防火墙，或者切换为个人热点。如果没有以下提示，可以直接跳转到以下的第12步

![image-20240523221912628](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013614.png)

4、找到【设置】中的【隐私和安全性】

![image-20240523222026052](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013062.png)

5、点击【Windows 安全中心】

![image-20240523222034551](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013587.png)

6、点击【防火墙和网络保护】

![image-20240523222043302](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013126.png)

7、点击【允许应用通过防火墙】

![image-20240523222050990](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013451.png)

8、点击【更改设置】后，再点击【允许其他应用】

![image-20240523222107871](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013698.png)

![image-20240523222129935](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013327.png)

9、点击【添加】

![image-20240523222139376](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013694.png)

10、在安装位置（如D:\Program Files\NV5\ENVI60\IDL90\bin\bin.x86_64）中，找到以下文件后，点击【添加】

![image-20240523222146931](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013757.png)

![image-20240523222154621](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013301.png)

11、再在该界面选择勾选【专用】和【公用】

![image-20240523222205904](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013990.png)

12、这个时候重新打开sav文件，就可以进入以下界面，填写个人信息后，点击【确定】

![image-20240523222217607](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013319.png)

13、点击如下的【激活适用许可】

![image-20240523222225438](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271013671.png)

14、成功激活之后会显示有效日期和剩余天数，每个月可以重新申请，每次激活会消耗总天数

![image-20240523222236234](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014906.png)

15、这个时候再打开ENVI6.0的快捷方式，即可正常打开

![image-20240523222852055](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014884.png)

![image-20240523222844450](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014202.png)

## 问题

1、sav文件（许可申请工具）打不开，如下所示。

主要是比较常见的防火墙问题，在上述激活步骤中已经演示过了；或者也有可能是网络问题，在激活之前把网络切换为手机热点（激活完记得切换回来）

![image-20240523221912628](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014611.png)

2、sav文件在安装完其他软件之后，不是用IDL激活工具打开，如下所示。

比如说当电脑在装完ENVI 6.0之后，又安装了SPSS软件，而SPSS软件也会识别sav格式的文件并默认使用其打开sav。此时右键该sav文件，打开【属性】，之后选择打开方式为【IDL Runtime to run an IDL Program】（如D:\Program Files\NV5\ENVI60\IDL90\bin\bin.x86_64）后，点击确定即可

![image-20240523223838077](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014113.png)

![image-20240523223959394](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014636.png)

3、ENVI有时候可能会突然打不开，等了好久一直停留在加载界面。

这个问题的一个解决方法，我之前这篇文章的文末提及了，这里就略过了

[ENVI不同版本个人使用对比_-CSDN博客](https://blog.csdn.net/zbh13859825167/article/details/138293186)

```
https://blog.csdn.net/zbh13859825167/article/details/138293186
```

4、深度学习等拓展模块怎么没有。

拓展模块需要自己在网盘链接中再去下载并安装，安装流程类似。

5、无法识别机器码，如下所示。

这个的解决方式官方也提供了，具体的目录需要根据自己安装路径决定。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271014185.png)

