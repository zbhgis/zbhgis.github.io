
个人主页：https://github.com/zbhgis

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括不同list的特点，以及List和LinkedList的常见用法

2.笔记对应视频138-139节

# 更新记录

无

# 特点

## ArrayList

- 有序，可重复，有索引
- 查询快，增删慢
- 利用无参构造器创建的集合，会在底层创建一个默认长度为0的数组
- 添加第一个元素时，底层会创建一个新的长度为10的数组
- 存满时，会扩容1.5倍
- 一次性添加多个元素，1.5倍还放不下，则新创建数组的长度以实际为准

## LinkedList

- 有序，可重复，有索引
- 查询慢，增删快，但对首尾元素进行增删改查的速度是极快的
- 基于双链表实现，可用于设计队列或栈

# List

除以下方法外，List也继承了Collection的功能

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131009449.png)

Lists1.java

```Java
package com.zbhgis.lists;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class Lists1 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("山");
        list.add("重");
        list.add("水");
        list.add("复");

        list.add(4, "疑");
        System.out.println(list);

        System.out.println(list.remove(4));
        System.out.println(list);

        System.out.println(list.get(1));
        System.out.println(list.set(0, "3"));
        System.out.println(list);


        for (int i = 0; i < list.size(); i++) {
            String s = list.get(i);
            System.out.print(s);
        }
        System.out.println();

        Iterator<String> it = list.iterator();
        while (it.hasNext()) {
            System.out.print(it.next());
        }
        System.out.println();

        for (String s : list) {
            System.out.print(s);
        }
        System.out.println();

        list.forEach(System.out::print);
        System.out.println();
    }
}
```

打印结果

```Plain
[山, 重, 水, 复, 疑]
疑
[山, 重, 水, 复]
重
山
[3, 重, 水, 复]
3重水复
3重水复
3重水复
3重水复
```

# LinkedList

LinkedList的新增方法

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601131009470.png)

Lists2.java

```Java
package com.zbhgis.lists;

import java.util.LinkedList;

public class Lists2 {
    public static void main(String[] args) {
        // 设计队列，先进先出，后进后出
        LinkedList<String> queue = new LinkedList<>();
        queue.addLast("1");
        queue.addLast("2");
        queue.addLast("3");
        queue.addLast("4");
        System.out.println(queue);

        System.out.println(queue.removeFirst());
        System.out.println(queue.removeFirst());
        System.out.println(queue.removeFirst());
        System.out.println(queue);

        // 设计栈，后进先出，先进后出
        LinkedList<String> stack = new LinkedList<>();
        // 或者stack.push("1");
        stack.addFirst("1");
        stack.addFirst("2");
        stack.addFirst("3");
        stack.addFirst("4");
        System.out.println(stack);

        // 或者stack.pop();
        System.out.println(stack.removeLast());
        System.out.println(stack.removeLast());
        System.out.println(stack.removeLast());
        System.out.println(stack);
    }
}
```

打印结果

```Plain
[1, 2, 3, 4]
1
2
3
[4]
[4, 3, 2, 1]
1
2
3
[4]
```

# 总结