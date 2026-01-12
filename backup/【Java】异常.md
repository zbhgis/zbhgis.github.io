

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括异常的体系，自定义异常，以及异常的处理

2.笔记对应视频134~135节

# 更新记录

无

# 异常的体系

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601071713955.png)

Error：代表的系统级别错误（属于严重问题），也就是说系统一旦出问题，sun公司会把这些问题封装成Error对象给出来

Exception：异常，代表的是我们程序可能出现的问题

- 运行时异常：RuntimeException及其子类，编译阶段不会出现错误提醒，运行时出现的异常（如：数组索引越界异常）
- 编译时异常：编译阶段就会出现错误提醒的。（如：日期解析异常）

Exception1.java

```Java
package com.zbhgis.exceptions;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Exceptions1 {
    // 解决异常方式二：添加ParseException
    public static void main(String[] args) throws ParseException{
        // 运行时异常
        // int[] arr = {11, 22, 33};
        // System.out.println(arr[5]);

        // 编译时异常
        // SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        // Date d = sdf.parse("2022");
        // System.out.println(d);

        // 解决异常方式一：try-catch
        // try {
        //     SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        //     Date d = sdf.parse("2022");
        //     System.out.println(d);
        // } catch (ParseException e) {
        //     e.printStackTrace();
        // }

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date d = sdf.parse("2022");
        System.out.println(d);
    }
}
```

打印结果

```Plain
Exception in thread "main" java.text.ParseException: Unparseable date: "2022"
        at java.base/java.text.DateFormat.parse(DateFormat.java:399)
        at com.zbhgis.exceptions.Exceptions1.main(Exceptions1.java:29)
```

# 自定义异常

自行定义异常类

## 自定义运行时异常

定义一个异常类继承RuntimeException，重写构造器，通过throw new 异常类() 来创建异常对象并抛出。IDEA反馈较弱

AgeIllegalRuntimeException

Exceptions2.java

```TypeScript
package com.zbhgis.exceptions;

public class Exceptions2 {
    public static void main(String[] args) {
        try {
            saveAge(160);
            System.out.println("底层执行成功");
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("底层出现了bug");
        }
    }

    private static void saveAge(int age) {
        if(age > 0 & age < 150){
            System.out.println("年龄被成功保存：" +age);
        } else {
            throw new AgeIllegalRuntimeException("age " + age + " is illegal");
        }
    }
}
```

打印结果

```Plain
com.zbhgis.exceptions.AgeIllegalRuntimeException: age 160 is illegal
        at com.zbhgis.exceptions.Exceptions2.saveAge(Exceptions2.java:18)
        at com.zbhgis.exceptions.Exceptions2.main(Exceptions2.java:6)
底层出现了bug
```

## 自定义编译时异常

定义一个异常类继承Exception，重写构造器，通过throw new 异常类() 来创建异常对象并抛出。IDEA反馈较强。

Exceptions3.java

```Java
package com.zbhgis.exceptions;

public class Exceptions3 {
    public static void main(String[] args) {
        try {
            saveAge(161);
            System.out.println("底层执行成功");
        } catch (AgeIllegalException e) {
            e.printStackTrace();
            System.out.println("底层出现了bug");
        }

    }

    private static void saveAge(int age) throws AgeIllegalException{
        if(age > 0 & age < 150){
            System.out.println("年龄被成功保存：" +age);
        } else {
            throw new AgeIllegalException("age " + age + " is illegal");
        }
    }
}
```

打印结果

```Plain
com.zbhgis.exceptions.AgeIllegalException: age 161 is illegal
        at com.zbhgis.exceptions.Exceptions3.saveAge(Exceptions3.java:19)
        at com.zbhgis.exceptions.Exceptions3.main(Exceptions3.java:6)
底层出现了bug
```

# 异常的处理

1.捕获异常，记录异常并响应合适的信息给用户

Exceptions4.java

