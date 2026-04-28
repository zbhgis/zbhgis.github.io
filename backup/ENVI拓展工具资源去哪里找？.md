# ENVI拓展工具资源去哪里找？

[TOC]



## 前言

ENVI 拓展工具是指 ENVI 软件的扩展功能或插件。这些扩展工具可以帮助用户增强 ENVI 的功能，使其能够执行更多高级任务。本文所指的拓展主要包括Extension、Task等多方面可以提高效率和提供便捷的工具和代码，以下是根据自己的使用经验总结出来的，如有不足欢迎指正！

## 网站（链接见文末）

### ENVI应用商店（App Store）

**ENVI App Store：**本身就是一个拓展工具，支持 ENVI 5.3及以上版本，需联网使用，低版本需要自己手动下载安装；是官方在维护，其中的内容更新频率较高，上面的插件也基本都是官方提供的。

**App Store主页：**在主页上有下载链接、使用手册、应用列表三个入口

![image-20240508161431180](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270851948.png)

**App Store 使用手册：**对App Store的功能介绍、安装方法等都十分详尽

![image-20240508161912689](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270851900.png)

**App Store 应用列表：**支持搜索功能，不同拓展工具所需要的版本以及详细作用都有注明（在软件内部打开的App Store界面也类似），截止发文时间，有97个工具

![image-20240508162137855](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270851471.png)

### ENVI官方提供

**ENVI国内官方博客/微信公众号：**在ENVI技术殿堂上会更新拓展工具，会对拓展工具作出更加详细的解释，大部分都会更新在App Store中

![image-20240508170320910](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270851966.png)

**ENVI教学资料：**ENVI国内的培训或者网络上的官方视频教学资料中，有不少好用的拓展工具、插件、Task、IDL代码示例等，可以直接下载使用，下面举了两个例子，没记错的话当时是在教学资料中下载的

ENVI Extension：Subset Data from Shapefile Batch，可以批量不规则裁剪

![image-20240508163839016](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270851921.png)

ENVI Modeler中的Task：Generate Output Filename，可以自定义输出文件的后缀

![image-20240508164019165](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270852322.png)

**ENVI的国外网站：**相对来说，里面提供的资源较少（也可能是我没找到），可以用来了解一下最新的资讯

![image-20240508182450619](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270852732.png)

### 第三方制作

第三方制作的插件主要是一些用户根据自己的实际需要编写的拓展/插件/代码，会分享在自己的仓库和博客上，比如Github

![image-20240508165009346](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270852625.png)

### 自己制作

通过ENVI Modeler和IDL二次开发可以快速开发一些适合自己使用的工具，教程官网和b站上通过关键词即可搜到

**ENVI Modeler：**是一个可视化的开发工具，类似于ArcGIS的模型构建器，但是自由度和功能齐全性相对较低，局限性很大，适用于一些简单的工作流的封装搭建

![image-20240508163633969](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270852646.png)

**IDL：**是ENVI内置的一个开发平台，有自己的语法，也有对应的VScode插件可以在VScode上进行代码的编写，适用于想要使用ENVI内部功能以及希望有更高自由度的用户

![image-20240508164520979](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270852027.png)

![image-20240508170136896](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270852473.png)

## 总结

一般来说，ENVI App Store和ENVI 官方提供的资源就够轻度用户使用了；ENVI拓展工具/插件主要是补足一些本身没有的功能（比如批处理、不同传感器图像的读取等），不同的群体侧重点不同，根据自己需要下载，需要注意的就是插件的适用版本，因为我现在用的是ENVI 6.0，可以使用绝大多数的拓展、插件，不想去深究版本问题的话（比如我），就直接把搜集来的拓展一股脑安装就行，哪个可以打开就表示哪个可以被当前版本兼容

## 参考

[ENVI App Store (geoscene.cn)](https://envi.geoscene.cn/appstore/)

```
https://envi.geoscene.cn/appstore/
```

[Geospatial Solutions & Analytics | Geospatial Data Analysis (nv5geospatialsoftware.com)](https://www.nv5geospatialsoftware.com/)

```
https://www.nv5geospatialsoftware.com/
```

[ENVI-IDL技术殿堂 - 博客园 (cnblogs.com)](https://www.cnblogs.com/enviidl)

```
https://www.cnblogs.com/enviidl
```

[ENVI/IDL\] 遥感应用与开发培训班资料分享 (qq.com)](https://mp.weixin.qq.com/s/3OWjwwPwVXHFjdIKsSfPCg)

```
https://mp.weixin.qq.com/s/3OWjwwPwVXHFjdIKsSfPCg
```

[Repository search results (github.com)](https://github.com/search?q=ENVI+IDL&type=repositories&s=&o=desc)

```
https://github.com/search?q=ENVI+IDL&type=repositories&s=&o=desc
```

