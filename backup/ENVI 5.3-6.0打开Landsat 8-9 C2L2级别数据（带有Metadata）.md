# ENVI 5.3/6.0打开Landsat 8/9 C2L2级别数据（带有Metadata）

@[toc]
## 前言

这篇文章主要介绍在ENVI不同版本如何通过Metadata打开Landsat 8/9 C2L2级别的数据。由于涉及到数据的修改，因此在开始操作前，记得先备份数据，以防万一。

在这里先放一张USGS网站提供的波段介绍，对后续的检查数据等比较有帮助。Landsat 8/9 C2L2产品还有很多使用注意点，详细可以见官网或者看我之前的文章。下载方式我在之前的文章也有介绍。

[Landsat 8/9 C2L2级别数据下载、使用、处理的个人经验以及注意事项汇总（查找用）-CSDN博客](https://zbhgis.blog.csdn.net/article/details/139023038)

```
https://zbhgis.blog.csdn.net/article/details/139023038
```
根据本文打开数据之后就可以进行预处理了，预处理的具体步骤见这篇文章
[ENVI 5.3对USGS网站下载的Landsat 8/9 C2L2地表反射率数据进行预处理（波段合成、裁剪、镶嵌、定标、去云）](https://zbhgis.blog.csdn.net/article/details/145453793)
```
https://zbhgis.blog.csdn.net/article/details/145453793
```

![image-20240530001438327](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270921842.png)

## 数据下载

USGS网站上具体的数据下载过程我之前已经介绍过了，就不再重复讲。这次我用的是Landsat 8和Landsat 9的C2L2级别数据产品，下载的一整个压缩包，具体的产品ID如下。

```
LC08_L2SP_119042_20220712_20220722_02_T1
LC09_L2SP_119038_20220720_20230406_02_T1
```

## ENVI 5.3打开Landsat 8 C2L2级别数据

1、打开ENVI 5.3之后，点击【File】|【Open As】，先尝试直接打开Metadata数据，找到LC08_L2SP_119042_20220712_20220722_02_T1_MTL.txt

然后打开，会发现报错显示无法识别

![image-20240529225808545](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270921785.png)

![image-20240529225946013](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922156.png)

2、这个时候，就需要修改文件内容。找到文件中的第一行

```
GROUP = LANDSAT_METADATA_FILE
```

将这行改为

```
GROUP = L1_METADATA_FILE
```

修改后如下，然后保存。

![image-20240529230226666](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922745.png)

3、接着Ctrl+F，找到LEVEL1相关的内容

```
LEVEL1
```

![image-20240529231032818](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922956.png)

![image-20240529231148826](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922484.png)

把LEVEL1之间的文本都删除，在这个产品中就是183行到354行及其之间的文本都删除

![image-20240529231236727](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922107.png)

删除后如下，然后保存。

![image-20240529231427613](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922859.png)

4、接着在ENVI 5.3中像第一步一样打开Landsat 8的Metadata数据，打开结果如下所示。说明多光谱数据，即地表反射率产品已经导入

![image-20240529231731368](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922129.png)

5、检查数据。右键图层选择【View Metadata】，检查信息是否导入成功。

![image-20240529231825480](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922546.png)

依次选择以下的信息大致看一遍过去，我这边传感器类型、投影、波谱信息等都导入没问题。

![image-20240529231947851](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922979.png)

也可以选择右下角的【Edit Metadata】，查看更多信息。比如云量，忽略值等等。

![image-20240529232532935](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922034.png)

6、查看像元值范围。右键图层，选择【Quic Stats】

![image-20240529232700924](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922238.png)

点击【Select Plot】的【All Histograms】，结果如下，可以看到像元值并没有自动自行转换，需要自行按照官方的公式进行像元值转换，之后再抽空单独写一篇讲预处理。

![image-20240529233059648](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922924.png)

![image-20240529233040978](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922559.png)



## ENVI 5.3打开Landsat 9 C2L2级别数据

1、对应Metadata文件的修改如Landsat 8所示，就不再演示。先试着能不能打开，我这边是打不开，会报错。（如果这个时候可以打开，就万事大吉）

![image-20240529233814599](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922195.png)

2、不能打开的话，在上述Landsat8修改的基础上，继续修改。Ctrl+F，找到Landsat_9，

```
LANDSAT_9
```

修改为Landsat_8

```
LANDSAT_8
```

![image-20240529235556630](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922664.png)

修改后如下所示，然后保存。

![image-20240529235745232](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270922286.png)

3、在ENVI 5.3中通过如下方法，重新打开

![image-20240529225808545](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923288.png)

结果如下

![image-20240530000145712](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923749.png)

4、检查数据。检查数据的步骤和类型一样，我这检查之后，发现也是像元值没有按照公式进行转换，在后续处理需要注意。

![image-20240530010552369](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923368.png)

## ENVI 6.0打开Landsat 8/9 C2L2级别数据

1、ENVI 6.0现在大家可以免费用到的就是试用版，已经支持直接打开Landsat 8/9的C2L2级别数据。我之前的文章有详细介绍ENVI 6.0试用版的安装。

[ENVI6.0试用版（180天）详细安装教程，附安装包链接和一些常见问题-CSDN博客](https://zbhgis.blog.csdn.net/article/details/139159672)

```
https://zbhgis.blog.csdn.net/article/details/139159672
```

至于网络上流传的ENVI 5.6学习版，貌似因为IDL功能不完全，很多功能使用不了，所以就没有测试。我之前的文章也有提及。

[ENVI不同版本个人使用对比-CSDN博客](https://zbhgis.blog.csdn.net/article/details/138293186)

```
https://zbhgis.blog.csdn.net/article/details/138293186
```

2、打开数据。在ENVI 6.0中可以直接通过【File】|【Open】打开Landsat 8的C2L2级别的MTL.txt数据（Landsat 9同理，这里的数据使用的没有修改的Landsat 8/9 C2L2级别数据的Metadata）。打开结果如下，包括了地表反射率、地表温度、质量评估三种产品。默认显示地表反射率产品。

![image-20240530011127276](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923561.png)

3、检查数据。右键图层选择【View Metadata】，检查信息是否导入成功。我这发现坐标系并未导入，显示为“Arbitrary”。（如果显示为“Project”，说明导入成功，可以继续检查其他部分）

![image-20240530011419324](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923598.png)

4、添加空间参考方法一。点击右下角的【Edit Metadata】，在【Spatial】切换参考类型为【Coordinate System】。

![image-20240530011750166](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923066.png)

点击浏览按钮，以如下关键词搜索，找到对应区域的坐标系之后，点击【OK】

```
WGS 1984 UTM
```

![image-20240530012236044](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923377.png)

![image-20240530012521861](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923564.png)

![image-20240530012718213](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923812.png)

如果报错如下，尝试方法二。

![image-20240530013215299](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923399.png)

添加空间参考方法二。在APP Store中下载好【Reproject Raster Batch】插件后，重启ENVI。

APP Store或者一些可获取拓展的渠道可以参考这篇文章。

[ENVI拓展工具资源去哪里找-CSDN博客](https://zbhgis.blog.csdn.net/article/details/138582220)

```
https://zbhgis.blog.csdn.net/article/details/138582220
```

![image-20240530013419729](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923296.png)

打开插件，选择好输入栅格和输出坐标系、输出目录后，其余保持默认，点击【OK】

![image-20240530013901669](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923352.png)

花费1分钟左右，之后默认输出灰度图像，可以自行在管理器中选择加载真彩色图像。

![image-20240530015210419](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923178.png)

5、再次检查数据，可以看到已经投影成功，显示“Projected”。（如果发现其他错误，也可以自行修正）

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270923230.png)


通过右键图层，选择【Quick Stats】，可以看到像元值已经经过初步转换，后续根据需要选择是否处理【Valid Range】之外的值。

![image-20240530015636601](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270924297.png)



## 总结（注意点与问题）

1、在ENVI 5.3打开Landsat 8/9的C2L2级别数据（带有Metadata）的时候，像元值没有转换，使用前需要做好预处理；而在ENVI 6.0打开Landsat 8/9的C2L2级别数据（带有Metadata）的时候，像元值虽然已经转换，但是还有Valid Range之外的值没有处理，这个根据需要选择是否处理。

2、在ENVI 5.3打开Landsat 8/9的C2L2级别数据（带有Metadata）的时候，ENVI 5.3仅仅只会识别并读取地表反射率数据产品（SR），对于地表温度（ST）和质量评估（QA）产品通过Metadata无法读取；而在ENVI 6.0打开Landsat 8/9的C2L2级别数据（带有Metadata）的时候，打开的数据包括了上述三种产品。

3、在ENVI 5.3打开数据时，需要修改Metadata，其中Landsat 8需要修改两处，Landsat 9需要修改三处。

4、在ENVI 5.3计算【Quick Stats】有时候会卡住，多试几次或者重启ENVI。如果还是卡住，在电脑的以下路径中，找到preferences5_3，把其中的文件都删除后，再尝试重启并计算。

```
C:\Users\你的用户名\.idl\envi\preferences5_3
```

![image-20240530010426994](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270924156.png)

![image-20240530010504149](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270924628.png)

5、在ENVI 6.0打开Landsat 8/9的C2L2级别数据（带有Metadata）的时候，有时候会缺失投影信息，对后续的处理可能会有影响，建议自行加上空间参考信息。

6、这篇仅仅是针对Landsat 8/9 C2L2级别数据的实验，其他卫星或级别的数据可能有所不同。

## 参考

[What are the band designations for the Landsat satellites? | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/faqs/what-are-band-designations-landsat-satellites)

```
https://www.usgs.gov/faqs/what-are-band-designations-landsat-satellites
```
