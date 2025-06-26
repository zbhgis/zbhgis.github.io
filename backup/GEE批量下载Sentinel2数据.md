# GEE批量下载Sentinel2数据

Google Earth Enginehttps://earthengine.google.com/网站批量下载数据，需要有谷歌账号和科学上网

## 界面功能

![image-20230712015903828](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712015903828.png)



## 导入研究区边界

1.学会导入roi的矢量文件，在【Assets】下选择【New】，导入shp文件

![image-20230712012523506](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712012523506.png)

![image-20230712012700256](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712012700256.png)

2.在弹出的界面可以选择自己的文件进行上传，除了在gee上的新建的数据集文件名需要修改之外，其他保持默认即可，最后点击【Upload】上传

![image-20230712013340325](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712013340325.png)

3.创建好之后就可以去copy别人的代码进行批量下载了，有两个数据可以需要自己手动导入，网上的教程有时没讲这部分，通过【Import】导入roi文件和数据集。其中，roi就是刚刚的矢量文件，在旁边的目录中有，点击之后在弹出的界面找到【Import】就可以导入了；数据集在上面的搜索栏中可以找到，比如下载Sentinel-2 L2A数据，就可以直接搜索“Sentinel”，点击搜索，之后找到对应的数据集，点击之后找到【Import】就可以导入

![image-20230712013745575](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712013745575.png)

![image-20230712014247262](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712014247262.png)

4.在导入这两个之后，就会再代码部分最上面出现如下三行（这三行不算代码，代码行数的计数从这三行之后开始），点击可以将”table”和“imageCollection”直接改名，因此在网上的一些代码中出现了未定义变量的报错，可能就是这两个错误；也可以通过在之后通过定义新变量来指代这两个，如下所示，这样名称就不用改了

![image-20230712014432273](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230712014432273.png)

```js
var roi = table;
var s2_collection = imageCollection;
```

## 数据下载

以哨兵数据批量下载为例（无云掩膜）

```js
var roi = table;

function filterImageCollection(collection) {
  // 日期 
  var startDate = '2021-01-01';
  var endDate = '2021-06-30';
  var filteredCollection = collection.filterDate(startDate, endDate);
  filteredCollection = filteredCollection.filterBounds(roi);
  // 云量
  filteredCollection = filteredCollection.filter(ee.Filter.rangeContains("CLOUDY_PIXEL_PERCENTAGE", 0, 30));
  return filteredCollection;
}
  var s2_collection = ee.ImageCollection('COPERNICUS/S2_SR');
  var filteredCollection = filterImageCollection(s2_collection);
  // 获取影像列表
  var imageList = filteredCollection.toList(filteredCollection.size());
  // 获取影像数量
  var count = imageList.size().getInfo();
  // 使用 for 循环进行迭代
for (var i = 0; i < count; i++) {
  // 通过索引获取影像
  var image = ee.Image(imageList.get(i));
  // 获取原始影像的文件名
  var originalFilename = ee.String(image.get('system:index')).getInfo();
  // 对影像进行研究区域裁剪和去云处理
  var maskedImage = image.clip(roi);
  // 选择需要的波段
  var composite = maskedImage.select(['B2', 'B3', 'B4', 'B8', 'B11']);
  // 导出波段合成影像
  Export.image.toDrive({
    image: composite,
    description: 'S2L2A_' + originalFilename,
    folder: 'S2L2A',
    region: roi,
    scale: 10,
    crs: "EPSG:4326",
    maxPixels: 1e13
  });
}
print('OK');
```

## 常见问题

1.如果代码点击【Run】之后，，没有报错，但是无响应，就是代码导出的数据太多了，因此在测试代码的时候一定要选择少一点的数据

2.测试代码时，可以加上一些print语句，看看是哪一步的问题

3.修改代码一定要及时保存

4.如果代码中波段合成了，但是导出数据仍然有多个类似的，可能是roi涉及到了多个区域，有些可能看似在一个区域，但是会触碰到别的影像的边界（因为有重叠），所有根据需求选择镶嵌或者是只下载需要的部分。

5.在【Task】中可以看到任务的源码

6.一次性不要【Run】太多数据，因为谷歌云盘只有15G

7.有时手速快，一次性【Run】太多数据，可能会在云盘里面给你创建多个同名文件夹

8.在谷歌云盘中的数据可以多选之后，直接打包成一个压缩包批量下载（如果一次选的数据量太多，系统会自动给你分成多个压缩包）

9.谷歌云盘的数据在删除掉（放到回收站，只保留30天）后仍然会占用空间，因此需要在回收站中进行【永久删除】

10..同名文件和同名文件夹在云盘中都一样，没有自动加上后缀区别，只能根据修改时间和其中的数据等信息来区分

11.下载好的数据有时在ENVI打开是全黑的，在ENVI右下角有一个构建金字塔的进度条，等他加载完再做定夺

12.一般情况下数据导出后只有1M左右的话，那么大概率是代码存在问题

13.下载的数据存在少部分不全的情况
<!-- ##{"timestamp":1698098400}## -->