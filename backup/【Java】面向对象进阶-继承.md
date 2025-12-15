

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括继承的概念和特点，权限修饰符，单继承，方法重写，子类构造器，以及兄弟构造器。

2.笔记对应视频99-103节

# 更新记录

无

# 继承的定义与特点

继承就是用extends关键字，让一个类和另一个类建立起一种父子关系。

子类可以继承父类非私有的成员。对象能直接访问什么成员，是由子父类这多张设计图共同决定的，这多张设计图对外暴露了什么成员，对象就可以访问什么成员。

其过程与之前类似，就是在访问类B时，如果涉及到了A中的变量和方法，会进一步访问类A。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512091741843.png)

A.java

```Java
package com.zbhgis.object3;

public class A {
    public int i;
    private int j;

    public void print1() {
        System.out.println("print1");
    }

    private void print2() {
        System.out.println("print2");
    }
}
```

B.java

```Java
package com.zbhgis.object3;

public class B extends A {
    public int k;

    public void print3() {
        System.out.println("print3");
        System.out.println(i);
        print1();
    }
}
```

Object3Demo1.java

```Java
package com.zbhgis.object3;

public class Object3Demo1 {
    public static void main(String[] args) {
        B b = new B();
        System.out.println(b.i);
        // 不可调用
        // System.out.println(b.j);
        System.out.println(b.k);
        b.print1();
        // 不可调用
        // b.print2();
        b.print3();
    }
}
```

打印结果

```Plain
0
0
print1
print3
0
print1
```

继承的好处是可以提高代码的复用性

People.java

```Java
package com.zbhgis.object3;

public class People {
    private String name;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

Teacher.java

```Java
package com.zbhgis.object3;

public class Teacher extends People {
    private String skill;

    public String getSkill() {
        return this.skill;
    }

    public void setSkill(String skill) {
        this.skill = skill;
    }

    public void printInfo() {
        System.out.println(getName() + "具备技能：" + skill);
    }
}
```

Object3Demo2.java

```Java
package com.zbhgis.object3;

public class Object3Demo2 {
    public static void main(String[] args) {
        Teacher t = new Teacher();
        t.setName("山");
        t.setSkill("MySQL");
        System.out.println(t.getName());
        System.out.println(t.getSkill());
        t.printInfo();
    }
}
```

打印结果

```Plain
山
MySQL
山具备技能：MySQL
```

# 继承的注意事项

## 权限修饰符

就是是用来限制类中的成员（成员变量、成员方法、构造器、代码块..）能够被访问的范围。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512091741606.png)

## 单继承

Java是单继承，即一个类只能继承一个直接父类，不支持多继承，但能多层继承。Object类是Java中所有类的祖宗。

## 方法重写

使用Override注解，检查我们方法重写的格式是否正确，代码可读性也会更好。

子类重写父类方法时，访问权限必须大于或者等于父类该方法的权限（public>protected>缺省）。

重写的方法返回值类型，必须与被重写方法的返回值类型一样，或者范围更小。

私有方法、静态方法不能被重写。

Student.java

```Java
package com.zbhgis.object3;

public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
    
    @Override
    public String toString() {
        return "Student{name=" + name + ",age=" + age + "}";
    }
}
```

Object3Demo3.java

```Java
package com.zbhgis.object3;

public class Object3Demo3 {
    public static void main(String[] args) {
        Student s = new Student("小明", 20);
        System.out.println(s);
    }
}
```

打印结果

```Plain
Student{name=小明,age=20}
```

## 访问的就近原则

1.在子类方法中访问其他成员，是按照就近原则的。

2.如果子父类中，出现了重名的成员，会优先使用子类的；此时通过super关键字可以访问父类成员。

X.java

```Java
package com.zbhgis.object3;

public class X {
    String name = "父类名称";

    public void print1() {
        System.out.println("父类的print1");
    }
}
```

Y.java

```Java
package com.zbhgis.object3;

public class Y extends X {
    String name = "子类名称";

    public void showName() {
        String name = "局部名称";
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }

    @Override
    public void print1() {
        System.out.println("子类的print1");
    }

    public void showMethod() {
        print1();
        super.print1();
    }
}
```

Object3Demo4.java

```Java
package com.zbhgis.object3;

