
# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站[黑马程序员](https://space.bilibili.com/37974444)的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m/?vd_source=3b69b85b41f42a9e26b3a8a195228a36

# 内容概览

1.本节内容包括面向对象的概念、执行原理，this关键字，构造器，封装，以及实体类JavaBean

2.笔记对应视频69-75节

# 更新记录

无

# 面向对象的概念

对象本质上是一种特殊的数据结构。class也就是类，也称为对象的设计图（或者对象的模板）。对象是用类new出阿里的，有了类就可以创建对象。

# 对象的执行原理

首先执行Test类，将其加载到方法区中，然后执行main()；接下来需要创建学生类，需要调用Student类，因此将Student类加载到方法区中；由于开始创建对象，在栈内存中开始存储变量s1，并在堆内存中开辟新创建的对象的空间，s1存储具体对象的地址，地址指向的堆内存中存有对应的数据以及Student类的地址，其按照Student类的要求，创建对应的对象变量，存储值为默认值；此时对象s1根据具体对象的地址，指向堆内存中的数据，因此后续赋值时，对s1的各个变量赋值，相当于改变了s1地址指向的堆内存中的内部变量的值。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512071438795.png)

Student.java

```Java
package com.zbhgis.object;

public class Student {
    String name;
    double chinese;
    double math;

    public void printTotalScore() {
        System.out.println(name + "总成绩是" + (chinese + math));
    }

    public void printAverageScore() {
        System.out.println(name + "平均成绩是:" + (chinese + math) / 2);
    }
}
```

ObjectDemo1.java

```Java
package com.zbhgis.object;

public class ObjectDemo1 {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "小明";
        s1.chinese = 100;
        s1.math = 10;
        s1.printTotalScore();
        s1.printAverageScore();

        Student s2 = new Student();
        s2.name = "李华";
        s2.chinese = 59;
        s2.math = 59;
        s2.printTotalScore();
        s2.printAverageScore();

        System.out.println(s1);
        System.out.println(s2);
    }

}
```

打印结果

```Plain
小明总成绩是110.0
小明平均成绩是:55.0
李华总成绩是118.0
李华平均成绩是:59.0
com.zbhgis.object.Student@15aeb7ab
com.zbhgis.object.Student@7b23ec81
```

# 对象的注意点

1.类名建议用英文单词，首字母大写，满足驼峰模式，且要有意义，比如Student, Car

2.类中定义的变量也称为成员变量（对象的属性），类中定义的方法也称为成员方法（对象的行为）。

3.成员变量本身存在默认值，定义成员变量时不必赋值

4.一个代码文件中可以写多个class类，但只能一个用public修饰，且用public修饰的类名必须成为代码文件名。

5.对象与对象之间的数据不会相互影响，但是多个变量指向同一个对象就会相互影响

当多个变量指向同一对象，其地址相同，指向堆内存的空间也相同。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512071438745.png)

6.如果某个对象没有一个变量引用它，则该对象无法被操作了，该对象会成为所谓的垃圾对象

Java存在自动来及回收机制，会自动清楚掉垃圾对象。

```Java
package com.zbhgis.object;

public class ObjectDemo2 {
    public static void main(String[] args) {
        Student s1 = new Student();
        // 成员变量存在默认值
        System.out.println(s1.name);
        System.out.println(s1.chinese);

        // 多个变量指向同一对象
        s1.math = 66;
        Student s2 = s1;
        s2.math = 99;
        System.out.println(s1.math);

        // 调用垃圾对象会报错
        s1 = null;
        System.out.println(s1.chinese);
    }
}
```

打印结果

```Plain
null
0.0
99.0
Exception in thread "main" java.lang.NullPointerException: Cannot read field "chinese" because "s1" is null
        at com.zbhgis.object.ObjectDemo2.main(ObjectDemo2.java:18)
```

# this关键字

this就是一个变量，可以用在方法中，获取到当前对象。用于解决变量冲突问题

首先执行Test类，将其加载到方法区中，然后执行main()；接下来需要创建学生类，需要调用Student类，因此将Student类加载到方法区中；由于开始创建对象，在栈内存中开始存储变量s1，并在堆内存中开辟新创建的对象的空间，其中存储具体对象的地址，s1存储具体对象的地址，地址指向的堆内存中存有对应的数据以及Student类的地址；此时对象s1.printThis()根据具体对象的地址，找到堆内存中的对象地址及其类地址，通过类地址找到调用到printThis()，即打印本身地址，又从堆内存中找到对象地址进行打印；s2同理。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512071438439.png)

Student.java

