# ENVI通过DEM数据计算坡度、坡向等地形特征

[TOC]

## 前言

这篇文章主要介绍ENVI通过DEM数据计算坡度、坡向等地形特征。在网络上ENVI提取地形相关特征的帖子较少，最近做实验碰到这个问题，记录一下，工具的具体原理见文末参考链接

【Topographic Modeling】工具，可提取出

- Slope
- Aspect
- Shaded Relief
- Profile Convexity
- Plan Convexity
- Longitudinal Convexity
- Cross Sectional Convexity
- Minimum Curvature
- Maximum Curvature
- RMS
- Slope Percent

可以按需计算

## 环境

ENVI 5.3（ENVI 6.0也类似）

## 地形特征提取

在ENVI工具箱中，找到【Terrain】|【Topographic Modeling】，打开之后就可以选择数据，我这里选择了一幅已经投影和裁剪过的ASTER GDEM数据。有需要也可以在打开界面的【Spatial Subset】对数据进行进一步裁切

![image-20240516193053738](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270905366.png)

![image-20240516193251111](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270905518.png)

点击【OK】之后，直接进入到【Topo Model Parameters】界面，【Topographic Kernel Size】，即卷积核大小，默认为3（一般来说，越大生成的结果越平滑）；【Select Topographic Measures to Compute】默认勾选了全部的，可以按需选择；

![image-20240516194422607](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270905661.png)

之后就是【Elevation】和【Azimuth】，即太阳高度角和太阳方位角，这个只有在计算【Shaded Relief】这个特征时需要填写【Elevation】和【Azimuth】，这两个值需要结合具体的影像数据进行填写，比如说现在有一幅LC08_L2SP_125039_20220706_20220722_02_T1影像，想要计算这幅影像对应的【Shaded Relief】，这个时候打开元数据文件可以找到（以这个数据产品为例，是“MTL.txt”结尾的数据文件，打开之后，找到以下两个值，就可以直接填上去了）

![image-20240516194820052](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270905612.png)

如果没有元数据文档，也可以去影像下载的网页中都会提供影像信息，这个时候就可以通过【Compute Sun Elevation and Azimuth】，将影像获取的具体时间以及对应地理位置输入到以下的面板参数中，之后点击【OK】可以直接计算出来

![image-20240516194059523](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270906559.png)

我这次选择全部计算，之后选择输出文件名即可（两个及以上的特征，将作为多波段栅格输出）

![image-20240516200057983](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270906107.png)

输出结果如下所示：

![image-20240516200248465](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270906791.png)

![image-20240516202726855](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270906252.png)

## 补充

在ENVI Model（ENVI 5.5版本之后支持）中，也提供对应的Task，在【Topographic Modeling】，提供的高度角和方位角都是默认45，如果需要计算【Shaded Relief】，尽量按照具体的影像信息去填写

![image-20240516203122281](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270906874.png)

## 总结

虽然ArcGIS的提取地形因子的工具已经挺全面的，但是有时候需要在ENVI中进行流程化处理的时候，使用ENVI内部的地形特征提取功能会节约不少时间

如果要计算【Shaded Relief】，就需要填写高度角和方位角，填写的时候一定不要弄错这两个的顺序

## 参考

[[Topographic Modeling (geoscene.cn)](https://envi.geoscene.cn/help/Subsystems/envi/Content/Topographic/ModelTopographicFeatures.htm)](https://envi.geoscene.cn/help/Subsystems/envi/Content/Topographic/ModelTopographicFeatures.htm)

```
https://envi.geoscene.cn/help/Subsystems/envi/Content/Topographic/ModelTopographicFeatures.htm
```