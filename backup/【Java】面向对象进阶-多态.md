

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括多态的概念与特点，多态的前提，以及多态的特点

2.笔记对应视频105-107节

# 更新记录

无

# 多态的概念

多态是在继承/实现情况下的一种现象，表现为：对象多态、行为多态。

例如：

People p1 = new Student();

p1.run();

People p2 = new Student();

p2.run();

# 多态的前提

有继承/实现关系；存在父类引用子类对象；存在方法重写。

！多态是对象、行为的多态，Java中的属性(成员变量)不谈多态。

Object4Demo1.java

```Java
package com.zbhgis.object4;

public class Object4Demo1 {
    public static void main(String[] args) {
        People p1 = new Student();
        p1.run(); // 编译看左边，运行看右边。
        System.out.println(p1.name); // 对于变量，编译看左边，运行看左边。

        People p2 = new Teacher();
        p2.run();
        System.out.println(p2.name);
    }
}

class People{
    public String name = "People";
    public void run(){
        System.out.println("People run");
    }
}

class Student extends People{
    public String name = "Student";

    @Override
    public void run(){
        System.out.println("Student run");
    }
}

class Teacher extends People{
    public String name = "Teacher";

    @Override
    public void run(){
        System.out.println("Teacher run");
    }
}
```

打印结果

```Plain
Student run
People
Teacher run
People
```

# 多态的特点

优点：

在多态形式下，右边对象是解耦合的，更便于扩展和维护。

定义方法时，使用父类类型的形参，可以接收一切子类对象，扩展性更强、更便利。

缺点及其解决：

多态不能使用子类的独有功能。为了解决这个问题，可以使用类型转换。

自动类型转换：父类 变量名 = new 子类();

强制类型转换：子类 变量名 = (子类)父类变量;

存在继承/实现关系就可以在编译阶段进行强制类型转换，编译阶段不会报错。运行时，如果发现对象的真实类型与强转后的类型不同，就会报类型转换异常（ClassCastException）的错误出来（可以使用instanceof关键字判断避免抛出异常）。

Object4Demo2.java

```Java
package com.zbhgis.object4;

import java.rmi.StubNotFoundException;

public class Object4Demo2 {
    public static void main(String[] args) {
        // 解耦合，右边对象可以随时切换
        Person p1 = new Family();
        p1.run();
        // p1.live(); // 多态不能使用子类的独有功能

        // 可以使用父类类型的变量作为形参，可以接收一切子类对象
        Friend f1 = new Friend();
        go(f1);

        Family f2 = new Family();
        go(f2);

    }

    public static void go(Person p){

    }
}


class Person{
    public String name = "Person";
    public void run(){
        System.out.println("Person run");
    }
}

class Friend extends Person{
    public String name = "Friend";

    @Override
    public void run(){
        System.out.println("Friend run");
    }

    public void play(){
        System.out.println("play");
    }
}

class Family extends Person{
    public String name = "Family";

    @Override
    public void run(){
        System.out.println("Family run");
    }

    public void live(){
        System.out.println("live");
    }
}
```

打印结果

```Plain
Family run
live

live

Friend run
play
Family run
live
```

# 总结

1.多态是对象、行为的多态，Java中的属性(成员变量)不谈多态。

2.多态不能使用子类的独有功能，需要加上类型转换

3.类型转换要转换对，不然会抛出异常

4.可以结合instanceof关键字识别对象的类型