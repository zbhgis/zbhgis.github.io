# Arcpy入门学习笔记（三）：数据属性的获取

[TOC]

官方说明：

**Describe** 函数返回的 Describe 对象包含多个属性，如数据类型、字段、索引以及许多其他属性。该对象的属性是动态的，这意味着根据所描述的数据类型，会有不同的描述属性可供使用。

Describe 属性被组织成一系列属性组。任何特定数据集都将获取其中至少一个组的属性。例如，如果要描述一个地理数据库要素类，您可访问 [GDB 要素类](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/gdb-featureclass-properties.htm)、[要素类](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/featureclass-properties.htm)、[表](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/table-properties.htm)和[数据集](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/dataset-properties.htm)属性组中的属性。所有数据，不管是哪种数据类型，总会获取通用 [Describe 对象](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe-object-properties.htm)属性。

## 常用的属性

### Describe对象属性（部分）

| 属性                     | 说明                 | 数据类型                                                     |
| ------------------------ | -------------------- | ------------------------------------------------------------ |
| baseName（只读）         | 文件基本名称         | String                                                       |
| catalogPath（只读）      | 数据路径             | String                                                       |
| children（只读）         | 子元素列表           | [Describe](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe.htm) |
| childrenExpanded（只读） | 指示子元素是否已扩展 | Boolean                                                      |
| dataElementType（只读）  | 元素的元素类型       | String                                                       |
| dataType（只读）         | 元素类型             | String                                                       |
| extension（只读）        | 文件扩展名           | String                                                       |
| file（只读）             | 文件名称             | String                                                       |
| name（只读）             | 元素的用户分配名称   | String                                                       |
| path（只读）             | 文件路径             | String                                                       |

测试

通过`hasattr`获取对应属性名是否存在，通过`getattr`获取对应属性名的属性值

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 2:47
# @Author : zbh

import arcpy

file_path2 = r"G:\MyTestProject\arcpy2_test\Note3\data\Start.shp"
if arcpy.Exists(file_path2):
    print("file_path2 Found!")
    desc = arcpy.Describe(file_path2)
    prop_to_print = ['name', 'extension', 'path', 'catalogPath', 'bandCount']
    for prop_name in prop_to_print:
        if hasattr(desc, prop_name):
            print("{}: {}".format(prop_name, getattr(desc, prop_name)))
        else:
            print(u"Property '{}' not found".format(prop_name))
else:
    print("file_path2 Not Found!")
```

输出

由于是矢量数据，所以没有`bandCount`属性

```
file_path2 Found!
name: Start.shp
extension: shp
path: G:\MyTestProject\arcpy2_test\Note3\data
catalogPath: G:\MyTestProject\arcpy2_test\Note3\data\Start.shp
Property 'bandCount' not found
```

### 数据集属性（部分）

| 属性                     | 说明                                                         | 数据类型                                                     |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| datasetType（只读）      | 返回所描述的数据集类型任何容器GeoFeatureDatasetFeatureClassPlanarGraphGeometricNetworkTopologyTextTableRelationshipClassRasterDatasetRasterBandTINCadDrawingRasterCatalogToolboxToolNetworkDatasetTerrainRepresentationClassCadastralFabricSchematicDatasetLocator | String                                                       |
| DSID（只读）             | 数据集的 ID。                                                | Integer                                                      |
| extent（只读）           | [Extent](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/extent.htm) 对象。注:**extent** 仅适用于空间数据集。 | [Extent](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/extent.htm) |
| MExtent（只读）          | 以空格分隔的字符串 (MMin, MMax)。注:**MExtent** 仅适用于空间数据集。 | String                                                       |
| spatialReference（只读） | 返回数据集的 [SpatialReference](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/spatialreference.htm) 对象。注:**spatialReference** 仅适用于空间数据集。 | [SpatialReference](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/spatialreference.htm) |
| ZExtent（只读）          | 以空格分隔的字符串 (ZMin, ZMax)。注:**ZExtent** 仅适用于空间数据集。 | String                                                       |

测试

逻辑同上

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 12:10
# @Author : zbh

import arcpy

file_path = r"..\Note3\data\GeoData.gdb\MyShpfiles"
if arcpy.Exists(file_path):
    print("file_path Found!")
    desc = arcpy.Describe(file_path)
    prop_to_print = ['name', 'datasetType', 'extent', 'catalogPath', 'bandCount']
    for prop_name in prop_to_print:
        if hasattr(desc, prop_name):
            print("{}: {}".format(prop_name, getattr(desc, prop_name)))
        else:
            print(u"Property '{}' not found".format(prop_name))
else:
    print("file_path Not Found!")

```

输出

也是没有`bandCount`属性

```python
file_path Found!
name: MyShpfiles
datasetType: FeatureDataset
extent: 756856.1147 2969639.1121 764981.2868 2978678.4795 NaN NaN NaN NaN
catalogPath: ..\Note3\data\GeoData.gdb\MyShpfiles
Property 'bandCount' not found
```



