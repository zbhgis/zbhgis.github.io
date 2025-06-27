# Landsat 8/9 C2L2级别数据表面反射率产品使用注意点

[TOC]

## 前言

这篇主要介绍Landsat 8/9 C2L2级别的地表反射率产品（SR）。使用Landsat 8/9 C2L2级别的产品由于不需要再自行大气校正，使用起来方便，但也存在很多需要注意的地方，也有很多坑。更详细的说明需要到官方网站查看，以下是我结合了官方说明的个人使用经验和需要格外注意的事项，如有错误和不足，欢迎指正和补充！

## 数据简介

地表反射率（SR）源自Landsat 8/9 Collection 2 Level 1 operational Land Imager (OLl)数据，在此产品中共提供了7个波段

| SR产品 | 波段类型 |
| ------ | -------- |
| SR_B1  | Coastal  |
| SR_B2  | Blue     |
| SR_B3  | Green    |
| SR_B4  | Red      |
| SR_B5  | NIR      |
| SR_B6  | SWIR 1   |
| SR_B7  | SWIR 2   |

## 常见问题

（1）该产品在全球范围内生产并且总体上表现符合预期，但是对于关注局部地区的，自行大气校正效果一般来说会更好。

（2）由于算法的问题，在明亮的雪/冰和云像素及其周围可能会反演失败，导致其值异常。

![image-20240515103811905](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270854844.png)

（3）由于问题（2）,在按照官方给出的公式进行像元值转换之后，反射率会出现>1.0或<0.0的情况。

反射率>1.0的像素几乎都在QA_PIXEL图层中被标记为云或雪/冰，用户可以通过QA_PIXEL找到这些像素。

![image-20240515180856250](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270854394.png)

有时候，Landsat 8 影像的右下角留下一条深色轨迹（伪影），导致该部分反射率值较低；同样的，在阴影水面上，气溶胶过度校正通常会导致表面反射率 <0.0。

![image-20240515104323899](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270854712.png)

（4）有时候在影像中也会出现“Nodata”像素，这是因为在用官方的算法之后，在影像中有的值会小于-0.2（-0.2是该算法计算出的地表反射率有效范围下界），因此官方统一把小于-0.2的像素归类到0.2中，再通过官方提供的公式转换之后，此类像素的值就变成0，也就是“Nodata”值。

![image-20240515104356886](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270855398.png)

（5）不同传感器的不同级别数据处理方式各不相同，不要弄混

## 注意事项

（1）该产品不包括全色波段。

（2）该产品不包括太阳天顶角大于76°的图像。

（3）该产品在高纬度地区(>65°）虽然提供部分产品，但是具有较大不确定性。（谨慎使用）

（4）来自Landsat 8/9 OLI的波段1和2，分别为海岸气溶胶和蓝色波段，其校正值不应用于分析。因为这两个波段已经在算法中用于进行气溶胶反演测试，这可能导致其不可靠。（尽量不要用该产品的这两个波段进行分析，可能有误）

（5）不要使用QA_PIXEL中标记为高气溶胶含量的像素。

（6）被LaSRC（官方的校正算法）标记为水的像素，使用了单独的程序处理。

（7）Landsat8/9 SR数据提取的不利条件包括：极度干旱或积雪覆盖的地区、低太阳角度条件、陆地面积相对于相邻水域较小的沿海地区以及存在广泛云污染的地区（即在这些地区，该产品的校正值可能有一定问题）

## 数据下载

数据可以在USGS网站进行下载

[EarthExplorer (usgs.gov)](https://earthexplorer.usgs.gov/)

```
https://earthexplorer.usgs.gov/
```



## 文件

产品（压缩包）命名格式

![image-20240515112441063](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270855049.png)

以下为产品中的数据说明（包括了SR、ST、QA)，需要注意B1到B7的像元值的转换公式

![image-20240515165952344](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270855568.png)

## 引用

使用该级别的产品可以引用以下论文

![image-20240515114907753](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270855719.png)

## 参考

[Landsat Collection 2 Known Issues | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR)

```
https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR
```

[Landsat 8-9 Collection 2 Level 2 Science Product Guide | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/media/files/landsat-8-9-collection-2-level-2-science-product-guide)

```
https://www.usgs.gov/media/files/landsat-8-9-collection-2-level-2-science-product-guide
```

