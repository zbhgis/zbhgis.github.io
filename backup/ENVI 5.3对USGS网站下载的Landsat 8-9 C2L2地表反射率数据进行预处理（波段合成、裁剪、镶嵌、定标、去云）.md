# ENVI 5.3对USGS网站下载的Landsat 8/9 C2L2地表反射率数据进行预处理（波段合成、裁剪、镶嵌、定标、去云）

@[toc]
## 前言（必读）

不同的下载方式以及不同级别的数据产品在ENVI的不同版本中有不同的处理方式，以本文为例，演示在USGS网站下载Landsat 8/9 C2L2级别的地表反射率（SR）产品在ENVI 5.3版本中的预处理流程

！！！建议所有数据在进行以下操作之前进行备份，避免操作失误等问题需要去网站上重新下载数据！！！

在进行预处理之前，最好对这个级别的数据有一定的了解。

[Landsat 8/9 C2L2级别数据下载、使用、处理的个人经验以及注意事项汇总（查找用）_landsat8l2sp数据怎么处理可用-CSDN博客](https://blog.csdn.net/zbh13859825167/article/details/139023038)

```
https://blog.csdn.net/zbh13859825167/article/details/139023038
```



## 软件准备

本次使用的软件是：ENVI 5.3，需提前安装好（其他版本软件处理流程类似），ENVI高版本支持的批处理工具更多会方便一些。



## 目标

现有在USGS网站上下载好的某个区域的Landsat8/9 C2L2级别的地表反射率数据产品若干幅，在ENVI 5.3中进行预处理，选择蓝、绿、红、近红外4个波段，得到研究区范围的波段合成好的TIF格式数据。



## 数据下载

详细步骤见以下文章：

[USGS网站下载Landsat 5/7/8/9数据最新详细教程（注册、筛选、单波段、批量下载等），附常见问题_usgs注册账号-CSDN博客](https://blog.csdn.net/zbh13859825167/article/details/139173382)

```
https://blog.csdn.net/zbh13859825167/article/details/139173382
```

影像ID：

```python
LC09_L2SP_118042_20220915_20230329_02_T1
LC09_L2SP_119042_20220821_20230402_02_T1
```



## 数据处理

数据下载好之后就可以直接开始处理了。

由于ENVI 5.3并不支持直接识别Landsat 8/9的C2L2级别的数据产品，因此本文介绍两种方法来打开数据并在ENVI中进行预处理。



### 打开数据

**方法一（通过Metadata打开，打开后进行波段裁剪并导出dat格式）：**

通过Metadata打开数据的方法见以下文章：

[ENVI 5.3/6.0打开Landsat 8/9 C2L2级别数据（带有Metadata），附常见问题_envi打开landsat8-CSDN博客](https://blog.csdn.net/zbh13859825167/article/details/139309431)

以其中的一幅影像为例，将其Metadata文件修改好后，通过【File】|【Open】打开如下所示：

![image-20250101115858725](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018188.png)

在菜单栏中选择【File】|【Save As】|【Save As ...】，选择【Spectral Subset】![image-20250101120302432](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018014.png)

![image-20250101130416309](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018509.png)

按住Ctrl键后选择需要的波段，本文选择其中的蓝、绿、红、近红四个波段进行导出，点击【OK】

![image-20250101132658053](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018725.png)

导出格式选择【ENVI】，文件命名为”L9_119042_220821.dat“

![image-20250101145139884](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018726.png)

![image-20250101145733571](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018573.png)

其他影像同理。打开之后进行图像裁剪。



**方法二（直接打开tif文件，打开后进行波段合成）：**

以普通的TIF格式文件打开，则需要自行完成波段合成：

以其中的一幅影像为例，将下载完成的蓝、绿、红、近红外这4个波段拷贝在一个文件夹中，在ENVI中通过【File】|【Open】打开下载的4个波段文件。（如果需要其他操作，比如计算一些指数的话，就选择一并选择其他的波段）

![image-20240923171742219](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018925.png)

![image-20240923175415606](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018193.png)

之后对这些导入的波段进行波段合成，方便后续操作。在右侧工具箱中的【Raster Management】|【Layer Stacking】中，选择刚刚导入的波段，然后选择输出路径，文件命名为”L9_119042_220915.dat“，点击【OK】。

![image-20250101145309239](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018671.png)

![image-20250101145452269](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271018704.png)

其他影像同理。打开之后进行图像裁剪。



### 图像裁剪

为了减少后续镶嵌花费的时间，以及减少地物降低色差，就先进行图像裁剪。

这里需要使用一个官方提供的插件，插件需要在APP Store中下载，或者手动安装。

[ENVI扩展工具：栅格图像批处理工具包（适用于低版本） - ENVI-IDL技术殿堂 - 博客园 (cnblogs.com)](https://www.cnblogs.com/enviidl/p/16334286.html)

```
https://www.cnblogs.com/enviidl/p/16334286.html
```

安装好之后，重启ENVI软件。首先通过【File】|【Open】在ENVI中打开矢量边界数据。其中，两幅影像分别为50度带和51度带的坐标系，矢量数据为50度带的坐标系。

![image-20241017095315982](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019086.png)

在右侧工具箱中的【Extension】|【Raster Processing Batch Tool】中找到【Subset Data from Shapefile Batch】，选择波段合成后的影像，【Input Vector】选择准备好的矢量文件，并选择后缀名和输出路径。点击【OK】。

![image-20250101151026904](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019002.png)

通过这个方式裁剪之后的输出结果还是各自保持为原来的投影坐标系，结果如下所示。

![image-20241017095022302](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019201.png)

### 图像镶嵌

在右侧工具箱中的【Mosaicking】|【Seamless Mosaic】，点击如图所示的“+”，通过【Open File】打开波段合成之后的两幅影像。并勾选右上角的【Show Preview】，能够实时预览。

![image-20240924085226327](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019583.png)

![image-20240924093755207](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019737.png)

![image-20240924085520648](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019907.png)

在【Main】配置中，将【Ignore Value】改为0，【Color Matching Action】选择“L9_119042_220821_subset.dat”为【Reference】，即基准影像，其他的为【Adjust】，即待校正影像。

![image-20250101151252580](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019258.png)



在【Color Correction】配置中，勾选【Histogram Matching】，并选择【Overlap Area Only】，

![image-20240924090954806](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019648.png)

在【Seamlines】选项中，选择【Auto Generate Seamlines】。

![image-20240924091112191](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019137.png)

在【Seamlines/Feathering】中，保持默认选择。

![image-20240924091342828](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019078.png)

在【Export】中，选择输出格式为【ENVI】，并选择输出路径，将【Output Background Value】设置为0，其余保持默认选择。

![image-20250101151521817](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019917.png)

点击下方的【Finish】，等待时间之后即可完成镶嵌。

![image-20241017101057895](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019526.png)







### 定标/像元值转换

这一步即将波段从DN值定标为反射率，这里需要使用一个官方提供的插件，插件需要在APP Store中下载，或者手动安装。

[ENVI扩展工具：栅格图像批处理工具包（适用于低版本） - ENVI-IDL技术殿堂 - 博客园 (cnblogs.com)](https://www.cnblogs.com/enviidl/p/16334286.html)

```
https://www.cnblogs.com/enviidl/p/16334286.html
```

安装好之后，重启ENVI软件。在右侧工具箱中的【Extension】|【Raster Processing Batch Tool】中找到【Band Math Batch】，选择裁剪后的影像，【Variable Type】选择【File】，【Expression】填入以下表达式，并选择输出路径。点击【OK】。

该表达式的含义是将设置影像的背景值为-1（建议设置为整数），非背景值设置按照公式进行转换为反射率，其中大于1的部分设置为1，小于0的部分设置为0。

```python
((b1 ne 0)*(b1*0.0000275-0.2))>0<1+(b1 eq 0)*(-1)
```

![image-20241018104521339](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019173.png)



![image-20241017145509802](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019578.png)

再进一步右键图层，选择【View Metadata】中的【Edit Metadata】

![image-20250101152737289](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019134.png)

点击左上角的【Add...】，找到【Data Ignore Value】，点击【OK】进行添加，并将其设置为“-1”。

![image-20250101153031643](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019809.png)

![image-20250101153142993](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019156.png)

![image-20250101161031879](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271019762.png)

### 去云

自己去手动查看并下载的影像云占比都很少，一般情况下不需要去云，可以跳过此步。

如果有特殊需要去云的话，则需要自行创建掩膜，将云层部分设置为Nodata，不参与后续运算。

这个部分的实现可以通过QA_PIXEL波段、观察确定经验阈值、云检测指数、云检测算法等多种方式。

右键图层，选择【New Raster Color Slice】，选择其中的蓝波段之后，创建密度分割波段。

先点击【Clear Color Slices】，将所有的分割层级删除，再点击【Add Color Slice】添加新的颜色分割，自行设置阈值。如下图，虽然官方有对应的QA_PIXEL质量评估波段，但是其在某些方面标记的不太准确，比较适合在宏观尺度上使用。例如下图中红色的部分为QA_PIXEL波段中的22280，为高置信度云，但是实际上为城区和水体。如果研究关注的是山区植被，进行计算NDVI等，那就没太大的影响；如果研究关注的是城区建筑，计算NDBI等，那就容易错误掩膜掉所需的信息。

![image-20241017112041848](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020052.png)

由于QA_PIXEL波段在本区域效果不好，并且本文只是实验，故采用较为方便的通过观察确定经验阈值的方式（这种方式的缺点就是不同区域的阈值不一定相同）。云层和白色建筑物较难区分，因此主要观察两者在各个波段反射率的差异。通过菜单栏中的【Cursor Value】，以此查看云层的反射率（主要观察云层与周围地物交界的反射率）。通过观察（前者为云，后者为地物），推断出云层的红绿蓝波段反射率都要略微低于白色建筑物。

![image-20241017151854830](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020013.png)

![image-20241017152028031](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020597.png)

右键图层，选择【New Raster Color Slice】，选择其中的蓝波段之后，创建密度分割波段。

先点击【Clear Color Slices】，将所有的分割层级删除，再点击【Add Color Slice】添加新的颜色分割，自行设置阈值。经过不断调整，确定阈值为0.25，大于0.25为云层，小于0.25为其他地物，基本上可以区分云层和白色建筑物。因此，将新的颜色分割设置为最小值至0.25，即创建一个不包括云层的密度分割图层。

![image-20241017154159305](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020873.png)


![image-20241017154637823](https://i-blog.csdnimg.cn/img_convert/1d7b393d008aace53c55176dc510f26d.png)

![image-20250101153341637](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020560.png)

选中“Slice”，右键选择【Export Color Slices】|【Shapefile】，并选择输出路径，点击【OK】。

![image-20241017162534234](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020920.png)

![image-20250101153641290](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020352.png)

在右侧工具箱中的【Raster Management】|【Masking】|【Build Mask】，选择转换像元值后的影像，在【Options】中选择【Import EVFs】，选择准备好的云层矢量，点击【OK】，在弹出的面板中，再次选择转换像元值后的影像，点击【OK】。

![image-20241017160406006](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020843.png)

![image-20241017160443942](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020016.png)

![image-20241017160558616](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020379.png)

![image-20250101155022072](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020082.png)

此时返回最初的界面，选择好输出文件的路径之后，再点击【OK】即可。创建的掩膜如下所示，掩膜中云层部分对应的值为0。

![image-20250101154951310](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020949.png)

![image-20250101160228824](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020730.png)

在右侧工具箱中的【Raster Management】|【Masking】|【Apply Mask】，在主面板中选择之前转换像元值之后的影像，然后在下方的【Select Mask Band】中，选择刚刚生成的掩膜栅格，点击【OK】。在之后面板中选择需要掩膜的值，设置为“-1”，即上一步中的波段计算设置的背景值，再文件输出路径，再次点击【OK】。

![image-20250101155337276](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020700.png)

![image-20250101155724150](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020810.png)

可以看到，掩膜之后的影像中云层部分的各个波段值均为nodata。

![image-20250101155808505](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020647.png)

### 导出为TIF

通过菜单栏中的【File】|【Save As】，将这个数据导出为TIFF格式。

![image-20250101160326479](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271020563.png)



## 注意点（必读）

1、在ENVI 5.3中处理这个级别的数据，一定要对数据进行检查，因此有的时候软件可能读取不到数据的空间参考信息，这个时候如果进行操作会导致后面的操作失败，因此如果软件没有读取到坐标系的空间参考信息的话，就需要自己先进行投影。

可以右键【View MetaData】，如果在【Map Info】中可以看到每个波段的【Type】为“Arbitrary”说明未进行投影，之后还得自行通过ENVI工具箱中的【Reproject Raster】进行投影；如果【Type】为“Projected”就说明已经投影过了或者成功读取到空间参考信息了。

![image-20240514222419810](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271021200.png)

2、Landsat8 C2L2级别的数据官方为了方便存储，通过整型数据存储，但是并不是像Collection1直接放大一万倍，需要按照特定的公式进行处理。

3、Landsat8 C2L2级别的数据在预处理的过程做过大气校正了，但是这个大气校正的结果可能会在部分指数计算的时候导致奇怪的值，就是这个也可以用，但是与C2L1级别的产品结合ENVI的FLAASH大气校正出来的结果肯定是有一定差别的，有时间的话可以下载C2L1级别的数据进行大气校正。

4、如果操作过程中，涉及到了影像的坐标系转换，建议使用ENVI的【Reproject Raster】工具进行重投影；通过【Edit  Metadata】直接修改影像的坐标系可能会导致影像的偏移。

5、原始数据最好备份一份，避免操作失误。

6、每一个步骤处理完后建议查看一下影像的处理结果是否符合预期，如果与预期相差较大，那么就可能是参数设置错误。

7、如果处理过程中发现某个盘爆满或者空间变小很多，可以在以下区域进行更改。在菜单栏【File】中选择【Preference】，找到【Temporary Directory】，对该路径进行修改，切换到其他路径，之后重启软件或电脑；或者也可以对这个路径的缓存文件进行删除即可。

![image-20240923174915951](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506271021313.png)



## 参考

[envi.geoscene.cn - /help/Subsystems/envi/Content/](https://envi.geoscene.cn/help/Subsystems/envi/Content/)

```
https://envi.geoscene.cn/help/Subsystems/envi/Content/
```
