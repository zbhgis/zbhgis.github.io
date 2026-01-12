

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括final关键字的使用，常量，抽象类的概念和特点，抽象类的好处与案例，以及抽象类的应用

2.笔记对应视频104节

# 更新记录

无

# final

final关键字是最终的意思，可以修饰（类、方法、变量）

修饰类：该类被称为最终类，特点是不能被继承了。

修饰方法：该方法被称为最终方法，特点是不能被重写了。

修饰变量：该变量只能被赋值一次。

注意点：

final修饰基本类型的变量，变量存储的数据不能被改变。

final修饰引用类型的变量，变量存储的地址不能被改变，但地址所指向对象的内容是可以被改变的。

Object5Demo1.java

```Java
package com.zbhgis.object5;

public class Object5Demo1 {
    public static final String SCHOOL_NAME = "黑马";
    private final String name = "1"; // 这种用法没有意义

    public static void main(String[] args) {

        // 3. final可以修饰变量：有且仅能赋值一次
        final int a;
        a = 12;
        // a = 13; // 第二次赋值报错
        final double r = 3.14;
        // r = 0.1; // 第二次赋值报错

        // SCHOOL_NAME = "1"; // 第二次赋值报错
    }

    public static void buy(final double z) {
        // z = 0.1 // 第二次赋值报错
    }
}

// 1. final修饰类，类不能被继承了
final class A {
}
// class B extends A{
//
// }

// 2. final修饰方法，方法不能被重写了
class C {
    public final void test() {
    }
}

class D extends C {
    // @Override
    // public void test(){
    //
    // }
}
```

# 常量

使用了static final修饰的成员变量就被称为常量；

作用：通常用于记录系统的配置信息。

命名规范：建议使用大写英文单词，多个单词使用下划线连接起来。

好处：可读性强；性能好：常量的地方全部会被替换成其记住的字面量，这样可以保证使用常量和直接用字面量的性能是一样的。

Object5Demo2.java

```Java
package com.zbhgis.object5;

public class Object5Demo2 {
    public static final String COUNTRY_NAME = "中国";

    public static void main(String[] args) {
        System.out.println(COUNTRY_NAME);
        System.out.println(COUNTRY_NAME);
        System.out.println(COUNTRY_NAME);
    }
}
```

打印结果

```Plain
中国
中国
中国
```

# 抽象类

## 抽象类的概念与特点

概念：

被abstract关键字修饰的类就是抽象类；修饰方法就是抽象方法

修饰符 abstract class 类名{

修饰符 abstract 返回值类型 方法名称(形参列表);

}

特点：

1.抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类。

2.类该有的成员（成员变量、方法、构造器）抽象类都可以有。

3.抽象类最主要的特点：抽象类不能创建对象，仅作为一种特殊的父类，让子类继承并实现。

4.一个类继承抽象类，必须重写完抽象类的全部抽象方法，否则这个类也必须定义成抽象类。

Object5Demo3.java

```Java
package com.zbhgis.object5;

public class Object5Demo3 {
    public static void main(String[] args) {
        System.out.println();
        // E e = new E(); // 抽象类不能创建对象
    }
}
```

E.java

```Java
package com.zbhgis.object5;

public abstract class E {
    public static String schoolName;
    private String name;

    public E() {
    }

    public E(String name) {
        this.name = name;
    }

    public abstract void run();

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

F.java

```Java
package com.zbhgis.object5;

// 一个类继承了抽象类，要么自己是抽象类，要么必须重写完父类的所有抽象方法
// 1. 自己为抽象类
// public abstract class F extends E{
// }

// 2. 自己重写所有抽象方法
public class F extends E {
    @Override
    public void run() {

    }
}
```

## 抽象类的好处与案例

更好地支持多态

Object5Demo4.java

```Java
package com.zbhgis.object5;

public class Object5Demo4 {
    public static void main(String[] args) {
        Animal animal = new Cat();
        animal.setName("猫");
        animal.cry();
    }
}
```

Animal.java

```Java
package com.zbhgis.object5;

public abstract class Animal {
    private String name;

    public abstract void cry();

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

Cat.java

```Java
package com.zbhgis.object5;

public class Cat extends Animal {
    @Override
    public void cry() {
        System.out.println(getName() + "喵喵");
    }
}
```

Dog.java

```Java
package com.zbhgis.object5;

public class Dog extends Animal {
    @Override
    public void cry() {
        System.out.println(getName() + "汪汪");
    }
}
```

打印结果

```Java
猫喵喵
```

## 抽象类的应用

经常用来设计模板方法，一种设计模式

即定义一个抽象类，在里面定义2个方法，一个是模板方法；一个是抽象方法（具体交给子类实现）

Object5Demo5.java

```Java
package com.zbhgis.object5;

public class Object5Demo5 {
    public static void main(String[] args) {
        Teacher t = new Teacher();
        t.speak();
        System.out.println();
        Student s = new Student();
        s.speak();
    }
}
```

People.java

```Java
package com.zbhgis.object5;

public abstract class People {
    // 模板方法，使用final修饰避免被子类重写
    public final void speak() {
        System.out.println("报了四六级");
        // 抽象方法
        speakMain();
        System.out.println("又捐款一笔");
    }

    public abstract void speakMain();
}
```

Teacher.java

```Java
package com.zbhgis.object5;

public class Teacher extends People {
    @Override
    public void speakMain() {
        System.out.println("十二月了没复习");
    }
}
```

Student.java

```Java
package com.zbhgis.object5;

public class Student extends People {
    @Override
    public void speakMain() {
        System.out.println("白天考试晚上醒");
    }
}
```

打印结果

```Java
报了四六级
十二月了没复习
又捐款一笔

报了四六级
白天考试晚上醒
又捐款一笔
```

# 总结

1.final修饰的变量只能赋值一次，修饰的类不可被继承

2.final修饰的引用类型变量，地址不可二次赋值，但是其中的内容元素可以多次赋值。

3.使用了static final修饰的成员变量就被称为常量

4.抽象方法不能写方法体

5.抽象类可以有普通类该有的一些成员

6.抽象类不能创建对象，只能被继承

7.一个类继承抽象类必须重写完抽象类的全部抽象方法，否则这个类也必须定义为抽象类

8.模板方法使用final修饰可以避免被子类重写，更加安全