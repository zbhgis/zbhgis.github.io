

个人主页：https://github.com/zbhgis

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括Lambda表达式，方法引用，以及Stream流

2.笔记对应视频127-128节，149-150节

# 更新记录

无

# Lambda表达式

Lambda表达式是JDK8开始新增的一种语法形式；作用：用于简化匿名内部类的代码写法。

(被重写方法的形参列表) -> {

被重写方法的方法体代码

}

只能简化函数式接口的匿名内部类（有且仅有一个抽象方法的接口，上面都可能会有一个@FunctionlInterface的注解，有该注解的接口就必定是函数式接口）。

Fresh1.java

```Java
package com.zbhgis.fresh;

import java.util.Arrays;

public class Fresh1 {
    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50, 60};
        System.out.println(Arrays.toString(arr));

        int[] arr2 = Arrays.copyOfRange(arr, 3, 4);
        System.out.println(Arrays.toString(arr2));

        int[] arr3 = Arrays.copyOf(arr, 10);
        System.out.println(Arrays.toString(arr3));

        double[] prices = {99.8, 124, 10};
        // Arrays.setAll(prices, new IntToDoubleFunction() {
        //     @Override
        //     public double applyAsDouble(int value) {
        //         return prices[value] * 0.8;
        //     }
        // });

        // Arrays.setAll(prices, (int value) -> {
        //         return prices[value] * 0.8;
        // });

        // Arrays.setAll(prices, (value) -> {
        //     return prices[value] * 0.8;
        // });

        // Arrays.setAll(prices, value -> {
        //     return prices[value] * 0.8;
        // });

        Arrays.setAll(prices, value -> prices[value] * 0.8);
    }
}
```

# 方法引用

## 静态方法引用

类名::静态方法

如果某个Lambda表达式里只是调用一个静态方法，并且前后参数形式一致，就可以使用静态方法引用。

## 实例方法引用

对象名::实例方法

如果某个Lambda表达式里只是调用一个实例方法，并且前后参数的形式一致，就可以使用实例方法引用。

## 特定类型方法的引用

类型::方法

如果某个Lambda表达式里只是调用一个实例方法，并且前面参数列表中的第一个参数是作为方法的主调，后面的所有参数都是作为该实例方法的入参的，则此时就可以使用特定类型的方法引用

## 构造器引用

类名::new

如果某个Lambda表达式里只是在创建对象，并且前后参数情况一致，就可以使用构造器引用，

（了解即可）

Fresh2.java

```Java
package com.zbhgis.fresh;

import java.util.Arrays;

interface CreateStudent {
    Student create(String name, int age, int[] scores);
}

public class Fresh2 {
    public static void main(String[] args) {
        Student[] students = new Student[4];
        students[0] = new Student("山", 16, new int[]{60, 99});
        students[1] = new Student("重", 15, new int[]{59, 100});
        students[2] = new Student("山", 16, new int[]{60, 99});
        students[3] = new Student("复", 17, new int[]{61, 100});

        // 静态方法引用
        // Arrays.sort(students, (o1, o2) -> CompareByData.compareByScore(o1, o2));
        Arrays.sort(students, CompareByData::compareByScore);
        System.out.println(Arrays.toString(students));

        // 实例方法引用
        CompareByData compare = new CompareByData();
        // Arrays.sort(students, (o1, o2) -> compare.compareByScoreDesc(o1, o2));
        Arrays.sort(students, compare::compareByScoreDesc);
        System.out.println(Arrays.toString(students));

        // 特定类型方法的引用
        String[] names = {"aa", "bc", "ab", "vd", "cd"};
        // Arrays.sort(names, (o1, o2) -> o1.compareToIgnoreCase(o2));
        Arrays.sort(names, String::compareToIgnoreCase);
        System.out.println(Arrays.toString(names));

        // CreateStudent cs = new CreateStudent() {
        //     @Override
        //     public Student create(String name, int age, int[] scores) {
        //         return new Student(name, age, scores);
        //     }
        // };

        // 构造器引用
        // CreateStudent cs = (name, age, scores) -> new Student(name, age, scores);
        CreateStudent cs = Student::new;
        Student s = cs.create("明", 23, new int[]{48, 71});
        System.out.println(s);
    }
}
```

