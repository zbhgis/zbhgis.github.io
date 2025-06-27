# Conda安装rasterio报错

[TOC]



## 问题

在conda环境中安装rasterio包之后，本来可以正常运行的，但是之后又重新安装了一个gdal，导致原来的引用rasterio的包的程序不可正常运行了

```
conda install rasterio
conda install gdal
```

报错DLL load failed while importing _base，应该两个包冲突了

```
ImportError: DLL load failed while importing _base: 找不到指定的程序。
```

![image-20240507124015821](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270845381.png)

## 解决

刚开始我是直接通过conda命令重新卸载并安装了rasterio包，然后还是不可以正常运行，之后又尝试了增加环境变量等一系列操作还是不行，可能是我的操作也有问题

```
conda uninstall rasterio
```

```
conda install rasterio
```

无奈之下，直接重新创建了一个Python3.9虚拟环境，然后重新安装这两个包，然后就可以了，初步推断应该是之前的版本冲突等问题，这回我安装的版本是Rasterio1.2.10和gdal3.0.2，然后切换好解释器之后重新运行了脚本就可以了

```
conda install gdal==3.0.2
```

```
conda install rasterio==1.2.10
```

## 参考

[rasterio/rasterio: Rasterio reads and writes geospatial raster datasets (github.com)](https://github.com/rasterio/rasterio)

```
https://github.com/rasterio/rasterio
```

[Switching from GDAL’s Python bindings — rasterio documentation](https://rasterio.readthedocs.io/en/stable/topics/switch.html)

```
https://rasterio.readthedocs.io/en/stable/topics/switch.html
```

