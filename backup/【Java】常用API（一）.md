
[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括Object类，Objects类，包装类，StringBuilder类，以及StringJoiner类

2.笔记对应视频116-118节

# 更新记录

无

# Object类

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080748735.png)

Student.java

```Java
package com.zbhgis.apis;

import java.util.Arrays;
import java.util.Objects;

// 实现克隆接口
public class Student implements Cloneable {
    private String name;
    private int age;
    private int[] scores;

    public Student() {
    }

    public Student(String name, int age, int[] scores) {
        this.name = name;
        this.age = age;
        this.scores = scores;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", scores=" + Arrays.toString(scores) +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && Objects.equals(name, student.name) && Objects.deepEquals(scores, student.scores);
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    protected Object clone2() throws CloneNotSupportedException {
        Student s2 = (Student) super.clone();
        // 深克隆，数组单独克隆
        s2.scores = s2.scores.clone();
        return s2;
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

    public int[] getScores() {
        return scores;
    }

    public void setScores(int[] scores) {
        this.scores = scores;
    }
}
```

Apis1.java

```Java
package com.zbhgis.apis;

public class Apis1 {
    // 必须设置抛出异常
    public static void main(String[] args) throws CloneNotSupportedException {
        Student s1 = new Student("赵敏", 23, new int[]{40, 60});
        System.out.println(s1);

        Student s2 = new Student("赵敏", 23, new int[]{40, 60});
        System.out.println(s2.equals(s1));

        // 默认重写的是浅克隆，克隆之后里面数组元素的地址一致
        Student s3 = (Student) s1.clone();
        System.out.println(s1.getScores());
        System.out.println(s3.getScores());

        // 深克隆，克隆之后里面数组元素的地址不一致
        Student s4 = (Student) s1.clone2();
        System.out.println(s4.getScores());

    }
}
```

打印结果

```Plain
Student{name='赵敏', age=23, scores=[40, 60]}
true
[I@5f184fc6
[I@5f184fc6
[I@3feba861
```

# Objects类

工具类，提供了很多操作对象的静态方法

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080749808.png)

Apis2.java

```Java
package com.zbhgis.apis;

import java.util.Objects;

public class Apis2 {
    public static void main(String[] args) {
        String s1 = null;
        String s2 = "itheima";

        System.out.println(Objects.equals(s1, s2));
        System.out.println(Objects.isNull(s1));
        System.out.println(s1 == null);
        System.out.println(Objects.isNull(s2));
        System.out.println(s2 == null);

        System.out.println(Objects.nonNull(s2));
        System.out.println(Objects.nonNull(s1));

    }
}
```

打印结果

```Plain
false
true
true
false
false
true
false
```

# 包装类

将基本类型的数据包装成对象

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080748737.png)

Apis3.java

```Java
package com.zbhgis.apis;

import java.util.ArrayList;

public class Apis3 {
    public static void main(String[] args) {
        // 已经弃用
        // Integer a1 = new Integer(12);

        Integer a2 = Integer.valueOf(12);
        System.out.println(a2);
        // 自动装箱：可以自动将基本类型的数据转换为对象
        Integer a3 = 12;
        // 自动拆箱：可以自动把包装类型的对象转换为对应的基本数据类型
        int a4 = a3;

        ArrayList<Integer> list = new ArrayList<>();
        list.add(12); // 自动装箱
        list.add(13); // 自动装箱

        int rs = list.get(1); // 自动拆箱
        System.out.println("--------------------");

        Integer a = 23;
        String rs1 = Integer.toString(a);
        System.out.println(rs1 + 1);
        String rs2 = a.toString();
        System.out.println(rs2 + 1);
        String rs3 = a + "";
        System.out.println(rs3 + 1);

        String ageStr = "29";
        // 或者Integer.parseInt();
        int ageI = Integer.valueOf(ageStr);
        System.out.println(ageI + 1);

        String scoreStr = "99.5";
        // 或者Double.parseDouble();
        double score = Double.valueOf(scoreStr);
        System.out.println(score + 0.5);
    }
}
```

打印结果

```Plain
12
--------------------
231
231
231
30
100.0
```

# StringBuilder类

StringBuilder代表可变字符串对象，相当于是一个容器，它里面装的字符串是可以改变的，就是用来操作字符串的，效率比String更高，频繁的操作建议使用StringBuilder

StringBuffer是线程安全的，操作与StringBuilder类似

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080749366.png)

Apis4.java

```Java
package com.zbhgis.apis;

public class Apis4 {
    public static void main(String[] args) {
        // StringBuilder s = new StringBuilder(); // s ""
        StringBuilder s = new StringBuilder("明"); // s "明"

        // 1、拼接内容
        s.append(12);
        s.append("山");
        s.append(true);

        // 支持链式编程
        s.append(1).append("心").append(1).append("意");
        System.out.println(s);

        // 反转
        s.reverse();
        System.out.println(s);

        // 字符串长度
        System.out.println(s.length());
    }
}
```

打印结果

```OpenGL
明12山true1心1意
意1心1eurt山21明
12
意1心1eurt山21明
```

# StringJoiner类

用于操作字符串，不仅能提高字符串的操作效率，并且在有些场景下使用它操作字符串，代码会更简洁

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601080749841.png)

Apis5.java

```Java
package com.zbhgis.apis;

import java.util.StringJoiner;

public class Apis5 {
    public static void main(String[] args) {
        StringJoiner s = new StringJoiner(", ", "[", "]");
        s.add("java1");
        s.add("java2");
        s.add("java3");
        System.out.println(s);

        System.out.println(getArrayData(new int[]{11, 22, 33}));
    }

    public static String getArrayData(int[] arr){
        if(arr == null){
            return null;
        }

        StringJoiner s = new StringJoiner(", ", "[", "]");
        for (int i = 0; i < arr.length; i++) {
            s.add(arr[i] + "");
        }
        return s.toString();
    }
}
```

打印结果

```Plain
[java1, java2, java3]
[11, 22, 33]
```

# 总结

多练多写就记住了