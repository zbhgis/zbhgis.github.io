# Flask调试模式（debug mode）开启不了，显示Debug mode: off

## 环境

Python 3.9 

Flask 2.2.3

Pycharm 2022

## 问题

在run中加上了`debug=True`之后（如下）

```python
if __name__ == '__main__':
    app.run(debug=True)
```

但在实际运行的时候调试模式（debug mode）仍然没有生效，在控制台显示以下信息

```
 * Debug mode: off
```

![image-20240519161419066](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270902013.png)

## 解决

在项目配置处的三角标，点击打开【编辑配置】

![image-20240519161739671](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270902719.png)

找到FLASK_DEBUG，点击勾选，之后点击【确定】即可

![image-20240519161816279](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270902480.png)

重启项目调试模式即可生效，在控制台显示如下信息

![image-20240519162033698](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506270902628.png)