```Java
package com.zbhgis.object;

public class Student {
    String name;
    double chinese;
    double math;

    public void printTotalScore() {
        System.out.println(name + "总成绩是" + (chinese + math));
    }

    public void printAverageScore() {
        System.out.println(name + "平均成绩是:" + (chinese + math) / 2);
    }

    public void printThis() {
        System.out.println(this);
    }

    public void printPass(double math) {
        // 解决变量命名冲突
        if (this.math < math) System.out.println("pass");
        else System.out.println("failure");
    }
}
```

ObjectDemo3.java

```Java
package com.zbhgis.object;

public class ObjectDemo3 {
    public static void main(String[] args) {
        Student s1 = new Student();
        System.out.println(s1);
        s1.printThis();
        s1.math = 59;
        s1.printPass(60);

        Student s2 = new Student();
        System.out.println(s2);
        s2.printThis();
        s2.math = 100;
        s2.printPass(60);
    }
}
```

打印结果

```Java
com.zbhgis.object.Student@4eec7777
com.zbhgis.object.Student@4eec7777
pass
com.zbhgis.object.Student@3b07d329
com.zbhgis.object.Student@3b07d329
failure
```

# 构造器

创建对象时，对象会去调用构造器，完成对对象成员变量（属性）的初始化赋值。

public class 名字{

public 名字(){

 ...

}

}

类在设计时，如果不写构造器，Java是会为类自动生成一个无参构造器的

一旦定义了有参数构造器，Java就不会帮我们的类自动生成无参构造器了，此时就建议自己手写第一个无参构造器出来。

Teacher.java

```Java
package com.zbhgis.object;

public class Teacher {
    String name;
    int age;

    public Teacher() {
        System.out.println("Teacher1");
    }

    public Teacher(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Teacher2");
    }
}
```

ObjectDemo4.java

```Java
package com.zbhgis.object;

public class ObjectDemo4 {
    public static void main(String[] args) {
        Teacher t1 = new Teacher();
        System.out.println(t1.name);
        System.out.println(t1.age);
        Teacher t2 = new Teacher("明", 60);
        System.out.println(t2.name);
        System.out.println(t2.age);
    }
}
```

打印结果

```Plain
Teacher1
null
0
Teacher2
明
60
```

# 封装

用类设计对象处理某一个事物的数据时，应该把要处理的数据，以及处理这些数据的方法，设计到一个对象中去。通过修饰符public和private来控制对象的成员公开，实现合理暴露，合理隐藏。

Teacher.java

```Java
package com.zbhgis.object;

public class Teacher {
    String name;
    int age;

    public Teacher() {
    }

    public Teacher(String name, int age) {
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

    public void printAll() {
        System.out.println(this.name + " " + this.age);
    }
}
```

ObjectDemo5.java

```Java
package com.zbhgis.object;

public class ObjectDemo5 {
    public static void main(String[] args) {
        Teacher t1 = new Teacher();
        t1.age = 40;
        t1.name = "明";
        t1.printAll();

        Teacher t2 = new Teacher("柳", 60);
        t2.setAge(77);
        t2.setName("花");
        t2.printAll();
    }
}
```

打印结果

```Plain
明 40
花 77
```

# 实体类JavaBean

一种特殊的类，只负责数据存取，而对数据的处理交给其他类来完成，以实现数据和数据业务处理相分离。其中，成员变量都要私有，并且要对外提供相应的get，set方法；且类中必须要有一个公共无参的构造器。

Lecture.java

```Java
package com.zbhgis.object;

public class Lecture {
    private String name;
    private long code;

    public Lecture(){

    }

    public Lecture(String name, long code) {
        this.name = name;
        this.code = code;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public long getCode() {
        return code;
    }

    public void setCode(long code) {
        this.code = code;
    }
}
```

LectureOperator.java

```Java
package com.zbhgis.object;

public class LectureOperator {
    private Lecture lecture;

    public LectureOperator(Lecture lecture) {
        this.lecture = lecture;
    }

    public void printAll() {
        System.out.println(lecture.getName() + " " + lecture.getCode());
    }
}
```

ObjectDemo6.java

```Java
package com.zbhgis.object;

public class ObjectDemo6 {
    public static void main(String[] args) {
        Lecture l1 = new Lecture();
        l1.setName("Geology");
        l1.setCode(1003499);
        System.out.println(l1.getName());
        System.out.println(l1.getCode());

        LectureOperator lp = new LectureOperator(l1);
        lp.printAll();
    }
}
```

打印结果

```Plain
Geology
1003499
Geology 1003499
```