# Arcpy入门学习笔记（二）：脚本工具

主要介绍Arcpy脚本工具制作

[TOC]

## Arcpy语法速查

1、ArcGIS工具界面的【工具帮助】

![image-20240419235458653](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328579.png)

![image-20240419235513830](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328624.png)

2、地理处理的【结果】会话窗口，右键工具提供的“【复制为Python代码片段】

![image-20240419235859687](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328279.png)

![image-20240419235944587](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328384.png)

3、ArcGIS模型【导出至Python脚本文件】

![image-20240420000844887](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328463.png)



## Arcpy脚本常用代码

会经常使用到的代码或代码块

### 包的导入

```python
# 导入sys模块，设置Python解释器的默认编码为UTF-8
import sys
reload(sys)
sys.setdefaultencoding('utf8')

# 导入ArcPy模块
import arcpy

# 导入NumPy库
import numpy as np

# 导入Python标准库中的os模块，用于操作文件路径
import os

# 导入datetime类，用于处理日期和时间
from datetime import datetime

# 从ArcPy空间分析模块导入所有函数和类
from arcpy.sa import *

# 导入xlwt模块，用于创建和操作Excel文件（xls格式）
import xlwt
```

### 获取工具箱参数

```python
# 获取参数
layer = arcpy.GetParameter(0)

# 获取参数并读取为Unicode
out_path = arcpy.GetParameterAsText(1)

# 获取参数并转为整数
num = int(arcpy.GetParameterAsText(2)) 

# 获取参数并转为字符串
out_path = str(arcpy.GetParameterAsText(3)) 

# 在参数获取方法相同时，可批量获取
args = tuple(arcpy.GetParameterAsText(i) for i in range(arcpy.GetArgumentCount()))
Test(*args)
```

### 环境设置

```python
#!/usr/bin/env python
# coding=utf-8

# 确认分析模块是否可用
arcpy.CheckOutExtension("spatial")

# 设置工作空间
arcpy.env.workspace = out_path

# 设置并行处理因子为0，因为有的学习版用不了这个功能
arcpy.env.parallelProcessingFactor = '0'

# 设置输出可覆盖文件
arcpy.env.overwriteOutput = "True"
```

### 工具箱输出

```python
# 在工具箱输出栏中打印信息
arcpy.AddMessage("ok")
```

## 脚本工具制作

本部分较为繁琐，可粗略看看

### 准备好py文件

比如下面这个，先在Pycharm中进行测试，可以根据指定数量生成圆的个数，每个圆的半径依次增加50m

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-21 11:41

import sys
reload(sys)
sys.setdefaultencoding('utf8')
import arcpy
import os
import math

def create_shapefiles(num, out_path):
    # 设置坐标系为WGS84_UTM_50N
    spatial_reference = arcpy.SpatialReference(32650)  # WGS84_UTM_50N的WKID为32650

    # 根据num循环创建矢量文件
    for i in range(1, num + 1):
        # 创建要素类名称和路径
        circle_name = "Circle_{}m".format(i * 50)
        circle_path = os.path.join(out_path, circle_name + ".shp")

        # 创建圆
        arcpy.management.CreateFeatureclass(os.path.dirname(circle_path), circle_name, "POLYGON", spatial_reference=spatial_reference)
        circle_cursor = arcpy.da.InsertCursor(circle_path, ["SHAPE@"])
        circle = arcpy.Point()
        circle_geometry = arcpy.Array()
        for angle in range(0, 361, 10):
            circle.X = 50 * i * math.cos(math.radians(angle))  # 半径为50*i
            circle.Y = 50 * i * math.sin(math.radians(angle))
            circle_geometry.add(circle)
        circle_geometry.add(circle_geometry.getObject(0))  # 添加起始点以闭合圆
        circle_cursor.insertRow([arcpy.Polygon(circle_geometry)])
        del circle_cursor

