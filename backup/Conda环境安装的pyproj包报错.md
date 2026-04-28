# Conda环境安装的pyproj包报错

[TOC]



## 问题

在conda创建的Python3.9虚拟环境中安装pyproj包3.6在运行时出现以下报错

```
UserWarning: pyproj unable to set database path. _pyproj_global_context_initialize()
```

## 解决

先激活并进入创建的环境

```
conda activate sa_test
```

先尝试卸载后重装

```
conda remove --force pyproj
```

```
conda install pyproj
```

如果不行的话，就直接通过pip重新安装

```
conda remove --force pyproj
```

```
pip install pyproj
```

重装之后就不会报错了

![image-20240503173223902](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270014947.png)



## 参考

[python - On fresh Conda installation of PyProj: pyproj unable to set database path. _pyproj_global_context_initialize() - Stack Overflow](https://stackoverflow.com/questions/69630630/on-fresh-conda-installation-of-pyproj-pyproj-unable-to-set-database-path-pypr)

```
https://stackoverflow.com/questions/69630630/on-fresh-conda-installation-of-pyproj-pyproj-unable-to-set-database-path-pypr
```

