# Landsat 8/9 C2L2级别数据地表温度产品使用注意点

[TOC]

## 汇总

整理了一份汇总文章，方便查阅
[Landsat 8/9 C2L2级别数据下载、使用、处理的个人经验以及注意事项汇总（查找用）](https://zbhgis.blog.csdn.net/article/details/139023038)

```
https://zbhgis.blog.csdn.net/article/details/139023038
```

## 前言

这篇主要介绍Landsat 8/9 C2L2级别的地表温度产品（ST）。使用Landsat 8/9 C2L2级别的产品由于不需要再自行大气校正，使用起来方便，但也存在很多需要注意的地方，也有很多坑。更详细的说明需要到官方网站查看，以下是我结合了官方说明的个人使用经验和需要格外注意的事项，如有错误和不足，欢迎指正和补充！

## 数据简介

地表温度 （ST） 产品由多个输入数据源和大气剖面生成，其中包括 NASA 的高级星载热发射和反射辐射计 （ASTER） 全球发射率数据集 （GED）

| ST产品   | 描述                                                       |
| -------- | ---------------------------------------------------------- |
| ST       | 包含地表温度，单位为开尔文。                               |
| ST_TRADE | 包含转换为热表面辐射的L1热波段。                           |
| ST_URAD  | 包含上升流热辐射。                                         |
| ST_DRAD  | 包含下升流热辐射。                                         |
| ST_ATRAN | 包含大气透射率。                                           |
| ST_EMIS  | 包含计算的表面发射率。                                     |
| ST_EMS   | 包含计算的表面发射率的期望标准偏差。                       |
| ST_CDIST | 包含像素与最近被QA_PIXEL带标记的云之间的距离，单位为千米。 |

## 常见问题

（1）该产品的部分地区没有数据，这是因为用于生成该数据的ASTER GED数据存在缺失，详见注意事项

（2）该产品中存在块状伪影。这是因为ASTER GED产品最邻近插值到Landsat数据格网中，以及ASTER NDVI 和 Landsat 数据存在几何错误配准的位置这两个问题。

（3）该产品中裸地和植被混合的地方有时会存在异常。因为混合像元是利用像元的裸地土壤和植被组分之间的线性关系来计算的，其中裸地土壤组分使用ASTER GEDv3发射率和平均NDVI产品估算，并根据Landsat观测时的植被状况进行调整。其中ASTER NDVI < 0.5的位置会被设置为裸土的发射率。

以下这些图像显示（左）Landsat 9 L1 TOA 反射率的真彩色 RGB 合成，以及（右）相应的L2 SR Band 10。地表温度块状伪影在中心枢轴灌溉田的边缘可见（示例由红色框突出显示）。由于植被调整不正确，一些灌溉田地的地表温度与其真实情况有差（绿色框突出显示的示例）。

![image-20240517000210918](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270856650.png)

## 注意事项

（1）因为用于生成该数据的ASTER GED数据存在缺失，部分地区没有ST数据

![image-20240517003105984](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270856440.png)

（2）夜间采集不能处理地表温度

## 数据下载

数据可以在USGS网站进行下载

[EarthExplorer (usgs.gov)](https://earthexplorer.usgs.gov/)

```
https://earthexplorer.usgs.gov/
```

## 文件

产品（压缩包）命名格式

![image-20240517004320168](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270856352.png)

以下为产品中的数据说明（包括了SR、ST、QA)，地表温度用的最多的是B10，需要注意B10的转换公式及单位，需要注意B10的转换公式及单位，按照官方公式给出的是开尔文单位，如果需要摄氏度单位需要自己再转换

![image-20240515165952344](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270856793.png)

## 引用

使用该级别的产品可以引用以下论文

![image-20240515114907753](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270856948.png)

## 参考

[Landsat Collection 2 Known Issues | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR)

```
https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR
```

[Landsat 8-9 Collection 2 Level 2 Science Product Guide | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/media/files/landsat-8-9-collection-2-level-2-science-product-guide)

```
https://www.usgs.gov/media/files/landsat-8-9-collection-2-level-2-science-product-guide
```

