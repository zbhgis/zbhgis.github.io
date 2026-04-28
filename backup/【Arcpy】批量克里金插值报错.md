

[TOC]



## 问题

在进行实验的时候，Arcpy中批量进行克里金插值报错，主要就是在运行这个工具的时候，一直报错，改了很多参数也不行

```
ERROR 010079: 无法估算半变异函数。
```

![image-20240503174302088](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270015546.png)

![image-20240503174332071](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270015605.png)

## 解决

去网络上找了很多方法，比如修改为默认路径，调整像元大小都不管用，后来自己在ArcGIS中去试着跑了一下克里金插值，才知道是参数设置的问题，在ArcGIS中执行克里金插值的时候lagSize、partialSill、Nugget要么都不设置（即保持为空），要么就都设置一个非零值，这个问题在ArcMap中会直接提示，但是在Arcpy中不会，因此在代码中只需要遵循上述规则就可以了，这也说明用Arcpy之前还是需要对这个工具有一定了解，避免低级错误。最后改完就能正常执行了

![image-20240503174838975](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270015351.png)

## 参考

[克里金法 (Spatial Analyst)—ArcGIS Pro | 文档](https://pro.arcgis.com/zh-cn/pro-app/latest/tool-reference/spatial-analyst/kriging.htm)