```Java
package com.zbhgis.exceptions;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.InputStream;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Exceptions4 {
    public static void main(String[] args){
        // 以下也可以直接抛出Exception，不需要具体的异常
        try {
            test1();
        } catch (ParseException e) {
            System.out.println("解析的时间有问题");
            e.printStackTrace();
        } catch (FileNotFoundException e) {
            System.out.println("要找的文件不存在");
            e.printStackTrace();
        }
    }

    private static void test1() throws ParseException, FileNotFoundException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        // Date d = sdf.parse("2025");
        // System.out.println(d);
        // 此处报错：
        /*
        java.text.ParseException: Unparseable date: "2025"
            at java.base/java.text.DateFormat.parse(DateFormat.java:399)
            at com.zbhgis.exceptions.Exceptions4.test1(Exceptions4.java:26)
            at com.zbhgis.exceptions.Exceptions4.main(Exceptions4.java:14)
        解析的时间有问题
         */

        Date d2 = sdf.parse("2025-12-11 03:03:03");
        System.out.println(d2);

        test2();
    }

    private static void test2() throws FileNotFoundException {
        InputStream is = new FileInputStream("D:/test.png");
    }
}
```

打印结果

```Plain
要找的文件不存在
java.io.FileNotFoundException: D:\test.png (系统找不到指定的文件。)
        at java.base/java.io.FileInputStream.open0(Native Method)
        at java.base/java.io.FileInputStream.open(FileInputStream.java:216)
        at java.base/java.io.FileInputStream.<init>(FileInputStream.java:157)
        at java.base/java.io.FileInputStream.<init>(FileInputStream.java:111)
        at com.zbhgis.exceptions.Exceptions4.test2(Exceptions4.java:44)
        at com.zbhgis.exceptions.Exceptions4.test1(Exceptions4.java:40)
        at com.zbhgis.exceptions.Exceptions4.main(Exceptions4.java:14)
```

或者将上述代码的操作进行简化

Exceptions5.java

```Java
package com.zbhgis.exceptions;

import java.io.FileInputStream;
import java.io.InputStream;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Exceptions5 {
    public static void main(String[] args){
        // 以下也可以直接抛出Exception，不需要具体的异常
        try {
            test1();
        } catch (Exception e) {
            System.out.println("操作有问题");
            e.printStackTrace();
        }
    }

    private static void test1() throws Exception {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        // Date d = sdf.parse("2025");
        // System.out.println(d);
        // 此处报错：
        /*
        操作有问题
        java.text.ParseException: Unparseable date: "2025"
            at java.base/java.text.DateFormat.parse(DateFormat.java:399)
            at com.zbhgis.exceptions.Exceptions5.test1(Exceptions5.java:21)
            at com.zbhgis.exceptions.Exceptions5.main(Exceptions5.java:12)
         */

        Date d2 = sdf.parse("2025-12-11 03:03:03");
        System.out.println(d2);

        test2();
    }

    private static void test2() throws Exception {
        InputStream is = new FileInputStream("D:/test.png");
    }
}
```

打印结果

```Plain
Thu Dec 11 03:03:03 CST 2025
操作有问题
java.io.FileNotFoundException: D:\test.png (系统找不到指定的文件。)
        at java.base/java.io.FileInputStream.open0(Native Method)
        at java.base/java.io.FileInputStream.open(FileInputStream.java:216)
        at java.base/java.io.FileInputStream.<init>(FileInputStream.java:157)
        at java.base/java.io.FileInputStream.<init>(FileInputStream.java:111)
        at com.zbhgis.exceptions.Exceptions5.test2(Exceptions5.java:41)
        at com.zbhgis.exceptions.Exceptions5.test1(Exceptions5.java:37)
        at com.zbhgis.exceptions.Exceptions5.main(Exceptions5.java:14)
```

2.捕获异常，尝试重新修复

Exceptions6.java

```Java
package com.zbhgis.exceptions;

import java.util.Scanner;

public class Exceptions6 {
    public static void main(String[] args) {
        while (true) {
            try {
                System.out.println(getMoney());
                break;
            } catch (Exception e) {
                System.out.println("请输入合法的数字");
            }
        }

    }

    private static double getMoney() {
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("请输入合适的价格");
            double money = sc.nextDouble();
            if (money >= 0) {
                return money;
            } else {
                System.out.println("输入价格不合适");
            }
        }
    }
}
```

打印结果

```Plain
请输入合适的价格
-2
输入价格不合适
请输入合适的价格
61f
请输入合法的数字
请输入合适的价格
564s
请输入合法的数字
请输入合适的价格
4
4.0
```

# 总结

1.异常可以使程序更加稳健

2.处理异常时可以选择直接抛出Exception，减少代码量