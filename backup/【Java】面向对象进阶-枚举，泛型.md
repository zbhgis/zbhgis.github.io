

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括枚举和泛型各自的概念、作用

2.笔记对应视频113-115节

# 更新记录

无

# 枚举

## 枚举的概念与特点

枚举是一种特殊类。

格式：

修饰符 enum 枚举类名{

名称1, 名称2, ...;

其他成员...;

}

注意：

枚举类的第一行，只能写一些合法的标识符（名称），多个名称用逗号隔开；

这个名称，本质是常量，每个常量都会记住枚举类的一个对象。

特点：

1.枚举类的第一行只能罗列一些名称，这些名称都是常量，并且每个常量记住的都是枚举类的一个对象。

2.枚举类的构造器都是私有的（写不写都只能是私有的），因此，枚举类对外不能创建对象。

3.枚举都是最终类，不可以被继承。

4.枚举类中，从第二行开始，可以定义类的其他各种成员。

5.编译器为枚举类新增了几个方法，并且枚举类都是继承：java.lang.Enum类的，从enum类也会继承到一些方法。

## 抽象枚举

在枚举类中定义一个或多个抽象方法，然后让每个枚举常量实例都必须实现这个抽象方法。

本质上是利用了枚举常量可以携带代码块（从而创建匿名内部类并重写方法）的特性。

A.java

```Java
package com.zbhgis.object8;

public enum A {
    // 枚举类第一行必须罗列的是枚举对象的名字
    X, Y, Z;

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

B.java

```Java
package com.zbhgis.object8;

// 抽象枚举
public enum B {
    X(){
        @Override
        public void go(){

        }
    }, Y("明"){
        @Override
        public void go(){
            System.out.println(getName() + "在跑");
        }
    };
    public abstract void go();

    // 默认私有
    B() {
    }

