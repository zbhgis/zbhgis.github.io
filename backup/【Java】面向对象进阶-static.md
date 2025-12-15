

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m/?vd_source=3b69b85b41f42a9e26b3a8a195228a36

# 内容概览

1.本文内容主要包括static修饰变量和方法，设计工具类，代码块，以及单例设计模式。

2.笔记对应视频92-98节

# 更新记录

无

# static修饰变量

类变量：有static修饰，属于类，在计算机里只有一份，会被类的全部对象共享。可以通过类名.类变量（推荐）或对象.类变量（不推荐）或类变量（在某个类中访问其他类里的类变量必须带类名访问）进行调用；用于某个数据只需要一份的场景，则该数据可以通过定义成类变量来记住。

实例变量（对象的变量）：无static修饰，属于每个对象的。可以通过对象.实例变量进行调用。

首先执行Test类，将其加载到方法区中，然后执行main()；接下来执行给类变量赋值，需要调用Student类，因此将Student类加载到方法区中，其中的类变量name也在此时加载到堆内存中，为默认值null，而由于代码给name实行了赋值操作，因此其值为“袁华”；由于需要调用Student类，在栈内存中开始存储变量s1，并在堆内存中开辟新创建的对象的空间，s1存储具体对象的地址，地址指向的堆内存中存有对应的数据以及Student类的地址；此时对象s1.name根据具体对象的地址，找到堆内存中的数据及其类地址，通过类地址找到类变量name，将堆内存中的变量名字改为“马冬梅”；s2同理。最后通过s1找到name，打印name，再通过Student找到name，打印name。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512071450196.png)

Student.java

```Java
package com.zbhgis.object2;

public class Student {
    static String name;
    int age;

    public static String getName() {
        return name;
    }

    public static void setName(String name) {
        Student.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

Object2Demo1.java

```Java
package com.zbhgis.object2;

public class Object2Demo1 {
    public static void main(String[] args) {
        // 类变量
        Student.name = "山";
        Student s1 = new Student();
        System.out.println(s1.name);
        s1.name = "重";
        System.out.println(s1.name);
        Student s2 = new Student();
        s2.name = "复";
        System.out.println(s1.name);

        // 实例变量
        s1.age = 23;
        s2.age = 18;
        System.out.println(s1.age);
        System.out.println(s2.age);
    }
}
```

打印结果

```Plain
山
重
复
com.zbhgis.object2.Student@4eec7777
com.zbhgis.object2.Student@3b07d329
```

# static修饰方法

类方法：有static修饰，属于类，在计算机里只有一份，会被类的全部对象共享。可以通过类名.类方法（推荐）或对象.类方法（不推荐）或类方法（在某个类中访问其他类里的类方法必须带类名访问）进行调用；用于某个方法只需要一份的场景，则该数据可以通过定义成类方法来记住。main方法也是类方法。

实例方法（对象的方法）：无static修饰，属于每个对象的。可以通过对象.实例方法进行调用。

首先执行Test类，将其加载到方法区中，然后执行main()；接下来需要调用Student类，因此将Student类加载到方法区中，其中的实例变量，实例方法，类方法也在此时加载到方法区中，为默认值，而由于代码调用printHelloWorld()方法，此时直接打印两行“HelloWorld”；由于需要调用Student类，在栈内存中开始存储变量s，并在堆内存中开辟新创建的对象的空间，s存储具体对象的地址，地址指向的堆内存中存有对应的数据以及Student类的地址；此时对象s.printHelloWorld()根据具体对象的地址，找到类地址，通过类地址找到类方法printHelloWorld()，打印两行“HelloWorld”；对象s.printPass()根据具体对象的地址，找到在堆内存中的具体数据和类地址，通过类地址找到对象方法printpass()，根据逻辑找到需要的具体数据score，打印“成绩：不及格”。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512071449822.png)

Student.java

```Java
package com.zbhgis.object2;

public class Student {
    static String name;
    int age;

    public static String getName() {
        return name;
    }

    public static void setName(String name) {
        Student.name = name;
    }

