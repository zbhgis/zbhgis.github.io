# Python多元非线性回归及绘图

[TOC]

在数字地形模型这门课做的一个小实验，代码实现的是以影像因子和地形要素为自变量，采样后的高程计算出的指标为因变量进行回归，本质上是通过curve_fit进行多元非线性回归，但是当时的要素偏多，需要写代码依次使用不同的自变量和因变量回归

环境：Python 3.9

## 部分数据截图

![image-20240425231728608](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262358404.png)



## 代码逻辑

### 导入所需库和模块

```python
# coding=gbk
# -*- coding = utf-8 -*-

import numpy as np
import pandas as pd
from scipy.optimize import curve_fit
import matplotlib.pyplot as plt
```

- `numpy`：用于数值计算和数组操作。
- `pandas`：用于读取和处理Excel数据。
- `scipy.optimize.curve_fit`：用于非线性最小二乘拟合。
- `matplotlib.pyplot`：用于绘制三维散点图和曲面。

### 定义非线性模型函数

```python
def nonlinear_model(xy, a, b, c):
    x, y = xy
    return (a * x - b) * y + c
```

定义`nonlinear_model`函数，它接受两个坐标`xy`（包含x和y的元组）以及三个参数`a`, `b`, `c`，即 `(a * x - b) * y + c`

### 设置数据源和变量

```python
excel_file_path = 'E:\zbh.xlsx'    
df = pd.read_excel(excel_file_path)

x = 'R'
y = 'SOS'
z = 'MEAN'
x_data = np.array(df[x])
y_data = np.array(df[y])
z_data = np.array(df[z])
```

指定的Excel文件路径可以改改，读取变量`R`, `SOS`, `MEAN`的列数据，这里也需要根据数据本身来改

### 非线性回归与参数估计

```python
popt, pcov = curve_fit(nonlinear_model, (x_data, y_data), z_data)
a_fit, b_fit, c_fit = popt
z_fit = nonlinear_model((x_data, y_data), a_fit, b_fit, c_fit)
```

使用`scipy.optimize.curve_fit`对给定的`nonlinear_model`函数进行拟合，传入观测到的`(x_data, y_data)`对和对应的`z_data`作为目标值。`curve_fit`返回最佳拟合参数`popt`和协方差矩阵`pcov`。接着，将最佳参数赋值给`a_fit`, `b_fit`, `c_fit`，并使用这些参数计算出所有数据点的拟合值`z_fit`。

### 计算拟合优度指标和均方根误差

```python
ss_total = np.sum((z_data - np.mean(z_data)) ** 2)
ss_reg = np.sum((z_fit - np.mean(z_data)) ** 2)
r_squared = ss_reg / ss_total
rmse = np.sqrt(np.mean((z_data - z_fit) ** 2))

print("R方:", r_squared)
print("RMSE:", rmse)
```

计算拟合优度指标（R方），均方根误差（RMSE），最后打印

### 构建拟合公式字符串

```python
formula = "{} = ({:.2f} * {} + ({:.2f})) * {} + {:.2f}".format(z, a_fit, x, b_fit, y, c_fit)
print(formula)
```

用已得到的最佳参数和变量名构建最终的拟合公式，并保留两位小数精度。

### 绘制三维散点图和拟合曲面

```python
fig = plt.figure(figsize=(6, 6))
ax = fig.add_subplot(111, projection='3d')

ax.scatter(x_data, y_data, z_data, color='blue', label='Data Points')
X, Y = np.meshgrid(np.linspace(min(x_data), max(x_data), 30),
                   np.linspace(min(y_data), max(y_data), 30))
Z = nonlinear_model((X.flatten(), Y.flatten()), a_fit, b_fit, c_fit).reshape(X.shape)
ax.plot_surface(X, Y, Z, color='r', alpha=0.6, label='Fitted Surface')

ax.set_xlabel(x)
ax.set_ylabel(y)
ax.set_zlabel(z)
plt.title(x +"-"+ y + "-" + z + ":" + formula)
plt.show()
```

计算Z值和绘图

## 完整代码

```python
# coding=gbk
# -*- coding = utf-8 -*-

import numpy as np
import pandas as pd
from scipy.optimize import curve_fit
import matplotlib.pyplot as plt

# 定义非线性模型函数
def nonlinear_model(xy, a, b, c):
    x, y = xy
    return (a * x - b) * y + c

# 指定Excel文件路径并读取
excel_file_path = 'E:\zbh.xlsx'
df = pd.read_excel(excel_file_path)
x = 'R'
y = 'SOS'
z = 'MEAN'
x_data = np.array(df[x])
y_data = np.array(df[y])
z_data = np.array(df[z])

# 利用 curve_fit 进行非线性回归
popt, pcov = curve_fit(nonlinear_model, (x_data, y_data), z_data)
a_fit, b_fit, c_fit = popt
z_fit = nonlinear_model((x_data, y_data), a_fit, b_fit, c_fit)

# 计算指标
ss_total = np.sum((z_data - np.mean(z_data)) ** 2)
ss_reg = np.sum((z_fit - np.mean(z_data)) ** 2)
r_squared = ss_reg / ss_total
rmse = np.sqrt(np.mean((z_data - z_fit) ** 2))
print("R方:", r_squared)
print("RMSE:", rmse)
# 拟合公式
formula = "{} = ({:.2f} * {} + ({:.2f})) * {} + {:.2f}".format(z, a_fit, x, b_fit, y, c_fit)
print(formula)

# 绘制三维散点图和拟合曲面
fig = plt.figure(figsize=(6, 6))
ax = fig.add_subplot(111, projection='3d')

# 散点图
ax.scatter(x_data, y_data, z_data, color='blue', label='Data Points')
# 曲面图
X, Y = np.meshgrid(np.linspace(min(x_data), max(x_data), 30),
                   np.linspace(min(y_data), max(y_data), 30))
Z = nonlinear_model((X.flatten(), Y.flatten()), a_fit, b_fit, c_fit).reshape(X.shape)
ax.plot_surface(X, Y, Z, color='r', alpha=0.6, label='Fitted Surface')

ax.set_xlabel(x)
ax.set_ylabel(y)
ax.set_zlabel(z)
plt.title(x +"-"+ y + "-" + z + ":" + formula)
plt.show()
```

## 部分结果

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202506262338915.png)
## 总结
由于这次实验用到的数据量较少，因此画图的效果感觉一般，趋势不明显，计算出的指标参考意义也有限，数据量大一点效果好坏会一目了然
## 参考
[Matplotlib文档](https://matplotlib.org/stable/users/index.html)
[Scipy Curve_fit文档](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve%5Ffit.html)