打印结果

```Plain
[Student{name='山', age=16, scores=[60, 99]}, Student{name='重', age=15, scores=[59, 100]}, Student{name='山', age=16, scores=[60, 99]}, Student{name='复', age=17, scores=[61, 100]}]
[Student{name='复', age=17, scores=[61, 100]}, Student{name='山', age=16, scores=[60, 99]}, Student{name='重', age=15, scores=[59, 100]}, Student{name='山', age=16, scores=[60, 99]}]
[aa, ab, bc, cd, vd]
Student{name='明', age=23, scores=[48, 71]}
```

# Stream流

## Stream的使用

大量结合Lambda语法，可链式调用，用于操作集合或数组的数据

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601181025455.png)

Fresh3.java

```Java
package com.zbhgis.fresh;

import java.util.*;
import java.util.stream.Stream;

public class Fresh3 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        String[] strs = {"Java", "Python", "C", "C++", "C#", "JavaScript"};
        Collections.addAll(list, strs);
        Stream<String> stream1 = list.stream();
        stream1.forEach(System.out::println);
        System.out.println();

        Set<String> set = new HashSet<>();
        Collections.addAll(set, strs);
        Stream<String> stream2 = set.stream();
        stream2.filter(s -> s.contains("C")).forEach(System.out::println);
        System.out.println();

        Map<Integer, String> map = new HashMap<>();
        for (int i = 0; i < strs.length; i++) {
            map.put(i, strs[i]);
        }
        Set<Integer> keys = map.keySet();
        Stream<Integer> stream3 = keys.stream();
        stream3.forEach(System.out::println);
        System.out.println();

        Collection<String> values = map.values();
        Stream<String> stream4 = values.stream();
        stream4.forEach(System.out::println);

        Set<Map.Entry<Integer, String>> entries = map.entrySet();
        Stream<Map.Entry<Integer, String>> stream5 = entries.stream();
        stream5.filter(e -> e.getValue().contains("Java")).forEach(System.out::println);
        System.out.println();

        Stream<String> stream6 = Arrays.stream(strs);
        Stream<String> stream7 = Stream.of(strs);
        stream6.forEach(System.out::println);
        System.out.println();
        stream7.forEach(System.out::println);
        System.out.println();
    }
}
```

打印结果

```Plain
Java
Python
C
C++
C#
JavaScript

C#
C++
C

0
1
2
3
4
5

Java
Python
C
C++
C#
JavaScript
0=Java
5=JavaScript

Java
Python
C
C++
C#
JavaScript

Java
Python
C
C++
C#
JavaScript
```

## stream的常用中间方法

调用完成会返回新的stream流，支持链式

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601181025464.png)

Fresh4.java

```Java
package com.zbhgis.fresh;

import java.awt.image.ImageProducer;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.stream.Stream;

public class Fresh4 {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        Student s1 = new Student("山", 16, new int[]{60, 99});
        Student s2 = new Student("重", 15, new int[]{59, 100});
        Student s3 = new Student("山", 16, new int[]{60, 99});
        Student s4 = new Student("复", 17, new int[]{61, 100});
        Collections.addAll(students, s1, s2, s3, s4);

        // 找出年龄大于15岁的学生，并降序输出
        students.stream().filter(s -> s.getAge() > 15)
                .sorted((o1, o2) -> o2.getAge() - o1.getAge())
                .forEach(System.out::println);
        System.out.println();

        // 找到年龄最小的前3名学生，并输出
        students.stream().sorted((o1, o2) -> Integer.compare(o1.getAge(), o2.getAge()))
                .limit(3)
                .forEach(System.out::println);
        System.out.println();

        // 找到年龄最小的学生，并输出
        students.stream().sorted((o1, o2) -> Integer.compare(o2.getAge(), o1.getAge()))
                .skip(students.size() - 3)
                .forEach(System.out::println);
        System.out.println();

        // 找到年龄小于等于16的学生，并输出名字
        // 如果需要内容一样就认为重复，那就需要重写hashCode()和equals()
        students.stream().filter(s -> s.getAge() <= 16)
                .map(Student::getName)
                .distinct()
                .forEach(System.out::println);
        System.out.println();

        // 拼接
        Stream<String> stream1 = Stream.of("1", "2");
        Stream<String> stream2 = Stream.of("1", "4");
        Stream<String> allStream = Stream.concat(stream1, stream2);
        allStream.forEach(System.out::println);
    }
}
```

