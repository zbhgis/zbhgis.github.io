# Conda中Richdem包遇到问题

[TOC]



## 问题一

### 报错

RichDEM 是一套数字高程模型 （DEM） 水文分析工具，这次打算用richdem进行地形分析，尝试在conda里面安装richdem包的时候，直接使用conda install richdem命令安装包，显示找不到该包

报错PackagesNotFoundError

### 解决

目前国内的资料较少，去github官网上看了官方文档，按照下面的命令即可解决

```
conda install richdem -c conda-forge
```

## 问题二

### 报错

在使用Richdem包的时候，太心急了没看文档，看着某个教程的示例直接使用了rasterio包读取后进行dem分析，然后报错如下

```
Exception: A richdem.rdarray or numpy.ndarray is required!
```

![image-20240506232248160](https://gitee.com/zbhgis/pic/raw/master/blog/image-20240506232248160.png)

### 解决

在分析之前，通过内部的函数读取为rdarray类型，然后再进行分析即可

```
dem = rd.rdarray(dem_data, no_data=-9999)
slope_data = rd.TerrainAttribute(dem, attrib='slope_riserun')
```

## 参考

[R-Barnes/Richdem：高性能地形和水文分析 (github.com)](https://github.com/r-barnes/richdem)

```
https://github.com/r-barnes/richdem
```

[Loading Data — RichDEM 0.0.03 documentation](https://richdem.readthedocs.io/en/latest/loading_data.html)

```
https://richdem.readthedocs.io/en/latest/loading_data.html
```

