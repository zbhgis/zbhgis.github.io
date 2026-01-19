

个人主页：https://github.com/zbhgis

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括集合特点，HashSet，LinkedHashSet，以及TreeSet集合

2.笔记对应视频140~141节

# 更新记录

无

# 集合特点

无序

HashSet：无序、不重复、无索引

LinkedHashSet：有序、不重复、无索引

TreeSet：可排序、不重复、无索引

Sets1.java

```Java
package com.zbhgis.sets;

import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.Set;
import java.util.TreeSet;

public class Sets1 {
    public static void main(String[] args) {
        // HashSet：无序、不重复、无索引
        // [0, 1, 2, 5, 7, -10]
        // Set<Integer> set = new HashSet<>();
        // LinkedHashSet：有序、不重复、无索引
        // [1, 5, 7, 0, -10, 2]
        // Set<Integer> set = new LinkedHashSet<>();
        // TreeSet：可排序、不重复、无索引
        // [-10, 0, 1, 2, 5, 7]
        Set<Integer> set = new TreeSet<>();
        set.add(1);
        set.add(5);
        set.add(7);
        set.add(0);
        set.add(1);
        set.add(-10);
        set.add(2);
        System.out.println(set);
    }
}
```

打印结果

```Plain
[-10, 0, 1, 2, 5, 7]
```

# HashSet

所有对象都有自己的哈希值

同一个对象多次调用hashCode()方法返回的哈希值是相同的

不同的对象它们的哈希值大概率不同，极小概率相同

jdk8之前HashSet集合的底层原理，基于哈希表：数组+链表；之后基于哈希表：数组+链表+红黑树

希望内容一致时hash值一致，则需要自行重写hashCode()方法

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131012719.png)

Student.java

```Java
package com.zbhgis.sets;

import java.util.Arrays;
import java.util.Objects;

public class Student{
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
    public int hashCode() {
        return Objects.hash(name, age, Arrays.hashCode(scores));
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

Sets2.java

```Java
package com.zbhgis.sets;

public class Sets2 {
    public static void main(String[] args) {
        Student s1 = new Student("山", 16, new int[]{60, 99});
        Student s2 = new Student("重", 16, new int[]{59, 100});
        Student s3 = new Student("山", 16, new int[]{60, 99});
        Student s4 = new Student("复", 16, new int[]{58, 57});
        System.out.println(s1.hashCode());
        System.out.println(s1.hashCode());
        System.out.println(s2.hashCode());
        System.out.println(s3.hashCode());

        String str1 = new String("abc");
        String str2 = new String("acD");
        System.out.println(str1.hashCode());
        System.out.println(str2.hashCode());
    }
}
```

打印结果

```Plain
22775272
22775272
35902502
22775272
96354
96354
```

# LinkedHashSet

基于哈希表（数组、链表、红黑树）实现的。

但是它的每个元素都额外多了一个双链表的机制记录它前后元素的位置。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131011913.png)

Sets3.java

```Java
package com.zbhgis.sets;

import java.util.LinkedHashSet;
import java.util.Set;

public class Sets3 {
    public static void main(String[] args) {
        Set<Integer> set = new LinkedHashSet<>();
        set.add(1);
        set.add(5);
        set.add(7);
        set.add(0);
        set.add(1);
        set.add(-10);
        System.out.println(set);
        set.add(2);
        System.out.println(set);
    }
}
```

打印结果

```Plain
[1, 5, 7, 0, -10]
[1, 5, 7, 0, -10, 2]
```

# TreeSet

基于哈希表（数组、链表、红黑树）实现的。

对于数值类型，默认按照数值本身的大小进行升序排序

对于字符串类型，默认按照首字符的编号升序排序

对于自定义类型，默认无法直接排序，必须指定排序规则（实现Comparable接口或者调用TreeSet集合有参构造器）

Student.java

```Java
package com.zbhgis.sets;

import java.util.Arrays;
import java.util.Objects;

public class Student implements Comparable<Student>{
    private String name;
    private int age;
    private int[] scores;

    @Override
    public int compareTo(Student o) {
        return this.age - o.age;
    }

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
    public int hashCode() {
        return Objects.hash(name, age, Arrays.hashCode(scores));
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

    public int getAverageScore() {
        return (scores[0] + scores[1]) / 2;
    }
}
```

Sets4.java

```Java
package com.zbhgis.sets;

import java.util.Comparator;
import java.util.Set;
import java.util.TreeSet;

public class Sets4 {
    public static void main(String[] args) {
        Student s1 = new Student("山", 16, new int[]{60, 99});
        Student s2 = new Student("重", 15, new int[]{59, 100});
        Student s3 = new Student("山", 16, new int[]{60, 99});
        Student s4 = new Student("复", 17, new int[]{58, 57});
        // Set<Student> students = new TreeSet<>();
        // [Student{name='重', age=15, scores=[59, 100]}, Student{name='山', age=16, scores=[60, 99]}, Student{name='复', age=17, scores=[58, 57]}]
        // 就近原则，选择自身的比较器
        Set<Student> students = new TreeSet<>((o1, o2) -> Double.compare(o1.getAverageScore(), o2.getAverageScore()));
        students.add(s1);
        students.add(s2);
        students.add(s3);
        students.add(s4);
        System.out.println(students);
    }
}
```

打印结果

```Plain
[Student{name='复', age=17, scores=[58, 57]}, Student{name='山', age=16, scores=[60, 99]}]
```

# 总结

1.

HashSet：无序、不重复、无索引

LinkedHashSet：有序、不重复、无索引

TreeSet：可排序、不重复、无索引

2.TreeSet中自定义类型，默认无法直接排序，必须指定排序规则（实现Comparable接口或者调用TreeSet集合有参构造器）