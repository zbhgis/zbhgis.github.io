# Arcpy入门学习笔记（一）：前期准备

使用Arcpy需要先安装ArcGIS或Pro，此处省略

[TOC]

## 环境配置

pycharm安装+ArcGIS 10.6提供的python2.7解释器

在【Settings】中的【Project】下的【Python Interpreter】选择ArcGIS自带的Python2.7

![image-20240420222738713](https://gitee.com/zbhgis/pic/raw/master/blog/image-20240420222738713.png)

## Pycharm调试功能

断点：在代码行号之后的空白点击一下即可，再次点击取消

![image-20240420224302787](https://gitee.com/zbhgis/pic/raw/master/blog/image-20240420224302787.png)

调试：debug按钮或Shift+F9

![image-20240420224418276](https://gitee.com/zbhgis/pic/raw/master/blog/image-20240420224418276.png)

F8：单步，遇到断点后停止运行

F7：进入函数

Alt+shift+F7：进入自己编写的代码

shift+F8：跳出函数

F9：到下一个断点或退出调试

Alt+F9：移动到光标

```Python
# coding=utf-8
# @Time : 2024-04-19 23:30

# 调试用
def print_str(num):
    for _ in range(num):
        print("你好")

if __name__ == '__main__':
    a = 2
    print_str(a)
    b = a
    print(b)
    b = 1
    print_str(b)
```

## Python2基础

### 数据类型

**整型**：整数的表示与运算

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# 整数运算
num1 = 100
num2 = 200
print "两数之和为：", num1 + num2
print "两数之差为：", num1 - num2
print "两数之积为：", num1 * num2
print "两数之商为：", num1 / num2  # 在Python 2中，整数除法结果为整数（向下取整）
print "两数之商（浮点数）为：", float(num1) / num2
```

**字符串**：文本的表示与操作

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# 字符串定义与拼接
greeting = "你好！"
name = "小明"
message = greeting + "，" + name + "！"
print message

# 字符串切片与索引
sentence = u"浩瀚地学"
print "首字符：", sentence[0]
print "倒数第二个字符：", sentence[-2]
print "子串：", sentence[2:4]

# 字符串格式化
age = 999
info = "今年{}岁。".format(age)
print info
```

**列表**：有序可变序列

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# 列表定义与操作
fruits = ["苹果", "香蕉", "橙子"]
print "列表元素个数：", len(fruits)
fruits.append("葡萄")
print "添加元素后：", repr(fruits).decode('string_escape')
fruits.insert(1, "梨")
print "插入元素后：", repr(fruits).decode('string_escape')
del fruits[2]
print "删除元素后：", repr(fruits).decode('string_escape')
```

**元组**：有序不可变序列

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# 元组定义与操作
colors = ("红色", "绿色", "蓝色")
print "元组元素个数：", len(colors)
new_tuple = colors[:2] + ("紫色",)
print "创建新元组：", repr(new_tuple).decode('string_escape')
```

**字典**：键值对存储结构

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# 字典定义与操作
student = {"姓名": "张三", "年龄": 20, "成绩": 95}
print "学生信息：", repr(student).decode('string_escape')
print "学生姓名：", student["姓名"]
student["成绩"] = 97
print "更新成绩后：", repr(student).decode('string_escape')
```

### 语句

**条件判断**：if...elif...else...

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

score = 86

if score >= 90:
    print "优秀"
elif score >= 80:
    print "良好"
else:
    print "需努力"
```

**循环**：for...in...，while...

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# for循环遍历列表
for fruit in ["苹果", "香蕉", "橙子"]:
    print "喜欢吃的水果：", fruit

# while循环计数
count = 1
while count <= 5:
    print "这是第{}次循环".format(count)
    count += 1
```

**循环控制语句**：break、continue

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

# break用于提前终止循环
for i in range(10):
    if i == 5:
        break
    print i

# continue用于跳过当前循环迭代
for j in range(10):
    if j % 2 == 0:
        continue
    print j
```

### 函数

**定义与调用**

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

def print_str(name):
    """定义一个打印问候语的函数"""
    print "!{}！".format(name)

print_str("张三")  # 调用函数
```

**参数传递**：位置参数、关键字参数、默认参数、可变参数

```python
# coding=utf-8
# @Time : 2024-04-20 23:42

def calculate_area(shape, length=10, width=5):
    """计算矩形或正方形面积"""
    if shape == "rectangle":
        area = length * width
    elif shape == "square":
        area = length ** 2
    else:
        raise ValueError("未知形状")
    return area

print "矩形面积：", calculate_area("rectangle", 4, 6)
print "正方形面积（使用默认边长）：", calculate_area("square")
```

## Python2注意点

1、以下形式的print后如果加括号就会输出中文乱码

```python
# 整数运算
num1 = 100
num2 = 200
print("两数之和为：", num1 + num2)
print "两数之和为：", num1 + num2
```

2、列表、元组中的中文元素控制台输出乱码，需要加上repr解码

```python
fruits = ["苹果", "香蕉", "橙子"]
print "列表元素个数：", len(fruits)
fruits.append("葡萄")
print "添加元素后：", fruits
print "添加元素后：", repr(fruits).decode('string_escape')
```

3、字符集设置，在开头加上两句中其中一个

```python
# coding=utf-8
```

```python
# -*- coding:utf-8 -*-
```

4、py2中汉字按照两个字符算，需要加u按照一个字符算

```python
print (len("浩瀚地学"))
print (len(u"浩瀚地学"))
```

5、创建一个“sitecustomize.py“的Python文件后，粘贴到”G:\ArcGIS\Python27\ArcGIS10.6\Lib\site-packages“的目录下，之后重启ArcGIS，可以解决部分中文乱码问题；或者在自己的py文件开头加上以下代码

```python
#coding=utf8

import sys

reload(sys)

sys.setdefaultencoding('utf8')
```

![image-20240420004523622](https://gitee.com/zbhgis/pic/raw/master/blog/image-20240420004523622.png)

## 总结

Python2对于中文的支持特别不友好，尽量不要用中文

<!-- ##{"timestamp":1713736800}## -->