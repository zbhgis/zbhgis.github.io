# SNAP软件对Sentinel-2数据进行重采样存在问题

**1.问题：重采样出现了Message：dataType out of range!的提示**

解决：以记事本格式打开并编辑以下文件

```
C:\Users\用户名\.snap\etc\s2tbx.properties
```

在最后添加以下信息并保存

```
user.openjp2.jna=true
```

重启SNAP后软件即可执行重采样

![image-20231221194253165](https://gitee.com/zbhgis/pic/raw/master/blog/image-20231221194253165.png)



**2.问题：处理完数据之后C盘和D盘爆满**

解决：C盘中是由于以下文件位置会有缓存，处理完后可以直接删除

```
C:\Users\用户名\.snap\var\cache\s2tbx\l2a-reader
```

![image-20231221192915397](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262243288.png)

D盘中是由于以下文件位置会有临时文件，通过电脑的清理垃圾功能会清除掉，或者在以下的D盘的temp文件中找到以下缓存文件手动清楚

```
D:\temp\snap-用户名
```

![image-20231221193221629](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262243624.png)



**3.问题：SNAP中重采样的速度慢**

在SANP中对某一幅影像所有波段，按照B2分辨率进行重采样之后的数据在16G左右，因此重采样之前加上一个BandSelect步骤，选择需要的波段进行重采样即可加快速度，尽量不要全部重采样。

![image-20230709144114576](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262243083.png)


<!-- ##{"timestamp":1698098400}## -->