### 表属性（部分）

| 属性                 | 说明                                                         | 数据类型                                                     |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| hasOID（只读）       | 指示表是否包含 ObjectID 字段。                               | Boolean                                                      |
| OIDFieldName（只读） | OID 字段（如果存在）名称。                                   | String                                                       |
| fields（只读）       | 此表的[字段](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/field.htm)对象的 Python 列表。这与使用 [ListFields](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/listfields.htm) 函数时相同。 | [Field](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/field.htm) |
| indexes（只读）      | 此表的[索引](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/index.htm)对象的 Python 列表。这与使用 [ListIndexes](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/listindexes.htm) 函数时相同。 | [Index](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/index.htm) |

测试

因为`fields`本身是ArcGIS指定的一种对象类型，需要使用对象或列表的方式处理，这里直接使用了官网的代码样例读取字段

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 12:22
# @Author : zbh

import arcpy

file_path = r"..\Note3\data\GeoData.gdb\MyShpfiles\Area"
if arcpy.Exists(file_path):
    print("file_path Found!")
    desc = arcpy.Describe(file_path)
    prop_to_print = ['name', 'OIDFieldName', 'bandCount']
    for prop_name in prop_to_print:
        if hasattr(desc, prop_name):
            print("{}: {}".format(prop_name, getattr(desc, prop_name)))
        else:
            print(u"Property '{}' not found".format(prop_name))
    print("--------------------")
    for field in desc.fields:
        print "%-22s %s %s" % (field.name, ":", field.type)
else:
    print("file_path Not Found!")
```

输出

```
file_path Found!
name: Area
OIDFieldName: OBJECTID
Property 'bandCount' not found
OBJECTID               : OID
Shape                  : Geometry
Id                     : Integer
Shape_Length           : Double
Shape_Area             : Double
```



### 要素类属性（部分）

| 属性                    | 说明                             | 数据类型 |
| ----------------------- | -------------------------------- | -------- |
| featureType（只读）     | 要素类的要素类型。               | String   |
| hasM（只读）            | 指示几何是否启用 m 值。          | Boolean  |
| hasZ（只读）            | 指示几何是否启用 z 值。          | Boolean  |
| hasSpatialIndex（只读） | 指示要素类是否具有空间索引。     | Boolean  |
| shapeFieldName（只读）  | Shape 字段的名称。               | String   |
| shapeType（只读）       | 几何形状类型。面折线点多点多面体 | String   |

测试

逻辑同上

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 13:13
# @Author : zbh

import arcpy

file_path = r"..\Note3\data\GeoData.gdb\MyShpfiles\Area"
if arcpy.Exists(file_path):
    print("file_path Found!")
    desc = arcpy.Describe(file_path)
    prop_to_print = ['name', 'featureType', 'shapeType', 'catalogPath', 'hasSpatialIndex']
    for prop_name in prop_to_print:
        if hasattr(desc, prop_name):
            print("{}: {}".format(prop_name, getattr(desc, prop_name)))
        else:
            print(u"Property '{}' not found".format(prop_name))
else:
    print("file_path Not Found!")
```

输出

```python
file_path Found!
name: Area
featureType: Simple
shapeType: Polygon
catalogPath: ..\Note3\data\GeoData.gdb\MyShpfiles\Area
hasSpatialIndex: True
```



### 图层属性（部分）

| 属性                 | 说明                                         | 数据类型                                                     |
| -------------------- | -------------------------------------------- | ------------------------------------------------------------ |
| dataElement（只读）  | 图层所指的数据源的 Describe 对象。           | [Describe](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe.htm) |
| featureClass（只读） | 与要素图层相关的要素类的 Describe 对象。     | [Describe](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe.htm) |
| FIDSet（只读）       | 用分号分隔的所选要素 ID 字符串（记录编号）。 | String                                                       |
| fieldInfo（只读）    | 图层的 FieldInfo 对象（属性集）。            | [FieldInfo](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-classes/fieldinfo.htm) |
| layer（只读）        | .lyr 文件内图层的 Describe 对象。            | [Describe](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe.htm) |
| nameString（只读）   | 图层的名称。                                 | String                                                       |
| table（只读）        | FeatureLayer 内表的 Describe 对象。          | [Describe](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe.htm) |
| whereClause（只读）  | 图层的定义查询 WHERE 子句。                  | String                                                       |

测试

这个的whereClause属性是指自己在属性窗口定义的查询语句，这里也是直接使用官网的代码样例

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 13:13
# @Author : zbh

import arcpy

file_path = r"..\Note3\data\Area.lyr"
if arcpy.Exists(file_path):
    print("file_path Found!")
    desc = arcpy.Describe(file_path)
    print "Name String:        " + desc.nameString
    print "Where Clause:       " + desc.whereClause

    if desc.dataElement.dataType == "FeatureClass":
        print "Feature class:      " + desc.dataElement.catalogPath
        print "Feature class Type: " + desc.featureClass.featureType
