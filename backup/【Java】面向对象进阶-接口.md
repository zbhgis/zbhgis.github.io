

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括接口的概念，接口的好处，接口的新特性，以及接口的注意事项。

2.笔记对应视频108-110节

# 更新记录

无

# 接口的概念

Java提供了一个关键字interface，用这个关键字我们可以定义出一个特殊的结构：接口。

public interface 接口名{

// 成员变量（常量）

// 成员方法（抽象方法）

}

接口不能创建对象；接口是用来被类实现的，实现接口的类称为实现类。

修饰符 class 实现类 implements 接口1, 接口2, 接口3, ...{

}

一个类可以实现多个接口，实现类实现多个接口必须重写所有接口的所有抽象方法，否则实现类需要定义为抽象类

Object6Demo1.java

```Java
package com.zbhgis.object6;

public class Object6Demo1 {
    public static void main(String[] args) {
        System.out.println(A.STUDENT_NAME);

        // A a = new A(); // 不可行
        D d = new D();
    }

}
```

A.java

```Java
package com.zbhgis.object6;

public interface A {
    // 成员变量
    String STUDENT_NAME = "明";
    // 成员方法（抽象方法）
    void test();
}
```

B.java

```Java
package com.zbhgis.object6;

public interface B {
    void testb1();

    void testb2();
}
```

C.java

```Java
package com.zbhgis.object6;

public interface C {
    void testc1();

    void testc2();
}
```

D.java

```Java
package com.zbhgis.object6;

public class D implements B, C{


    @Override
    public void testb1() {

    }

    @Override
    public void testb2() {

    }

    @Override
    public void testc1() {

    }

    @Override
    public void testc2() {

    }
}
```

# 接口的好处

弥补单继承的不足

解耦合，编程更加灵活

案例：通过接口实现两套方法，打印不同的学生信息和学生分数

Student.java

```Java
package com.zbhgis.object6;

public class Student {
    private String name;
    private char sex;
    private double score;

    public Student() {
    }

    public Student(String name, char sex, double score) {
        this.name = name;
        this.sex = sex;
        this.score = score;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public char getSex() {
        return sex;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }
}
```

ClassManager.java

```Java
package com.zbhgis.object6;

import java.util.ArrayList;

public class ClassManager {
    private ArrayList<Student> students = new ArrayList<>();
    private StudentOperator studentOperator = new StudentOperatorImpl1();

    public ClassManager() {
        students.add(new Student("明", '女', 66));
        students.add(new Student("山", '男', 33));
        students.add(new Student("水", '男', 99));
    }

    public void printInfo() {
        studentOperator.printAllInfo(students);
    }

    public void printScore() {
        studentOperator.printAverageScore(students);
    }
}
```

StudentOperator.java

```Java
package com.zbhgis.object6;

import java.util.ArrayList;

public interface StudentOperator {
    void printAllInfo(ArrayList<Student> students);

    void printAverageScore(ArrayList<Student> students);
}
```

StudentOperatorImpl1.java

```Java
package com.zbhgis.object6;

import java.util.ArrayList;

public class StudentOperatorImpl1 implements StudentOperator {

    @Override
    public void printAllInfo(ArrayList<Student> students) {
        System.out.println("-------------------");
        for (int i = 0; i < students.size(); i++) {
            Student s = students.get(i);
            System.out.println("姓名：" + s.getName() + "性别：" + s.getSex() + "成绩：" + s.getScore());
        }
        System.out.println("--------------------");
    }

    @Override
    public void printAverageScore(ArrayList<Student> students) {
        double allScore = 0.0;
        for (int i = 0; i < students.size(); i++) {
            Student s = students.get(i);
            allScore += s.getScore();
        }
        System.out.println("平均分：" + allScore / students.size());
    }
}
```

StudentOperatorImpl2.java

```Java
package com.zbhgis.object6;

import java.util.ArrayList;

public class StudentOperatorImpl2 implements StudentOperator {
    @Override
    public void printAllInfo(ArrayList<Student> students) {
        System.out.println("-------------------");
        int count1 = 0;
        int count2 = 0;
        for (int i = 0; i < students.size(); i++) {
            Student s = students.get(i);
            System.out.println("姓名：" + s.getName() + "性别：" + s.getSex() + "成绩：" + s.getScore());
            if (s.getSex() == '男') count1++;
            else count2++;
        }
        System.out.println("男生人数：" + count1);
        System.out.println("女生人数：" + count2);
        System.out.println("--------------------");
    }

    @Override
    public void printAverageScore(ArrayList<Student> students) {
        double allScore = 0.0;
        double maxScore = students.get(0).getScore();
        double minScore = students.get(0).getScore();
        for (int i = 0; i < students.size(); i++) {
            Student s = students.get(i);
            allScore += s.getScore();
            if (s.getScore() > maxScore) maxScore = s.getScore();
            if (s.getScore() < minScore) minScore = s.getScore();
        }
        System.out.println("最高分：" + maxScore);
        System.out.println("最低分：" + minScore);
        System.out.println("平均分：" + allScore / students.size());
    }
}
```

Object6Demo2.java

```Java
package com.zbhgis.object6;

public class Object6Demo2 {
    public static void main(String[] args) {
        ClassManager clazz = new ClassManager();
        clazz.printInfo();
        clazz.printScore();
    }
}
```

打印结果

```Plain
-------------------
姓名：明性别：女成绩：66.0
姓名：山性别：男成绩：33.0
姓名：水性别：男成绩：99.0
--------------------
平均分：66.0
```

# 接口的新特性

JDK8之后

1.默认方法，必须被default修饰，默认被public修饰

2.私有方法，必须被private修饰

3.静态方法，必须被static修饰，默认被public修饰

# 接口的注意事项

1、一个接口继承多个接口，如果多个接口中存在方法签名冲突，则此时不支持多继承。

2、一个类实现多个接口，如果多个接口中存在方法签名冲突，则此时不支持多实现。

3、一个类继承了父类，又同时实现了接口，父类中和接口中有同名的默认方法，实现类会优先用父类的。

4、一个类实现了多个接口，多个接口中存在同名的默认方法，可以不冲突，这个类重写该方法即可。

了解即可

# 总结

1.接口不能创建对象

2.接口通过类实现

3.一个类可以实现多个接口

4.一个类可以实现多个接口，实现类实现多个接口必须重写所有接口的所有抽象方法，否则实现类需要定义为抽象类

5.接口可以继承接口