if __name__ == "__main__":
    num = 2
    out_path = r'G:\MyTestProject\arcpy2_test\data'

    arcpy.CheckOutExtension("spatial")
    arcpy.env.parallelProcessingFactor = '0'
    arcpy.env.overwriteOutput = "True"
    arcpy.env.workspace = out_path

    create_shapefiles(num, out_path)

    arcpy.AddMessage(num)
    arcpy.AddMessage(out_path)
```

在Pycharm中运行结果打开如下：

![image-20240421130358309](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328633.png)

测试没问题之后，将最后一段改掉，从面板获取参数，并将代码中的中文注释都删掉或者改成英文注释，不然会有一些离谱的bug，修改后准备的导入脚本的代码如下：

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-21 11:41

import sys
reload(sys)
sys.setdefaultencoding('utf8')
import arcpy
import os
import math

def create_shapefiles(num, out_path):
    spatial_reference = arcpy.SpatialReference(32650)  # WGS84_UTM_50N的WKID为32650

    for i in range(1, num + 1):
        circle_name = "Circle_{}m".format(i * 50)
        circle_path = os.path.join(out_path, circle_name + ".shp")

        arcpy.management.CreateFeatureclass(os.path.dirname(circle_path), circle_name, "POLYGON", spatial_reference=spatial_reference)
        circle_cursor = arcpy.da.InsertCursor(circle_path, ["SHAPE@"])
        circle = arcpy.Point()
        circle_geometry = arcpy.Array()
        for angle in range(0, 361, 10):
            circle.X = 50 * i * math.cos(math.radians(angle))
            circle.Y = 50 * i * math.sin(math.radians(angle))
            circle_geometry.add(circle)
        circle_geometry.add(circle_geometry.getObject(0))
        circle_cursor.insertRow([arcpy.Polygon(circle_geometry)])
        del circle_cursor

if __name__ == "__main__":
    # num = 2
    # out_path = r'G:\MyTestProject\arcpy2_test\data'
    num = int(arcpy.GetParameterAsText(0))
    out_path = str(arcpy.GetParameterAsText(1))

    arcpy.CheckOutExtension("spatial")
    arcpy.env.parallelProcessingFactor = '0'
    arcpy.env.overwriteOutput = "True"
    arcpy.env.workspace = out_path

    create_shapefiles(num, out_path)

    arcpy.AddMessage(num)
    arcpy.AddMessage(out_path)
```



### 创建工具

创建好一个工具箱后，在其中创建工具集，并在工具集中添加脚本

![image-20240421130946332](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328627.png)



修改名称和标签，存储为相对路径（对应的地图文档属性最好也提前设置为相对路径，在【文件】【地图文档属性】【路径名】处进行勾选）

![image-20240421131053202](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328631.png)

导入脚本文件所在位置

![image-20240421131411366](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328222.png)

设置参数，一个为“圆的数量”，对应数据类型为长整型；一个为输出文件夹，对应数据类型为文件夹

![image-20240421131900538](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328706.png)

右键打开工具

![image-20240421132218453](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328281.png)

初步使用可行

![image-20240422001014508](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262328952.png)

### 脚本工具各功能详解

脚本右键功能

![image-20240421133114511](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262329285.png)

【属性】中的【常规】

![image-20240421133327100](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262329403.png)

【属性】中的【源】

![image-20240421133508006](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262329400.png)

【属性】中的【参数】

![image-20240421134022597](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262329001.png)

【属性】中的【验证】

![image-20240421134315206](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262329159.png)

### 修改默认编辑和调试

在ArcGIS菜单栏中【地理处理选项】中，将【编辑器】和【调试程序】换做pycharm所在位置，之后即可在脚本右键【编辑】快速在pycharm中打开对应文件（这个根据个人需要设置）

```
D:\py\Pycharm\bin\pycharm64.exe
```

![image-20240421115026617](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262329660.png)



## 总结

脚本工具先自己有个数就行，而且在Pycharm中可以正常运行的工具转为脚本工具可能会有一些奇奇怪怪的错误，最好学一些Arcpy基础之后再用，边学边用就懂了；

其次就是在脚本工具中，尽量不要使用中文，包括注释
<!-- ##{"timestamp":1713736800}## -->