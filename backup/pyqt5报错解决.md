# pyqt5报错解决

[TOC]



## 环境

Python 3.9  Pyqt5 5.15

## 错误一

```
File "try.ui", line 1

  <?xml version="1.0" encoding="UTF-8"?>

  ^

syntaxError: invalid syntax
```

报这个错的，

把PyUIC的Arguments参数改为： -m PyQt5.uic.pyuic \$FileName\$ -o \$FileNameWithoutExtension\$.py  

参考： https://www.bilibili.com/read/cv17738858/?jump_opus=1 

## 错误二

```
Error while finding module specification for 'PyQt5.uic.pyuic' (ModuleNotFoundError: No module named 'PyQt5')
```

File|Settings|Tools|External Tools|PyUIC的【Program】选择pyuic5.exe,并将【Arguments】替换成

```
$FileName$ -o $FileNameWithoutExtension$.py
```

参考：[Pycharm-Error while finding module specification for ‘PyQt5.uic.pyuic‘ (ModuleNotFoundError: No modu_error while finding module specification for 'pyqt-CSDN博客](https://blog.csdn.net/zkw_1998/article/details/121806681)