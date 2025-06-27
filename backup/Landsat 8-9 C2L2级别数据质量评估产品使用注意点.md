# Landsat 8/9 C2L2级别数据质量评估产品使用注意点

[TOC]

## 汇总

整理了一份汇总文章，方便查阅
[Landsat 8/9 C2L2级别数据下载、使用、处理的个人经验以及注意事项汇总（查找用）](https://zbhgis.blog.csdn.net/article/details/139023038)

```
https://zbhgis.blog.csdn.net/article/details/139023038
```

## 前言

这篇主要介绍Landsat 8/9 C2L2级别的质量评估产品（QA）。使用Landsat 8/9 C2L2级别的产品由于不需要再自行大气校正，使用起来方便，但也存在很多需要注意的地方，也有很多坑。更详细的说明需要到官方网站查看，以下是我结合了官方说明的个人使用经验和需要格外注意的事项，如有错误和不足，欢迎指正和补充！

## 数据简介

QA标示哪个像素可能受仪器或云层等要素影响，让用户更容易地识别 “坏”像素、挑选出“好”数据、得到更准确更精确的结果。

| QA产品        | 描述                          |
| ------------- | ----------------------------- |
| QA_PIXEL      | 云置信度、云阴影和雪/冰等标志 |
| SR_QA_AEROSOL | 内部表面反射气溶胶质量评估    |
| QA_RADSAT     | 辐射测量饱和质量评估          |
| ST_QA         | ST波段的不确定性              |

## QA中的二进制与十进制

QA波段中，会涉及到二进制，二进制和十进制之间可以通过在线网站进行转换（当然也有公式可以直接算），比如十进制的21824转为二进制的101010101000000

在QA产品中，Pixel Value指的是十进制的像素值，就是例子中的21824；Bit指的是二进制的位数（从0开始），就是例子中的101010101000000每个0或者1所在的位置，从右边开始第一个为0，以此类推，位数不够在最左边直接加0补充位数，值还是不变。例子中的二进制对应关系如下

| Bit  | Value |
| ---- | ----- |
| 0    | 0     |
| 1    | 0     |
| 2    | 0     |
| 3    | 0     |
| 4    | 0     |
| 5    | 0     |
| 6    | 1     |
| 7    | 0     |
| 8    | 1     |
| 9    | 0     |
| 10   | 1     |
| 11   | 0     |
| 12   | 1     |
| 13   | 0     |
| 14   | 1     |
| 15   | 0     |

## QA_PIXEL

L2的QA_Pixel包含了来自L1的QA_Pixel的信息，这些信息在L2产品中保持不变。L2还包含了来自CFMask算法版本3.3.1的云置信度、云阴影和雪/冰标志。

QA_PIXEL不同值对应的含义（二进制位数）如下

![image-20240516233227918](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270857853.png)

QA_PIXEL不同像素值对应的含义（十进制数值）如下

![image-20240516233323727](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270857479.png)

## QA_RADSAT

传感器波段在数据捕获期间饱和，产生不可用的数据，在QA_RADSAT标记。

饱和发生在两种区域：

（1）在可反射光线的地物的光学波段上

（2）在火山和野火的短波红外(SWIR)和热波段上

饱和记录为两种形式:

（1）记录为像素值65535

（2）记录为有效值范围的下界(不一定只是一个值0)。这被称为过饱和，只发生在OLl传感器上，而不会发生在TIRS上。

Landsat 8/9 QA_RADSAT只标记饱和情况。QA_RADSAT不同值对应的含义（二进制位数）如下

![image-20240517121027885](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270857802.png)

## SR_QA_AEROSOL

SR_QA_AEROSOL用于大气校正，提供了可能影响最终产品结果的因素。

SR_QA_AEROSOL不同值对应的含义（二进制位数）如下

![image-20240517121748423](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270857686.png)

SR_QA_AEROSOL不同像素值对应的含义（十进制数值）如下（尽量避免使用被标记为High-level aerosol的像素）

![image-20240517121851143](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270858848.png)

SR_QA_AEROSOL不同像素值对应的含义（十进制数值）详细版如下

![image-20240517184413481](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270858057.png)

![image-20240517184428193](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270858823.png)

## ST_QA

包含了ST波段的不确定性

## 文件

产品（压缩包）命名格式

![image-20240515112441063](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270858767.png)

以下为产品中的数据说明（包括了SR、ST、QA)，QA产品中一般使用QA_PIXEL较多

![image-20240515165952344](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270858047.png)

## 引用

使用该级别的产品可以引用以下论文

![image-20240515114907753](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270858734.png)

## 参考

[Landsat Collection 2 Known Issues | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR)

```
https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR
```

[Landsat 8-9 Collection 2 Level 2 Science Product Guide | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/media/files/landsat-8-9-collection-2-level-2-science-product-guide)

```
https://www.usgs.gov/media/files/landsat-8-9-collection-2-level-2-science-product-guide
```