else:
    print("file_path Not Found!")
```

输出

```
file_path Found!
Name String:        Area
Where Clause:       
Feature class:      G:\MyTestProject\arcpy2_test\Note3\data\GeoData.gdb\MyShpfiles\Area
Feature class Type: Simple
```

### 栅格数据集属性（部分）

| 属性                    | 说明                                                        | 数据类型 |
| ----------------------- | ----------------------------------------------------------- | -------- |
| bandCount（只读）       | 栅格数据集内的波段数。                                      | Integer  |
| compressionType（只读） | 压缩类型                                                    | String   |
| format（只读）          | 栅格格式                                                    | String   |
| permanent（只读）       | 指示栅格的永久状态：False 表示临时栅格；True 表示永久栅格。 | Boolean  |
| sensorType（只读）      | 用于捕获图像的传感器类型。                                  | String   |

测试

直接使用的官网的代码样例修改

```Python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 14:01
# @Author : zbh

import arcpy

file_path = r"..\Note3\data\Raster1.tif"
if arcpy.Exists(file_path):
    print("file_path Found!")
    desc = arcpy.Describe(file_path)
    print "Band Count:       %d" % desc.bandCount
    print "Compression Type: %s" % desc.compressionType
    print "Raster Format:    %s" % desc.format
else:
    print("file_path Not Found!")
```

输出

```
file_path Found!
Band Count:       1
Compression Type: LZW
Raster Format:    TIFF
```

### 空间参考属性（部分）

| 属性                  | 说明                                        | 数据类型 |
| --------------------- | ------------------------------------------- | -------- |
| factoryCode (只读)    | The factory code of the spatial  reference. | Integer  |
| type (只读))          | The type of the spatial reference.          | String   |
| projectionName (只读) | 投影名称                                    | String   |
| GCSName (只读))       | The geographic coordinate system name.      | String   |

测试

空间参考属性需要写成`sr = arcpy.Describe(file_path).spatialReference`更方便后面的读取

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 14:16
# @Author : zbh

import arcpy

file_path = r"..\Note3\data\Raster1.tif"
if arcpy.Exists(file_path):
    print("file_path Found!")
    sr = arcpy.Describe(file_path).spatialReference
    prop_to_print = ['factoryCode', 'projectionName', 'GCSName', 'type']
    for prop_name in prop_to_print:
        if hasattr(sr, prop_name):
            print("{}: {}".format(prop_name, getattr(sr, prop_name)))
        else:
            print(u"Property '{}' not found".format(prop_name))
else:
    print("file_path Not Found!")
```

结果

```
file_path Found!
factoryCode: 4326
projectionName: 
GCSName: GCS_WGS_1984
type: Geographic
```

## 一些注意点

### 路径的区别

python本身只能处理系统路径，涉及到ArcGIS本身的数据库组织需要使用Arcpy读取

比如

```
G:\test\data.shp
G:\test\test.gdb\data\data1
```

前者可以通过OS模块读取，后者只能通过Arcpy读取

```python
#!/usr/bin/env python
# coding=utf-8
# @Time : 2024-04-26 1:20
# @Author : zbh

import arcpy
import os

file_path1 = r"G:\MyTestProject\arcpy2_test\Note3\data\GeoData.gdb\Raster1"
if(arcpy.Exists(file_path1)):
    print("arcpy.Exists Found!")
else:
    print("arcpy.Exists Not Found")
if(os.path.exists(file_path1)):
    print("os.path.exists Found!")
else:
    print("os.path.exists Not Found")
```

输出结果

```python
arcpy.Exists Found!
os.path.exists Not Found
```

### 字符串

Python2中输出有汉字尽量加上u，格式化输出用format

```python
print(u"name: '{}' ".format(name))
```

### 属性的说明

Describe属性是基本属性，大多数的数据都有。

Shapefile 支持[要素类属性](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/featureclass-properties.htm)、[表属性](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/table-properties.htm)和[数据集属性](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/dataset-properties.htm)。

栅格数据集还支持[数据集属性](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/dataset-properties.htm)。单波段栅格数据集也支持[栅格波段属性](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/raster-band-properties.htm)。

有些属性本身是对象，比如空间参考属性

## 总结

主要是学会通过Python读取属性，由于不同数据之间有不同的属性，不用单独记，遇到的时候查一下或者hasattr函数查询该属性是否存在即可

## 参考

ArcGIS的官方文档，还有很多种，用到的时候再查

[Describe—帮助 | ArcGIS Desktop](https://desktop.arcgis.com/zh-cn/arcmap/10.3/analyze/arcpy-functions/describe.htm)

![image-20240426170939176](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262331049.png)