public class Object3Demo4 {
    public static void main(String[] args) {
        Y y = new Y();
        y.showName();
        System.out.println();
        y.showMethod();
    }
}
```

打印结果

```Plain
局部名称
子类名称
父类名称

子类的print1
父类的print1
```

## 子类构造器

### 子类构造器的概念和特点

子类的全部构造器都会先调用父类的构造器，再执行自己。

默认情况下，子类全部构造器的第一行代码都是super()（写不写都有），它会调用父类的无参数构造器。

如果父类没有无参数构造器，则我们必须在子类构造器的第一行手写super(..)，指定去调用父类的有参数构造器。

Object3Demo5.java

```Java
package com.zbhgis.object3;

class C {
    public C() {
        System.out.println("父类无参构造器");
    }

    public C(String name, int age) {
        System.out.println("父类有参构造器");
    }
}

class D extends C {
    public D() {
        // super(); // 可不写
        System.out.println("子类无参构造器");
    }

    public D(String name) {
        // super(); // 可不写
        System.out.println("子类有参构造器");
    }
}

class E extends C {
    public E() {
        super("小明", 6);
        System.out.println("子类无参构造器");
    }

    public E(String name) {
        super("小明", 6);
        System.out.println("子类有参构造器");
    }
}

public class Object3Demo5 {
    public static void main(String[] args) {
        D d1 = new D();
        System.out.println();
        D d2 = new D("小明");
        System.out.println();
        E e1 = new E();
        System.out.println();
        E e2 = new E("小明");
        System.out.println();
    }
}
```

打印结果

```Plain
父类无参构造器
子类无参构造器

父类无参构造器
子类有参构造器

父类有参构造器
子类无参构造器

父类有参构造器
子类有参构造器
```

### 子类构造器的执行原理

将Test2.class和main()方法，以及Teacher类和People类加载到方法区，接下来通过Teacher类创建变量，存储对象，因此栈内存存储变量t，里面的内容为地址，指向堆内存中的对象，通过其类地址找到方法区中的类，找到对应的变量和方法进行创建，进行到super()方法时，进一步前往People类寻找对应的变量和方法进行创建，传回Teacher类，Teacher类创建完所有变量后，再传回到堆内存，此时对象创建完成。之后就是通过get()方法以类似的路径找到变量输出。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512091742379.png)

Object3Demo6.java

```Java
package com.zbhgis.object3;

public class Object3Demo6 {
    public static void main(String[] args) {
        Friend f = new Friend("明", 16, "小明");
        System.out.println(f.getName());
        System.out.println(f.getAge());
        System.out.println(f.getNickname());
    }
}

class Friend extends Person{
    private String nickname;

    public Friend() {
    }

    public Friend(String name, int age, String nickname) {
        super(name, age);
        this.nickname = nickname;
    }

    public String getNickname() {
        return nickname;
    }

    public void setNickname(String nickname) {
        this.nickname = nickname;
    }
}


class Person{
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

打印结果

```Plain
明
16
小明
```

## this兄弟构造器

通过this关键字直接调用兄弟构造器

Object3Demo7.java

```Java
package com.zbhgis.object3;

public class Object3Demo7 {
    public static void main(String[] args) {
        Pet p = new Pet("旺仔", 2.5);
        System.out.println(p.getName());
        System.out.println(p.getAge());
        System.out.println(p.getWeight());
    }
}

class Pet{
    private String name;
    private int age;
    private double weight;

    public Pet() {
    }

    public Pet(String name, double weight) {
        // 没有提供age的情况，可以这么写，提供默认age
        // this.name = name;
        // this.age = 1;
        // this.weight = weight;
        // 也可以this调用兄弟构造器
        this(name, 1, weight);
    }

    public Pet(String name, int age, double weight) {
        this.name = name;
        this.age = age;
        this.weight = weight;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public double getWeight() {
        return weight;
    }

    public void setWeight(double weight) {
        this.weight = weight;
    }
}
```

打印结果

```Plain
旺仔
1
2.5
```

# 总结

1.修饰符权限：private＜缺省＜protected＜public

2.方法重载是在一个类中，形参列表不同；方法重写是在父类和子类之间，形参列表一致。

3.在子类方法中访问其他成员按照就近原则。

4.子类的全部构造器都会先调用父类的构造器，再执行自己。

5.this()和super()不能够在同一处代码中调用构造器。