# 在USGS上批量下载Landsat系列影像

## 前言

试了一下USGS提供的批量下载的功能，整体使用体验OK。

## 正文

1.打开USGS网站(https://earthexplorer.usgs.gov/)，登录-注册-设置条件-选择数据集-查找等一系列步骤后，来到了这个界面

![image-20231007163538182](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231007163538182.png)

2.在这个界面我们可以明显得看到，每个数据下面有个小菜单，我们可以通过这个菜单中的这个按钮**【Add  to Bulk Download】**，将想要批量下载的数据添加到【Item Basket】，如果这个数据添加成功，那么这个按钮就会变成绿色的（点击之后有一点延迟，过一小会就变亮了)

![image-20230708225117110](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708225117110.png)

![image-20230708225711575](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708225711575.png)

3.如果选择好数据之后，那么上方菜单中的**【Item Basket】**就会右下角的数字就会变成对于所选择的数据量

![image-20230708230029721](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708230029721.png)

4.点击**【Item Basket】**进入到如下界面，并点击**【Start Order】**

![image-20230708230150666](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708230150666.png)

5.加载片刻之后，会出现以下界面，点击Landsat 8-9左边的一个倒三角标，将展开所选的各个数据

![image-20230708230445920](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708230445920.png)

在此界面，可以通过【Options】或者各个数据最右侧的按钮对数据进行操作

![image-20230708231125031](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708231125031.png)

6.通过鼠标左键，单击想要批量下载的数据，确认无误后，最后点击右下角的**【Submit Product Selections】**进行筛选（如果显示提交失败，显示一串提示“Unable。。。”，先确认自己是否选择了文件，再去排查其他问题）

![image-20230708231556747](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708231556747.png)

7.Order创建成功之后，会返回如下界面，显示了申请到的Order名称，如果网络没问题的话，对应的邮箱也会在1-2分钟之内，收到来自usgs的邮件通知

![image-20230708232054508](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708232054508.png)

![image-20230708231857147](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708231857147.png)

8.再点击如下界面中的超链接**【Bulk Download Web Application】**，进入批量下载界面（根据官方提醒，通过该Web应用下载不需要安装Java环境，不过需要在基于chorme的浏览器上使用或者edge上使用，本次测试使用的edge浏览器）

![image-20230708232248409](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708232248409.png)

9.进入到如下界面后，点击绿色按钮**【Launch Bulk Download Web Application】**

![image-20230708232636976](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708232636976.png)

10.之后稍等片刻，即可看到如下界面（由于本次测试之前就创建过两次Order，所以共有3个Order）

![image-20230709001323234](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230709001323234.png)

11.进入任意一个Order后，会弹出以下窗口，可以提前新建好文件夹，这里我们选择建好的文件夹存放数据

![image-20230708233354331](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708233354331.png)

12.在选择好文件夹之后，会弹出以下窗口（edge浏览器），依次同意

![image-20230708233456940](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708233456940.png)

![image-20230708233512861](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708233512861.png)

13.点击其中一个Order后，可以查看到以下信息

![image-20230708234711793](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708234711793.png)

![image-20230708234111132](https://gitee.com/zbhgis/pic/raw/master/blog/image-20230708234111132.png)

14、Windows下载完成提示

![image-20240519221506902](https://gitee.com/zbhgis/pic/raw/master/blog/image-20240519221506902.png)

## **总结**

1.关于下载的诸多事宜，如限制、设置等，在帮助中均有所提及，这里就不啰嗦了

2.还可以通过GEE代码或者生成URL等方式更加便捷地进行批量下载，由于其他网站可能没有以上的Web应用，因此在其他网站可以通过这两个思路进行下载

3.由于是网络问题，部分操作会有所延迟，需要耐心等待片刻，不要频繁操作，比如在将数据添加到Item Basket时，那个小按钮很容易卡顿

4.进行了个简单的小测试，发现换个浏览器登录USGS后，貌似无法记住你的Order及其中的数据集，所以推荐申请之后直接开始下载

<!-- ##{"timestamp":1696629600}## -->