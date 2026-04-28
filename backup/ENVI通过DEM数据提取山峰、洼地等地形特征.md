# ENVI通过DEM数据提取山峰、洼地等地形特征

[TOC]

## 前言

之前的文章介绍了在ENVI中怎么提取坡度、坡向等地形因子

[ENVI通过DEM数据计算坡度、坡向等地形特征-CSDN博客](https://blog.csdn.net/zbh13859825167/article/details/139023262)

```
https://blog.csdn.net/zbh13859825167/article/details/139023262
```

这篇文章主要介绍ENVI通过DEM数据提取山峰、洼地等地形特征。在网络上关于ENVI提取地形相关特征的帖子较少，其工具的实际操作与之前的提取坡度工具参数上有所不同，记录一下，工具的具体原理见文末参考链接

【Topographic Features】工具，可提取出

- Peak
- Ridge
- Pass
- Plane
- Channel
- Pit

可以按需提取

## 环境

ENVI 5.3（ENVI 6.0也类似）

## 地形特征提取

在ENVI工具箱中，找到【Terrain】|【Topographic Features】，打开之后就可以选择数据，我这里选择了一幅已经投影和裁剪过的ASTER GDEM数据。有需要也可以在打开界面的【Spatial Subset】对数据进行进一步裁切

![image-20240516200547390](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904588.png)

![image-20240516200610757](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904805.png)

点击【OK】之后，直接进入到【Topo Feature Parameters】界面，【Slope Tolerance】，即坡度容差，默认为1.0（一般来说，值越大，越容易提取出Peak、Pass、Pit）；【Curvature Tolerance】，即曲率容差，默认为0.1（一般来说，值越小，越容易提取出Peak、Pass、Pit），【Topographic Kernel Size】，即卷积核大小，默认为3（一般来说，值越大生成的结果越平滑），【Select Feature to Classify】默认勾选全部特征，可以按需进行选取，之后选择输出文件路径即可，点击【OK】即可输出（输出文件为分类栅格文件）

![image-20240516202150734](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904105.png)

输出结果如下所示：

![image-20240516202531936](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904610.png)

![image-20240516202631224](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904981.png)

右键【Quick Stats】，可以看到不同类型的占比

![image-20240517211932521](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904479.png)

如果之后想要使用矢量格式的话，可以通过工具箱中的【Classification to Vector】功能，将输出的分类栅格再转为矢量格式的数据

![image-20240517205905523](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904169.png)

![image-20240517205931598](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904518.png)

点击【OK】之后，进入【Raster To Vector Parameters】界面。【Select Classes to Vectorize】中，默认不勾选，可以按需进行选取；【Output】中有两种模式，【Single Layer】为默认，即所有类型放在一个文件，【One Layer per Class】，即不同类型单独一个文件，输出结果就是在指定的文件名中加上对应类别的后缀；【Output Raster to】选择是要临时存储在【Memory】，还是保存为具体的【File】；之后选择输出文件路径即可，点击【OK】即可输出（输出文件为evf格式矢量文件）

![image-20240517210625635](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904975.png)

输出结果如下（如果选择的【Single Layer】，那么输出结果就只有一个evf文件）

![image-20240517213534857](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904675.png)

![image-20240517213600777](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904305.png)

## 补充

由于ENVI中的evf格式无法在ArcGIS中直接打开，因此如果要在ArcGIS中进行操作，那么还需将evf转为shp格式

在ENVI工具箱中，找到【Vector】|【Classic EVF to Shapfile】，打开之后就可以选择输入数据了



![image-20240517215238087](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904218.png)

进入【Output EVF Layer to Shapfile】界面，之后选择输出文件路径即可，点击【OK】即可输出（输出文件为shp格式矢量文件）

![image-20240517215502311](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270904603.png)

## 总结

在ENVI中可以直接提取这些地形特征，在ArcGIS中还是需要进行其他操作之后通过【焦点统计】才能得到数据

在提取这些地形特征的时候，由于输出的是分类栅格，因此在输出的时候最好不要直接在后面加上“.tif”，避免输出错误，可以在生成之后通过【Save as】保存为TIF格式

如果要将分类栅格转矢量，数据尽量小一点，不然可能需要很久的转换时间（裁剪过后的1000*1000大小的数据需要花费5分钟），因此可以考虑转为tif到ArcGIS里面转矢量

## 参考

[Extract Topographic Features (geoscene.cn)](https://envi.geoscene.cn/help/Subsystems/envi/Content/Topographic/ExtractingTopographicFeatures.htm)

```
https://envi.geoscene.cn/help/Subsystems/envi/Content/Topographic/ExtractingTopographicFeatures.htm
```

