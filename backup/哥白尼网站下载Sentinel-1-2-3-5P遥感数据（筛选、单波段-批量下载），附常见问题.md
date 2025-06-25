# 哥白尼网站下载Sentinel-1/2/3/5P遥感数据（筛选、单波段/批量下载），附常见问题

## 前言

之前就看到有人推送这个ESA下载Sentinel数据的新网站https://dataspace.copernicus.eu/browser/，就自己探索了一下，有一些意料之外的功能

## 准备工作

1、刚开始进行点击的是这个界面，目测功能很多，但是先登录才能使用，**点击【Login】按钮进入登录界面**，如果没有账号的话，需要注册一个，在进入这个界面之后如果没有账号，那么就可以**点击【Register】按钮进行注册**，注册的流程与USGS类似，最好使用谷歌邮箱或者163邮箱

![image-20231010205321035](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010205321035.png)

![image-20231010210136221](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010210136221.png)

2.登录之后，点击上面的**【Search】按钮**来到搜索面板，按照下面的图片设置各种条件即可，其中【**Filters】和【Filter by months】可以根据自己的需要进行额外设置**，设置好条件之后可以准备设置区域了

![image-20231010212431533](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010212431533.png)

3.在图层上添加研究边界时，可以上传文件，也可以自行绘制边界，根据需要也可以选择下面的绘制线和地标，点击绘制多边形的按钮之后，直接在地图上通过点击的方法即可完成绘制，完成绘制后就可以点击**左侧的面板最下方的【Search】按钮**，搜索

![image-20231010213213795](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010213213795.png)

![image-20231010213519429](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010213519429.png)

4.搜索结果如下，**左上角的【Go to Search】按钮**可以返回搜索参数设置，重新调整条件；当鼠标在左侧影像上悬停时，右侧对应的方框也会变绿

![image-20231010213737934](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010213737934.png)

## 单幅影像直接下载

5.以下面这幅影像为例，在面板上已经显示了他的数据级别，大小，监测时间等主要信息，![image-20231010214437888](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214437888.png)【Product info】是查看具体的信息，![image-20231010214524305](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214524305.png)【Zoom to product】是在右侧图层上定位，![image-20231010214555074](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214555074.png)【Add to workspace】是添加到工作空间，![image-20231010214800076](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214800076.png)【Download product】是直接下载按钮

![image-20231010214238582](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214238582.png)

【Product info】（进一步显示**图像的具体信息**)

![image-20231010214946260](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214946260.png)

【Zoom to product】（将所选图像**定位到地图中心**）

![image-20231010215012155](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010215012155.png)

【Add to workspace】（**加入到workspace，可以用于后续批量下载，云端处理等**）

![image-20231010215040600](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010215040600.png)

【Download product】（**直接下载数据，下载速度随缘**，我下载的时候是前10%速度很慢，后面的速度可以跑满，下载700MB大概要花15分钟）

![image-20231010215057891](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010215057891.png)

## 单波段下载

这个功能需要点击![image-20231010214437888](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214437888.png)**【Product info】**按钮，找到**【Download single files】**，就可以根据需要**直接下载波段文件**

![image-20231010223748786](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010223748786.png)

![image-20231010224124453](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010224124453.png)



## 在线波段组合显示

1.![image-20231010214858191](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010214858191.png)按钮可以将现有的图像加载到图层上，以上面那副影像为例，可以**默认将图像的真彩色添加至显示**，也可以根据需要切换至不同的波段组合

![image-20231010224909214](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010224909214.png)

2.这些提供的组合不满意也可以在末尾选择**【Custom】**，点击之后可以自行选择波段和指数，也可以通过**【Custom script】**自行修改完成更多的显示

![image-20231010225531107](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010225531107.png)

![image-20231010225547658](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010225547658.png)

![image-20231010225613598](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010225613598.png)



3.在可视化的最初面板中，每个波段组合还附带有如下功能

![image-20231010230101008](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010230101008.png)

添加之后依次存放在各个面板中。在**对比面板中可以尝试对比不同波段和图层的差异，标记面板中的图像可以直接添加到对比面板中**

![image-20231010230854851](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010230854851.png)

## 批量申请离线数据

1.通过进入在线工作空间，可以**申请Sentinel-2离线数据**，选择需要申请的数据，点击**【Add to Processing center】**，出现以下的界面

![image-20231011155441879](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231011155441879.png)



![image-20231010231213704](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010231213704.png)

![image-20231010231601865](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010231601865.png)

2.在**【Processing center】**中，选择需要处理的数据之后，在最上面选择处理类型，本次选择**【Order Sentinel-2 offline products】**，最后点击**【create processing order】**，出现如下界面，根据提示点击即可

![image-20231011155542496](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231011155542496.png)

![image-20231010233000931](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010233000931.png)

![image-20231010233019565](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010233019565.png)

![image-20231010233035506](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010233035506.png)

![image-20231010233418527](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010233418527.png)

3.在**【Processing status】**中，可以看到正在执行的order，由于**本次并未遇到离线数据，仅仅是做个示范**，所以该功能的可靠性和后续操作没法演示了

![image-20231011155637226](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231011155637226.png)

## 批量下载影像

在**【My products】**选择需要批量下载的数据，点击**右下角的【Download】**开始下载，下载速度跟单幅下载没有差别

![image-20231011155717575](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231011155717575.png)

![image-20231010234859052](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010234859052.png)

![image-20231010235545917](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231010235545917.png)

2.关闭上述面板之后，可以在工作空间的主面板的右上角找到![image-20231011000131684](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231011000131684.png)下载标志，重新打开下载任务界面

## 总结

1.这个网站的功能挺齐全的，批量下载，单波段下载都有，总体的使用体验是OK的

2.但是下载速度随缘，暂时不确定是自身网络的原因还是网站的原因

3.推荐下载加入到workspace之后再进行下载，这样可以挂在后台，单幅影像下载貌似不行

