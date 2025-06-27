# Conda安装opencv后显示找不到指定的模块

[TOC]



## 问题

直接通过conda install opencv安装的opencv，通过Import cv2之后，显示DLL load failed while importing cv2: 找不到指定的模块。

```
conda install opencv
```

```
DLL load failed while importing cv2: 找不到指定的模块。
```

![image-20240507171645404](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270847148.png)

## 解决

经过多方查找，最终确定是版本对应的问题，我用的是Python3.9，对应的opencv版本4.5.1，而我用的源默认下载的版本是4.6.0，因此会报错，所以卸载opencv之后，直接通过conda命令指定对应的版本下载即可

```
conda uninstall opencv
```

```
conda install opencv==4.5.1 -c conda-forge
```

## 总结

以后安装第三包之前一定要确认好对应的环境以及相应的包的依赖版本，尽量不要直接conda install，很多时候报错就是版本的对应问题，找不到对应的版本的时候就在命令后加上-c conda-forge，速度慢但是内容全

```
-c conda-forge
```



## 参考

https://blog.csdn.net/weixin_44340978/article/details/132647309

```
https://blog.csdn.net/weixin_44340978/article/details/132647309
```

