# USGS网站下载Landsat 5/7/8/9数据最新详细教程（注册、筛选、单波段、批量下载等），附常见问题

@[toc]
## 前言

本文主要介绍了在USGS网站上下载Landsat系列影像的过程，发现了很多坑，特此记录一下。下载之后的影像预处理过程介绍可以参考以下文章。
[ENVI 5.3对USGS网站下载的Landsat 8/9 C2L2地表反射率数据进行预处理（波段合成、裁剪、镶嵌、定标、去云）](https://blog.csdn.net/zbh13859825167/article/details/145453793)
```
https://blog.csdn.net/zbh13859825167/article/details/145453793
```

## 环境

Edge浏览器（可能需要科学上网）

## 网站

[EarthExplorer (usgs.gov)](https://earthexplorer.usgs.gov/)

```
https://earthexplorer.usgs.gov/
```

![在这里插入图片描述](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270912731.png)


## 注册

1、在主页右上角点击【Login】

![image-20240524010043786](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913757.png)

2、如果没有账号，就选择【Create New Account】

![image-20240524010116319](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913724.png)

3、按右侧的要求填写好用户名和密码之后，点击【Continue】

![image-20240524011826693](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913339.png)

4、之后填写如下的一些使用信息后，点击【Continue to Contact Information】

![image-20240524012112074](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913880.png)

![image-20240524012128681](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913703.png)

![image-20240524012202411](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913501.png)

5、填写如下的个人信息之后，点击【Save Contact Information】

![image-20240524012234986](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913479.png)

6、之后确认信息无误之后，点击【Submit Registeration】

![image-20240524012624418](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913987.png)

7、显示注册请求已提交，可以点击【Return to Login Page】。这个时候去看看自己的邮箱里面有没有收到注册链接，点击之后即可激活账号。

![image-20240524012708580](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913238.png)

## 登录

在【Login】界面中，输入用户名和密码之后，点击【Sign In】即可登录

![image-20240524014018117](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913879.png)

## 区域筛选

区域筛选界面：分为行政区搜索、地址搜索、行列号搜索、文件上传、当前地图获取、地理坐标获取、预定义文件获取，可以根据自己的需要选择其中的一种方式即可，下面会逐一介绍

![image-20240524105842692](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913072.png)

### 行政区划搜索

在【Select a Geocoding Method】选择【Feature（GNIS】,选择【US Features】或者【World Features】，之后可以在【Feature Name】进行检索或者选择，再点击【Show】，就会在下方出现结果，在结果中点击对应的【Placename】就会在右侧的地图出现对应的标记



![image-20240524110052577](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913869.png)

![image-20240524112020735](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913976.png)

### 地址搜索

在【Select a Geocoding Method】选择【Address/Place】，下方的搜索框中输入地名后，点击【Show】，就会在下方出现结果，在结果中点击对应的【Address/Place】就会在右侧的地图出现对应的标记

![image-20240524112304903](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270913836.png)

![image-20240524112447407](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914163.png)



### 行列号搜索

在【Select a Geocoding Method】选择【Path/Row】，下方的【Point】或【Polygon】选择其中一种标记形式，【Type】中选择使用【WRS2】（Landsat 4/5/7/8/9）或者【WRS1】（Landsat 1/2/3），输入对应的行列号，点击【Show】，点击【Show】，就会在下方出现结果，并在右侧地图出现对应的标记

![image-20240524113945450](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914291.png)

### 文件上传

切换到【KML/Shapefile Upload】，选择一种文件形式，之后选择【Select File】上传具体的文件即可

![image-20240524114222258](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914717.png)

![image-20240524114439645](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914459.png)

![image-20240524114508483](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914400.png)

### 当前地图获取

在上述的操作中，对应的标记形式会记录在如下【Polygon】区域，可以自行选择【Degree/Minute/Second】或者【Decimal】形式显示，或者进行编辑或删除。

【Use Map】是通过右侧地图直接创建当前区域的多边形标记，【Add Coordinate】是添加点标记，【Clear Coordinates】是清除当前所有标记

![image-20240524114618781](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914603.png)

如果是切换到【Circle】，那么就是需要输入中心店经纬度和半径，点击【Apply】应用，【Clear Circle】清除标记

![image-20240524115545893](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914836.png)

![image-20240524120113018](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914095.png)

如果是切换到【Predefined Area】，那么就可以使用预定义的标记（美国内），【Apply Shape】选择区域，【Clear Shape】清除标记

![image-20240524115915676](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914109.png)

![image-20240524120135189](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914643.png)

## 影像筛选

影像初步筛选包括日期筛选、云量筛选、结果显示、数据集筛选、高级筛选、根据结果筛选，一般来说这几个步骤都要进行，下面会按照顺序介绍

### 日期筛选

在【Data Range】面板下，选择起止日期，也可以在【Search months】中选择具体要获取的月份，默认为【all】，我这里选择2024.1.1至2024.5.10之间的一月份和五月份影像

![image-20240524121315686](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914450.png)

### 云量筛选

在【Cloud Cover】面板下，选择云量范围以及是否包含未知云量的影像，我这里选择了低于30%

![image-20240524121446604](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914779.png)

### 结果展示

在【Result Options】选择结果展示页面的每页的影像展示个数，我这里保持默认

![image-20240524121542594](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914300.png)

### 数据集筛选

在进行上述操作之后，点击【Data Sets】，选择数据集。可以选择【Use Data Set Prefilter】是否进行预过滤，也可以搜索数据集名称，我这里直接按照默认设置，并选择Landsat 8/9的C2L2级别产品，可以根据需要选择其他数据

![image-20240524122706400](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270914851.png)

![image-20240524122133489](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270919800.png)

![image-20240524122114796](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270919620.png)

### 高级筛选

在进行上述操作之后，点击【Additional Criteria】，进行进一步筛选。在这里进行筛选需要对Landsat数据有一定的了解，我这里没有设置筛选条件。

![image-20240524123037223](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915603.png)

![image-20240524122926805](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915439.png)

### 根据结果筛选

在进行上述操作之后，点击【Result】，进行结果查询。

![image-20240524123154828](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915926.png)

可以根据需要，选择功能进行操作。主要是需要添加至图层查看影像的具体质量，以及尽量选择后缀为T1级别的数据下载（质量较好）

![image-20240524132414155](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915207.png)

点击【Show Metadata And Browse】，添加至图层显示，查看研究区范围内的影像情况如何。

![image-20240524133152733](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915508.png)

![image-20240524132729434](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915334.png)

## 影像下载

USGS支持单波段和添加至Bulk中批量下载，确定好需要的影像之后，就可以根据需要进行操作。我接下来选择其中一幅进行演示。



![](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915950.png)

![image-20240524133703035](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915777.png)

### 单波段下载

点击【Select Files】，在之后的界面选择【Download all Selected Now】，也可以选择【Add All Selected to Bulk】到时候批量下载

![image-20240524133819027](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915902.png)

![image-20240524133948474](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915669.png)

### 整个产品下载

点击【Product Options】，之后点击最上面的下载按钮就是直接下载整个产品

![image-20240524134231964](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270915649.png)

![image-20240524134353883](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916552.png)

### 批量下载

一般就是将所要的数据添加至Bulk后，再进行批量下载，以下总结可以直接添加至待批量下载列表的方法（红框选项），根据需要选择即可。具体的批量下载方法我之前已经总结过了，见以下文章。

[在USGS上批量下载Landsat系列影像（最新）-CSDN博客](https://blog.csdn.net/zbh13859825167/article/details/133661780)

```
https://blog.csdn.net/zbh13859825167/article/details/133661780
```

![image-20240524134727249](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916918.png)

![image-20240524134743742](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916610.png)

![image-20240524134807304](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916049.png)

![image-20240524134901928](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916624.png)

![image-20240524134920068](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916893.png)

## 问题

1、注册时显示Captcha value is wrong，如下所示。

网络问题，国内网络经常出现这个问题，需要科学上网。

![image-20240524010840453](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916300.png)

2、邮箱没有收到注册信息。

可以尝试切换注册邮箱为谷歌邮箱或者163邮箱。

3、登录的时候登录不了，并在上面显示无法进入，如下所示。

多试几次，大概率是网络不稳定的问题。

![image-20240524014452021](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916036.png)4、有时候操作了但是网站没有反应，如下所示。

网络不稳定，等不及可以直接刷新网页。

![image-20240524015126726](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916264.png)

5、直接上传Shapefile数据失败，如下所示。

因为只有shp文件就没有投影等其他矢量数据信息， 因此官方推荐的是需要将至少shp、shx、dbf、prj这四个文件放在一个zip格式的压缩包中，直接上传，不想挑的话，可以直接一股脑把shp文件及其相关文件都打包为zip格式一起上传。

![image-20240524015746249](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916733.png)



6、上传的Shapefile文件中，只有一个省或市的边界也会失败，如下所示。

如果该边界数据中也包含了岛屿的边界，导致出现了两个及以上的多边形，该网站无法识别，因此需要上传中只能一个多边形或者闭合线数据。

![image-20240524015635628](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270916084.png)

7、重新上传文件的时候，有时候上传了但是网页没有反应。

刷新网页即可重新上传。


8、在日期选择时，起止日期有时候包含的年份不全。

在修改起止日期时，网站默认开始日期必须小于结束日期，建议按照顺序设置两个日期。