打印结果

```Plain
Student{name='复', age=17, scores=[61, 100]}
Student{name='山', age=16, scores=[60, 99]}
Student{name='山', age=16, scores=[60, 99]}

Student{name='重', age=15, scores=[59, 100]}
Student{name='山', age=16, scores=[60, 99]}
Student{name='山', age=16, scores=[60, 99]}

Student{name='山', age=16, scores=[60, 99]}
Student{name='山', age=16, scores=[60, 99]}
Student{name='重', age=15, scores=[59, 100]}

山
重

1
2
1
4
```

## Stream流的常见终结方法

调用完成后，不会返回新的Stream了，没法继续使用流了。

流只能收集一次

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601181028880.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601181025357.png)

Student.java

```Java
package com.zbhgis.fresh;

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

Fresh5.java

```Java
package com.zbhgis.fresh;

import java.util.*;
import java.util.stream.Collectors;

public class Fresh5 {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        Student s1 = new Student("山", 16, new int[]{60, 99});
        Student s2 = new Student("重", 15, new int[]{59, 100});
        Student s3 = new Student("山", 16, new int[]{60, 99});
        Student s4 = new Student("复", 17, new int[]{61, 100});
        Collections.addAll(students, s1, s2, s3, s4);

        // 找出年龄大于15岁的学生，并降序输出
        long count = students.stream().filter(s -> s.getAge() > 15)
                .count();
        System.out.println(count);

        // 找出平均分最高的学生对象，并输出
        Student max = students.stream().max(((o1, o2) -> Integer.compare(o1.getAge(), o2.getAge()))).get();
        System.out.println(max);

        // 找出平均分最低的学生对象，并输出
        Student min = students.stream().min(((o1, o2) -> Integer.compare(o1.getAge(), o2.getAge()))).get();
        System.out.println(min);

        // 找出年龄大于16岁的学生对象，放到一个新集合中返回
        List<Student> collect1 = students.stream().filter(a -> a.getAge() > 16).collect(Collectors.toList());
        System.out.println(collect1);

        Set<Student> collect2 = students.stream().filter(a -> a.getAge() > 16).collect(Collectors.toSet());
        System.out.println(collect2);

        // 找出年龄小于16岁的学生对象，放到一个新集合或数组中返回
        Map<String, Integer> collect3 =
                students.stream().filter(a -> a.getAge() < 16).collect(Collectors.toMap(Student::getName, Student::getAge));
        System.out.println(collect3);

        Object[] collect4 = students.stream().filter(a -> a.getAge() < 16).toArray();
        System.out.println(Arrays.toString(collect4));
    }
}
```

打印结果

```Plain
3
Student{name='复', age=17, scores=[61, 100]}
Student{name='重', age=15, scores=[59, 100]}
[Student{name='复', age=17, scores=[61, 100]}]
[Student{name='复', age=17, scores=[61, 100]}]
{重=15}
[Student{name='重', age=15, scores=[59, 100]}]
```

# 总结

1.Lambda表达式

(被重写方法的形参列表) -> {

被重写方法的方法体代码

}

2.方法引用

静态方法引用  类名::静态方法

实例方法引用  对象名::实例方法

特定类型方法引用  类型::方法

3.Stream流的常用api多用就熟悉了