    public static void printName() {
        System.out.println("名字：" + Student.name);
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void printAge() {
        System.out.println("年龄：" + this.age);
    }
}
```

Object2Demo2.java

```Java
package com.zbhgis.object2;

public class Object2Demo2 {
    public static void main(String[] args) {
        Student.printName();
        Student s = new Student();
        s.printAge();
        // 不推荐写法
        s.printName();
    }
}
```

打印结果

```Plain
名字：null
年龄：0
名字：null
```

# static方法设计工具类

类方法用来设计工具类，不使用实例方法是因为实例方法需要创建对象来调用，会浪费内存。

工具类中的方法都是类方法， 每个类方法都是用来完成一个功能的，可以提高代码复用性和开发效率。

工具类不需要创建对象，建议将工具类的构造器私有化。

MyUtil.java

```Java
package com.zbhgis.object2;

public class MyUtil {
    private MyUtil() {
        
    }

    public static int calSum(int n) {
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            sum += i;
        }
        return sum;
    }
}
```

Object2Demo3.java

```Java
package com.zbhgis.object2;

public class Object2Demo3 {
    public static void main(String[] args) {
        System.out.println(MyUtil.calSum(100));
    }
}
```

打印结果

```Plain
5050
```

# static的注意事项

类方法中可以直接访问类的成员，不可以直接访问实例成员。

实例方法中既可以直接访问类成员，也可以直接访问实例成员。

实例方法中可以出现this关键字，类方法中不可以出现this关键字的，

# 代码块

代码块是类的5大成分之一（成员变量、构造器、方法、代码块、内部类）。

静态代码块：类加载时自动执行，由于类只会加载一次，所以静态代码块也只会执行一次。用于完成类的初始化，例如：对类变量的初始化赋值。

实例代码块：每次创建对象时，执行实例代码块，并在构造器前执行。可以用于实现创建对象日志记录。

Student.java

```Java
package com.zbhgis.object2;

public class Student {
    static String name;

    static {
        System.out.println("静态代码块执行了");
    }

    int age;

    {
        System.out.println("实例代码块执行了");
        System.out.println("对象创建：" + this);
    }

    public Student() {
        System.out.println("无参构造器执行了");
    }

    public Student(String name, int age) {
        System.out.println("有参构造器执行了");
    }

    public static String getName() {
        return name;
    }

    public static void setName(String name) {
        Student.name = name;
    }

    public static void printName() {
        System.out.println("名字：" + Student.name);
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void printAge() {
        System.out.println("年龄：" + this.age);
    }

}
```

Object2Demo5.java

```Java
package com.zbhgis.object2;

import java.rmi.StubNotFoundException;

public class Object2Demo5 {
    public static void main(String[] args) {
        Student.name = "水";
        System.out.println();
        Student s1 = new Student();
        System.out.println();
        s1.name = "山";
        System.out.println();
        s1.age = 18;
        System.out.println();
        Student s2 = new Student("重", 20);
    }
}
```

打印结果

```Plain
静态代码块执行了

实例代码块执行了
对象创建：com.zbhgis.object2.Student@6d311334
无参构造器执行了



实例代码块执行了
对象创建：com.zbhgis.object2.Student@682a0b20
有参构造器执行了
```

# 单例设计模式

确保一个类只有一个对象。

1.把类的构造器私有

2.定义一个类变量记住类的一个对象

3.定义一个类方法，返回对象。

A.java

```Java
package com.zbhgis.object2;

public class A {
    // 2. 定义一个类变量记住类的一个对象。
    private static A a = new A();

    // 1. 构造器私有化。
    private A() {

    }

    // 3. 定义一个类方法，返回对象。
    public static A getObject() {
        return a;
    }
}
```

Object2Demo6.java

```Java
package com.zbhgis.object2;

public class Object2Demo6 {
    public static void main(String[] args) {
        A a1 = A.getObject();
        A a2 = A.getObject();
        System.out.println(a1);
        System.out.println(a2);
    }
}
```

打印结果

```Plain
com.zbhgis.object2.A@4eec7777
com.zbhgis.object2.A@4eec7777
```

# 总结

1.有static修饰的变量和方法属于类

2.类方法中不可以出现this关键字

3.代码块的作用了解即可，不常用。