    B(String name) {
        this.name = name;
    }

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

Object8Demo1.java

```Java
package com.zbhgis.object8;

public class Object8Demo1 {
    public static void main(String[] args) {
        A a1 = A.X;
        System.out.println(a1);
        // 枚举类的构造器是私有的，不能对外创建对象
        // A a = new A();

        // 枚举类的第一行都是常量，记住的是枚举类的对象
        A a2 = A.Y;

        // 枚举类提供一些额外的API
        A[] as = A.values();
        for (int i = 0; i < as.length; i++) {
            System.out.print(as[i]);
        }
        System.out.println();
        A a3 = A.valueOf("Z");
        System.out.println(a3.name());
        System.out.println(a3.ordinal());

        System.out.println("------------");
        B y = B.Y;
        y.go();

    }
}
```

打印结果

```Plain
X
XYZ
Z
2
------------
明在跑
```

## 枚举实现单例设计模式

```Java
package com.zbhgis.object8;

public enum C {
    X; // 单例
}
```

## 枚举的作用

表示一组信息，然后作为参数进行传输。

参数值不受约束。

Object8Demo1.java

```Java
package com.zbhgis.object8;

public class Object8Demo2 {
    public static void main(String[] args) {
        check(Constant.GIRL);
    }

    public static void check(Constant sex){
        switch (sex){
            case BOY:
                System.out.println("男");
                break;
            case GIRL:
                System.out.println("女");
                break;
        }
    }
}
```

Constant.java

```Java
package com.zbhgis.object8;

public enum Constant {
    BOY, GIRL;
}
```

打印结果

```Plain
女
```

# 泛型

定义类、接口、方法时，同时声明了一个或者多个类型变量（如：<E>），称为泛型类、泛型接口，泛型方法、它们统称为泛型。

可参考ArrayList

## 泛型的认识

作用：避免强制类型转换，及其可能出现的异常。

本质：把具体的数据类型作为参数传给类型变量。

Object9Demo1.java

```Java
package com.zbhgis.object9;

import java.util.ArrayList;

public class Object9Demo1 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("java1");
        list.add("java2");
        list.add("java3");

        for (int i = 0; i < list.size(); i++) {
            // 由于提前设置好了变量类型，因此能自动识别
            String e = list.get(i);
            System.out.println(e);
        }
    }
}
```

打印结果

```Plain
java1
java2
java3
```

## 泛型类

修饰符 class 类名<类型变量，类型变量，...> {

}

public class ArrayList<E, T>{

}

MyArrayList.java

```Java
package com.zbhgis.object9;

public class MyArrayList<E> {
    private Object[] arr = new Object[10];
    private int size;

    public boolean add(E e){
        arr[size++] = e;
        return true;
    }

    public E get(int index){
        return (E) arr[index];
    }
}
```

MyArrayList2.java

```Java
package com.zbhgis.object9;

public class MyArrayList2<E, T> {
    public void put(E e, T t){

    }
}
```

MyArrayList3.java

```Java
package com.zbhgis.object9;

public class MyArrayList3<E extends Animal> {
}
```

Animal

```Java
package com.zbhgis.object9;

public class Animal {
}
```

Cat

```Java
package com.zbhgis.object9;

public class Cat extends Animal {
}
```

Dog

```Java
package com.zbhgis.object9;

public class Dog {
}
```

Object9Demo2.java

```TypeScript
package com.zbhgis.object9;

public class Object9Demo2 {
    public static void main(String[] args) {
        MyArrayList<String> list = new MyArrayList<>();
        list.add("java1");
        list.add("java2");
        String ele = list.get(1);
        System.out.println(ele);

        MyArrayList2<Cat, String> list2 = new MyArrayList2<>();
        MyArrayList3<Cat> list3 = new MyArrayList3<>();
        MyArrayList3<Animal> list33 = new MyArrayList3<>();
        // 会报错，因此Dog没有继承Animal
        // MyArrayList3<Dog> list33 = new MyArrayList3<>();
    }

}
```

打印结果

```Plain
java2
```

## 泛型接口

修饰符 interface 接口名<类型变量，类型变量，...>{

}

public interface A<E>{

}

Data.java

```Java
package com.zbhgis.object9;

import java.util.ArrayList;

public interface Data<T> {
    void add(T t);
    ArrayList<T> getByName(String name);

}
```

Student.java

```Java
package com.zbhgis.object9;

public class Student {
}
```

Teacher.java

```Java
package com.zbhgis.object9;

public class Teacher {
}
```

StudentData.java

```Java
package com.zbhgis.object9;

import java.util.ArrayList;

public class StudentData implements Data<Student>{

    @Override
    public void add(Student student) {

    }

    @Override
    public ArrayList<Student> getByName(String name) {
        return null;
    }
}
```

TeacherData.java

```Java
package com.zbhgis.object9;

import java.util.ArrayList;

public class TeacherData implements Data<Teacher>{
    @Override
    public void add(Teacher teacher) {

    }

    @Override
    public ArrayList<Teacher> getByName(String name) {
        return null;
    }
}
```

## 泛型方法

修饰符<类型变量, 类型变量, ...> 返回值类型 方法名(形参列表){

}

public static <T> void test(T t){

}

通配符

就是“？”，可以在“使用泛型”的时候代表一切类型；E T K V是在定义泛型的时候使用

泛型的上下限

? Extends Car    ?能接收的必须是Car或者其子类

？super Car      ?能接收的必须是Car或者其父类

Car.java

```Java
package com.zbhgis.object9;

public class Car {
}
```

BENZ.java

```Java
package com.zbhgis.object9;

public class BENZ extends Car{
}
```

BMW.java

```Java
package com.zbhgis.object9;

public class BMW extends Car{
}
```

Object9Demo3.java

```Java
package com.zbhgis.object9;

import java.util.ArrayList;

public class Object9Demo3 {
    public static void main(String[] args) {
        String rs = test("java");
        System.out.println(rs);

        Dog d = test(new Dog());
        System.out.println(d);

        ArrayList<Car> cars = new ArrayList<>();
        cars.add(new BMW());
        cars.add(new BENZ());
        go(cars);

        ArrayList<BENZ> benzs = new ArrayList<>();
        benzs.add(new BENZ());
        benzs.add(new BENZ());
        go(benzs);

        ArrayList<BMW> bmws = new ArrayList<>();
        bmws.add(new BMW());
        bmws.add(new BMW());
        go(bmws);
    }

    // 或者使用通配符
    // public static void go(ArrayList<? extends Car> cars)
    public static <T extends Car> void go(ArrayList<T> cars) {

    }

    public static <T> T test(T t) {
        return t;
    }
}
```

泛型的注意事项

泛型是工作在编译阶段的，一旦程序编译成class文件，class文件中就不存在泛型了，这就是泛型擦除。

泛型不支持基本数据类型（比如int或double），只能支持对象类型（引用数据类型，比如Integer或Double）。

# 总结

1.枚举类对外不能创建对象，且不能被继承

2.泛型就是把具体的数据类型作为参数传给类型变量。