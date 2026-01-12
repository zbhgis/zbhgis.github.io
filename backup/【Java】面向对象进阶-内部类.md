

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括成员内部类，静态内部类，局部内部类，以及匿名内部类。

2.笔记对应视频111-112节

# 更新记录

无

# 内部类

如果一个类定义在另一个类的内部，这个类就是内部类

包括成员内部类，静态内部类，局部内部类，匿名内部类

## 成员内部类

类中成员

public class 外部类名{

public class 内部类名{

}

}

创建其对象

外部类名.内部类名 对象名 = new 外部类().new 内部类();

1.可以直接访问外部类的实例成员和静态成员。

2.拿到当前外部类对象，    外部类名.this

Outer.java

```Java
package com.zbhgis.object7;

public class Outer {
    public static String a;
    private int age = 99;

    public void test2() {
        System.out.println(age);
        System.out.println(a);
    }

    public class Inner {
        public static String schoolName; // JDK16开始支持
        private String name;
        private int age = 88;

        public void test() {
            System.out.println(age);
            System.out.println(a);

            int age = 66;
            System.out.println(age);
            System.out.println(this.age);
            System.out.println(Outer.this.age);
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
}
```

Obeject7Demo1.java

```Java
package com.zbhgis.object7;

public class Object7Demo1 {
    public static void main(String[] args) {
        Outer.Inner in = new Outer().new Inner();
        in.test();
    }
}
```

打印结果

```Plain
88
null
66
88
99
```

## 静态内部类

有static类修饰的内部类，属于外部类自己持有。

public class 外部类名{

public static class 内部类名{

}

}

创建其对象

外部类名.内部类名 对象名 = new 外部类.内部类();

可以直接访问外部类的静态成员，不可以直接访问外部类的实例成员。

Outer2.java

```Java
package com.zbhgis.object7;

public class Outer2 {
    public static String schoolName;
    private int age;

    public static void test() {

    }

    public static void test2() {
        System.out.println(schoolName);
        // System.out.println(age); // 报错
    }

    public static class Inner2 {
        public static int a;
        private String name;

        public void test() {
            System.out.println(schoolName);
            // System.out.println(age); // 报错
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
}
```

Object7Demo2.java

```Java
package com.zbhgis.object7;

public class Object7Demo2 {
    public static void main(String[] args) {
        Outer2.Inner2 in2 = new Outer2.Inner2();
        in2.test();
    }
}
```

打印结果

```Plain
null
```

## 局部内部类

局部内部类是定义在在方法中、代码块中、构造器等执行体中。

了解即可。

## 匿名内部类

特殊的局部内部类，通常作为一个参数传输给方法；

本质就是一个子类，并会立即创建出一个子类对象

New 类或接口(参数值){

类体(一般是方法重写);

}

Object7Demo3.java

```Java
package com.zbhgis.object7;

interface Swimming {
    void swim();
}

public class Object7Demo3 {
    public static void main(String[] args) {
        go(new Swimming() {
            @Override
            public void swim() {
                System.out.println("狗游得快");
            }
        });
    }

    public static void go(Swimming s) {
        System.out.println("开始");
        s.swim();
    }
}
```

打印结果

```Plain
开始
狗游得快
```

# 总结

1.内部类在另一个类内部

2.匿名内部类本质就是一个子类，并会立即创建出一个子类对象

3.匿名内部类通常作为方法的函数