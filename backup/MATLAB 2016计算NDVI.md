# MATLAB 2016计算NDVI

之前大二的一段MATLAB代码，突然找到，记录一下当时初学MATLAB的程序，用于读取TIFF计算归一化植被指数（NDVI）并将其保存为TIFF文件。

[TOC]


## 读取波段数据

```matlab
[B4,R] = geotiffread('G:\data-2022\result_2_Red.tif');
[B5,R] = geotiffread('G:\data-2022\result_4_NIR.tif');
```

使用`geotiffread`函数分别读取两个GeoTIFF文件：`result_2_Red.tif`（红光波段，对应B4）和`result_4_NIR.tif`（近红外波段，对应B5）。每个波段数据被存储为一个二维数组（矩阵），有相同的地理参考信息`R`，包含图像的坐标系统、像素大小等空间属性。

## 初始化NDVI矩阵和转换数据类型

```matlab
NDVI = zeros(10715,13980,'single');
B4 = single(B4);
B5 = single(B5);
```

根据波段数据的维度（此处为10715行×13980列，当时提前看属性的，这里改为size函数更通用），用`zeros`函数创建一个同样大小的零矩阵`NDVI`，用于存储计算出的NDVI值，并指定数据类型为`'single'`（单精度浮点数）。接着，将读取到的波段数据`B4`和`B5`转换为单精度浮点数类型。

## 计算NDVI

```matlab
for i = 1:10715
    for j =  1:13980
        if B4(i,j) == 0 || B5(i,j) ==0
            continue;
        end
        NDVI(i,j) = (B5(i,j)-B4(i,j))/(B5(i,j)+B4(i,j));
    end
end
```

使用两层循环遍历波段数据的每一个像素位置（`i`为行索引，`j`为列索引）。在计算NDVI时，检查`B4`和`B5`是否为零，避免除以零。

## 获取参考图像信息并写入GeoTIFF文件

```matlab
info = geotiffinfo('G:\data-2022\result_2_Red.tif');
geotiffwrite('G:\data-2022\result_NDVI.tif', NDVI, R, 'GeoKeyDirectoryTag', info.GeoTIFFTags.GeoKeyDirectoryTag);
```

使用`geotiffinfo`函数读取`result_2_Red.tif`的元数据信息，并将其存储在结构体变量`info`中。然后，使用`geotiffwrite`函数将计算得到的NDVI矩阵写入新的GeoTIFF文件。

## 完整代码如下

```matlab
[B4,R] = geotiffread('G:\data-2022\result_2_Red.tif');
[B5,R] = geotiffread('G:\data-2022\result_4_NIR.tif');
NDVI = zeros(10715,13980,'single');
B4 = single(B4);
B5 = single(B5);
for i = 1:10715
    for j =  1:13980
        if B4(i,j) == 0 || B5(i,j) ==0
            continue;
        end
        NDVI(i,j) = (B5(i,j)-B4(i,j))/(B5(i,j)+B4(i,j));
    end
end
info = geotiffinfo('G:\data-2022\result_2_Red.tif');
geotiffwrite('G:\data-2022\result_NDVI.tif',NDVI,R,'GeoKeyDirectoryTag',info.GeoTIFFTags.GeoKeyDirectoryTag);

```

# 参考

[Matlab语法](https://www.cainiaojc.com/matlab/matlab-syntax.html)