
个人主页：https://github.com/zbhgis

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括集合体系与Collection的遍历方法

2.笔记对应视频136~137节

# 更新记录

无

# 集合体系

Collection 单列集合

Map 双列集合

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131007554.png)

集合特点 List集合：添加的元素是有序、可重复、有索引

- ArrayList、LinkedList：有序、可重复、有索引

Set集合：添加的元素是无序、不重复、无索引

- HashSet：无序、不重复、无索引
- LinkedHashSet：有序、不重复、无索引
- TreeSet：按照大小默认升序排序、不重复、无索引

Collections1.java

```Java
package com.zbhgis.collections;

import com.zbhgis.object3.A;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;
import java.util.Objects;

public class Collections1 {
    public static void main(String[] args) {
        Collection<String> c = new ArrayList<>();
        c.add("山");
        c.add("重");
        c.add("水");
        c.add("复");
        System.out.println(c);

        c.clear();
        System.out.println(c);

        System.out.println(c.isEmpty());
        System.out.println(c.size());

        c.add("山");
        c.add("重");
        c.add("水");
        c.add("复");
        System.out.println(c.contains("山"));
        System.out.println(c.contains(null));
        System.out.println(c.remove("山"));
        System.out.println(c);

        Object[] arr = c.toArray();
        System.out.println(Arrays.toString(arr));

        String[] arr2 = c.toArray(new String[c.size()]);
        System.out.println(Arrays.toString(arr2));

        // 把一个集合的数据全部添加到另一个集合中
        Collection<String> c1 = new ArrayList<>();
        c1.add("山");
        c1.add("重");
        Collection<String> c2 = new ArrayList<>();
        c2.add("水");
        c2.add("复");
        c1.addAll(c2);
        System.out.println(c1);
        System.out.println(c2);
    }
}
```

打印结果

```Plain
[山, 重, 水, 复]
[]
true
0
true
false
true
[重, 水, 复]
[重, 水, 复]
[重, 水, 复]
[山, 重, 水, 复]
[水, 复]
```

# Collection的遍历方式

## 三种方式

- 迭代器

来遍历集合的专用方式

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131006619.png)

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131007714.png)

- 增强for循环

增强for用来遍历集合或数组

- Lambda表达式

forEach方法

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131006656.png)

Collections2.java

```Java
package com.zbhgis.collections;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;
import java.util.function.Consumer;

public class Collections2 {
    public static void main(String[] args) {
        Collection<String> c = new ArrayList<>();
        c.add("山");
        c.add("重");
        c.add("水");
        c.add("复");
        System.out.println(c);

        // 迭代器
        Iterator<String> it = c.iterator();
        while (it.hasNext()) {
            System.out.print(it.next());
        }
        System.out.println();

        // 增强for循环
        for (String ele : c) {
            System.out.print(ele);
        }
        System.out.println();

        // Lambda表达式
        c.forEach(new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.print(s);
            }
        });
        System.out.println();
        c.forEach((String s) -> {
                System.out.print(s);
        });
        System.out.println();
        c.forEach(s ->{
            System.out.print(s);
        });
        System.out.println();
        c.forEach(System.out::print);
        System.out.println();
    }
}
```

打印结果

```Plain
[山, 重, 水, 复]
山重水复
山重水复
山重水复
山重水复
山重水复
山重水复
```

## 案例

实现电影的存储与查找

Movie.java

```Java
package com.zbhgis.collections;

public class Movie {
    private String name;
    private double score;
    private String actor;

    public Movie() {
    }

    public Movie(String name, double score, String actor) {
        this.name = name;
        this.score = score;
        this.actor = actor;
    }

    @Override
    public String toString() {
        return "Movie{" +
                "name='" + name + '\'' +
                ", score=" + score +
                ", actor='" + actor + '\'' +
                '}';
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }

    public String getActor() {
        return actor;
    }

    public void setActor(String actor) {
        this.actor = actor;
    }
}
```

Collections3.java

```Java
package com.zbhgis.collections;

import java.util.ArrayList;
import java.util.Collection;

public class Collections3 {
    public static void main(String[] args) {
        Collection<Movie> movies = new ArrayList<>();
        movies.add(new Movie("肖申克的救赎", 9.7, "罗宾斯"));
        movies.add(new Movie("霸王别姬", 9.6, "张国荣、张丰毅"));
        movies.add(new Movie("阿甘正传", 9.5, "汤姆·汉克斯"));

        for (Movie movie : movies) {
            System.out.println("电影名：" + movie.getName());
            System.out.println("评分：" + movie.getScore());
            System.out.println("主演：" + movie.getActor());
        }
    }
}
```

打印结果

```Plain
电影名：肖申克的救赎
评分：9.7
主演：罗宾斯
电影名：霸王别姬
评分：9.6
主演：张国荣、张丰毅
电影名：阿甘正传
评分：9.5
主演：汤姆·汉克斯
```

执行原理

先在栈内存中加载main方法，并创建变量movies，在堆内存中开辟空间，准备存储ArrayList，并将当前地址传给movies变量进行存储；在movies中添加新的对象时，先在堆内存中开辟空间，将新的对象的地址传入到movies对应的地址中进行存储；最后打印时，获取movies中某个地址指向的对象，并获取其信息打印。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131006754.png)