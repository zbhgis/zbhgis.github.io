
# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站[黑马程序员](https://space.bilibili.com/37974444)的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m/?vd_source=3b69b85b41f42a9e26b3a8a195228a36

# 内容概览

1.本文内容包括String的创建，常用API，特点以及一些应用案例。

2.笔记对应视频77-79节

# 更新记录

无

# String的创建

## 1.直接创建

通过直接双引号得到字符串对象，即创建的字符串变量是对象。但直接打印出来的其内容而不是地址，因为String类的toString方法被重写了。

## 2.String方法

通过new String类来创建字符串对象，并调用构造器初始化字符串。第一种和第二种不常用。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052132443.png)

```Java
package com.zbhgis.string;

public class StringDemo0 {
    public static void main(String[] args) {
        // 直接创建
        String name = "test1";
        System.out.println(name);

        // new String类创建，四种
        String rs1 = new String();
        System.out.println(rs1);

        String rs2 = new String("test123");
        System.out.println(rs2);

        char[] chars = {'t', 'e', '1', '2'};
        String rs3 = new String(chars);
        System.out.println(rs3);

        byte[] bytes = {1, 127, 66};
        String rs4 = new String(bytes);
        System.out.println(rs4);
    }
}
```

打印结果

```Plain
test1

test123
te12
ABC
```

# String常用API

一些字符串处理的常用方法，了解即可。

https://docs.oracle.com/en/java/javase/17/docs/api/index.html

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052133502.png)

## 注意点

1.String中的length()为方法，需要加括号；数组中的length为值，不需要加括号

2.String中的substring方法中如果只传入一个参数，识别是beginIndex；

3.String中的toCharArray()和split()方法返回结果为数组，不可以直接打印，得遍历；或者使用Array.toString()方法转为字符串后打印

4.String中的substring()方法包前不包后；

5.String中的equalsIgnoreCase()方法，使用在含有中文的字符串也可以。

6.打印字符串长度，中文一个汉字算一个字符长度

```Java
package com.zbhgis.string;

import java.util.Arrays;

public class StringDemo1 {
    public static void main(String[] args) {
        String s1 = "编程语言Java";
        System.out.println(s1.length());
        
        char c = s1.charAt(1);
        System.out.println(c);

        char[] chars = s1.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            System.out.println(chars[i]);
        }

        String s2 = "编程语言java";
        String s3 = new String("编程语言Java");

        System.out.println(s1 == "编程语言Java");
        System.out.println(s1 == s3);
        System.out.println(s1.equals(s2));
        System.out.println(s1.equalsIgnoreCase(s2));
        System.out.println(s1.substring(0, 2));
        System.out.println(s1.substring(1));
        System.out.println(s1.replace("编程语言", "C++"));
        System.out.println(s1.contains("编程语言"));
        System.out.println(s1.contains("java"));
        System.out.println(s1.startsWith("编程语言"));
        System.out.println(s1.startsWith("Java"));
        System.out.println(Arrays.toString(s1.split("语言")));
    }
}
```

打印结果

```Plain
8
程
编
程
语
言
J
a
v
a
false
false
true
编程
程语言Java
C++Java
true
false
true
false
[编程, Java]
```

# String本身的特点

## 1.String的对象是不可变字符串对象

如果直接修改字符串对象，那么本质上是产生了新的字符串对象，变量也指向了新的字符串对象。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052133722.png)

## 2.双引号创建的字符串对象存储在常量池中，且内容相同只能存储一份

通过双引号直接创建的字符串对象，会在堆内存中的字符串常量池存储。即双引号创建的字符串对象被视为固定常量赋值给变量，如果再通过双引号创建一个相同的字符串对象，那么存储的位置相同，其地址也相同。用于节约内存。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052133664.png)

## 3.new String创建的字符串对象存储在堆内存中，内容相同但地址不同

通过new String创建的字符串对象，每new一次都会产生一个新的对象放在堆内存中。即new String创建的对象每次即使内容相同，但是由于开辟了新的内存，因此其地址不同。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052132835.png)

```Java
package com.zbhgis.string;

public class StringDemo2 {
    public static void main(String[] args) {
        // 1.String的对象是不可变字符串对象
        String s1 = "test";
        String res1 = s1 + "123";
        String res2 = res1 + "!";
        System.out.println(s1);
        System.out.println(res1);
        System.out.println(res2);

        System.out.println();
        
        // 2.双引号创建的字符串对象存储在常量池中，且内容相同只能存储一份
        // 3.new String创建的字符串对象存储在堆内存中，内容相同但地址不同
        String s2 = "test";
        String s3 = new String("test");
        String s4 = new String("test");
        System.out.println(s1 == s2);
        System.out.println(s1 == s3);
        System.out.println(s1 == s4);
    }
}
```

## 思考

### 创建对象的个数

s2先创建了一个常量存储到堆内存的常量池中，然后new String方法又创建了一个内容相同但地址不同的字符串对象到堆内存中。之后的s1通过双引号生产字符串对象相当于从堆内存的常量池中直接获取到“abc”对象，因此没有创建新的字符串对象。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052132449.png)

### 字符串是否相同

在Test3中，s3是通过s2与“c”进行运算得到，结果开辟在新的堆内存中，而s1通过双引号创建存储在常量池中，因此s3与s1地址不同。

在Test4中，s2是通过“a” “b” “c”三者相加得到，但是由于三者都是字面量（常量），因此java程序在编译性，识别到运算的三者都是常量，会直接转为"abc"，提高程序性能，因此相当于s2 = "abc"，相当于只创建了一个字符串变量在堆内存的常量池中。而上面的s1执行后已经存储了一份"abc"在常量池，依次s2直接从常量池中获取到"abc"。因此s2与s1地址相同。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052134739.png)

```Java
package com.zbhgis.string;

public class StringDemo3 {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "a" + "b" + "c";
        String s3 = s2;
        // 涉及到运算，结果需要开辟新内存
        String s4 = s2 + "";

        // 内容相同，地址也相同
        System.out.println(s1 == s2);
        System.out.println(s1 == s3);
        System.out.println(s2 == s3);

        // 内容相同，地址不同
        System.out.println(s1 == s4);
        System.out.println(s1.equals(s4));
    }
}
```

打印结果

```Plain
true
true
true
false
true
```

# String的应用案例

设计一个系统模拟登录界面，检查用户提供的账户与密码是否相同。

```Java
package com.zbhgis.string;

import java.util.Scanner;

public class StringDemo4 {
    public static void main(String[] args) {
        for (int i = 0; i < 3; i++) {
            Scanner sc = new Scanner(System.in);
            System.out.println("请您输入登录名称");
            String loginName = sc.next();
            System.out.println("请您输入登录密码");
            String passWord = sc.next();

            boolean res = login(loginName, passWord);
            if (res) {
                System.out.println("恭喜您，欢迎进入系统");
            } else {
                System.out.println("登录名或密码错误，请确认");
            }
        }

    }

    public static boolean login(String loginName, String passWord) {
        String okLoginName = "test";
        String okPassWord = "123456";
        if (okLoginName.equals(loginName) && okPassWord.equals(passWord)) {
            System.out.println("账户密码正确");
            return true;
        } else {
            System.out.println("账户或密码错误");
            return false;
        }
    }
}
```

# 总结

1.String常用api需要熟悉；

2.String本身是对象，进行比较时候是比较地址。==比较的是地址；equals()比较的是内容。

3.String创建的字符串对象通过双引号创建时，其值只在堆内存的常量池中存储一份；通过new String方法创建时，其值为每new一次都会在堆内存中开辟新内存。