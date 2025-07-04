# Landsat 8/9 C2L2使用注意点（简略版）

## 详细版（更新中）

[Landsat 8/9 C2L2级别数据表面反射率产品使用注意点-CSDN博客](https://zbhgis.blog.csdn.net/article/details/139023038)

```
https://zbhgis.blog.csdn.net/article/details/139023038
```



## 像元值转化

表面反射率产品时和表面温度时，即对应的SR和ST波段的遥感数据时，需要进行像元值的转换，其转换公式与Collection1不一样（Collection1已经弃用了，但在地理空间数据云应该还可以下载），在使用时最好先进行转换

| 科学产品              | 缩放因子   | 偏移量 | 填充值 | 数据类型       |   有效范围   |
| --------------------- | ---------- | ------ | ------ | -------------- | :----------: |
| Collection2地表反射率 | 0.0000275  | -0.2   | 0      | 无符号16位整数 | 7273 - 43636 |
| Collection2地表温度   | 0.00341802 | 149    | 0      | 无符号16位整数 | 293 - 65535  |

即在影像像元值中剔除无效像元值之后，使用Digital Number (DN) * scale_factor + offset计算，即缩放因子*像元值+偏移量

表面反射率：Landsat Collection 2 表面反射率的比例因子为 0.0000275，每个像素的额外偏移为 -0.2。比如，18639为有效值， 因此乘以 0.0000275 比例因子，然后将 -0.2 相加，获得反射率值 0.313。

表面温度：Landsat Collection 2 表面温度的比例因子为 0.00341802，每个像素的额外偏移量为 149.0。 比如，44947为有效值， 因此乘以 0.00341802 比例因子，将 149.0 相加，得到 302.6 开尔文。

## 水体区域效果差

该产品的数据对于水体的反演效果不太友好，因此在涉及到水体的时候需要斟酌一下，比如在计算NDVI的时候，水体区域的NDVI值可能会特别高，因此可以考虑下载Level 1的数据自行进行大气校正后再计算相关的指数

官方解答：由于水的表面反射率本身较低，Landsat 大气校正和表面反射率反演算法对于水体来说并不理想。同样，在明亮的目标（如雪地和海滩）上可能会遇到大于 1.0 的表面反射率值。这些是 Landsat 表面反射率产品中的已知计算伪影。

## 总结

第一个点很重要，因为这个在计算AWEI等本身就没有进行归一化的指数的时候值会很离谱，此外就算是归一化差值型指数也尽量进行系数转化，因为在Level2中还带有偏移量和有效值范围，没有办法通过比值完全抵消，因此在使用时预处理一定要做好，在进行一个实验时发现的，虽然重做了一遍，也算是弥补了我的一个知识缺口，之后有时间写一个详细版的，这个级别的数据还有很多个“坑”。

## 参考

[Landsat Collection 2 Known Issues | U.S. Geological Survey (usgs.gov)](https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR)

```
https://www.usgs.gov/landsat-missions/landsat-collection-2-known-issues#SR
```

