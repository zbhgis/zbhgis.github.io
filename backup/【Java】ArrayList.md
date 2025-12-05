



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容包括ArrayList的创建、常用API与元素删除。

2.笔记对应视频80-83节

# 更新记录

无

# ArrayList的创建

ArrayList是一种集合，集合就是一种容器，用于存储数据。功能类似于数组。集合大小可变，而数组大小固定。可以直接打印，打印结果见下文。

1.未指定类型创建（不推荐）

在创建ArrayList集合的对象的时候，通过不指定这个具体的数据类型，那么这个ArrayList中可以存储多种数据类型。

```Java
package com.zbhgis.arraylist;

import java.util.ArrayList;

public class ArrayListDemo1 {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();
        list.add("test");
        list.add("123");
        list.add(123);
        list.add('\t');
        list.add((char) 48);
        list.add(new int[] {7, 8, 9});
        System.out.println(list);
    }
}
```

打印结果

```Plain
[test, 123, 123,         , 0, [I@776ec8df]
```

2.指定数据类型创建

在创建ArrayList集合的对象的时候，通过在<>中指定具体的数据类型，那么这个ArrayList中可以存储指定数据类型。

```Java
package com.zbhgis.arraylist;

import java.util.ArrayList;

public class ArrayListDemo2 {
    public static void main(String[] args) {
        // ArrayList<String> list = new ArrayList<String>();
        ArrayList<String> list = new ArrayList<>();
        list.add("test");
        list.add("123");
        list.add("好的");
        list.add("Java");
        System.out.println(list);
    }
}
```

打印结果

```Plain
[test, 123, 好的, Java]
```

# ArrayList的常用API

一些ArrayList的增删查改API

https://docs.oracle.com/en/java/javase/17/docs/api/index.html

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512052125302.png)

## 注意点

1.在指定位置添加数据时，即使用add(int index, E element)时，不返回结果。

2.在指定位置查询数据时，即使用get(int index)是，返回结果是查询到的数据，对原始ArrayList没影响

3.在指定位置删除数据时，即使用remove(int index)时，返回结果是被删除的原始元素

4.在指定位置修改数据时，即使用set(int index, E element)是，返回结果是被修改的原始元素

5.使用remove(Object o)时，如果ArrayList中有多个object内容相同，那么就remove掉第一个元素。

```Java
package com.zbhgis.arraylist;

import java.util.ArrayList;

public class ArrayListDemo3 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("123");
        list.add("test");
        list.add("123");
        list.add("好的");
        list.add("Java");
        list.add("123");
        System.out.println(list);

        list.add(1, "666");
        System.out.println(list);

        System.out.println(list.get(1));

        System.out.println(list.size());

        System.out.println(list.remove(3));
        System.out.println(list);

        list.remove("123");
        System.out.println(list);

        System.out.println(list.set(1, "000"));
        System.out.println(list);

    }
}
```

打印结果

```Plain
[123, test, 123, 好的, Java, 123]
[123, 666, test, 123, 好的, Java, 123]
666
7
123
[123, 666, test, 好的, Java, 123]
[666, test, 好的, Java, 123]
test
[666, 000, 好的, Java, 123]
```

# ArrayList的元素删除

创建一个ArrayList，然后添加若干元素之后，删除包含指定名称的元素。

由于ArrayList本身元素被删除之后，其内容会减少，容量变小了，对应索引也改变，因此使用常规方法直接从前往后遍历删除元素不可行。

方法一：删除元素后调整遍历的下标，往前移动。

方法二：从后往前遍历元素并删除。

方法三：创建一个相同内容的ArrayList，然后依次遍历ArrayList1，对ArrayList2进行删除操作。

```Java
package com.zbhgis.arraylist;

import java.util.ArrayList;

public class ArrayListDemo4 {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("3060显卡");
        list.add("AMD");
        list.add("5060显卡");
        list.add("显卡");
        list.add("Java教程");
        list.add("AirPods");
        list.add("4090显卡");
        ArrayList<String> list2 = new ArrayList<>(list);
        ArrayList<String> list3 = new ArrayList<>(list);
        ArrayList<String> list4 = new ArrayList<>(list);
        ArrayList<String> list5 = new ArrayList<>(list);


        // 方法一：对list遍历，remove后i左移一个
        System.out.println("list1");
        System.out.println(list);
        for (int i = 0; i < list.size(); i++) {
            String obj = list.get(i);
            if (obj.contains("显卡")) {
                list.remove(obj);
                i--;
            }
        }
        System.out.println(list);

        // 方法二：对list2遍历，从后往前remove
        System.out.println("list2");
        System.out.println(list2);
        for (int i = list2.size() - 1; i >= 0; i--) {
            String obj = list2.get(i);
            if (obj.contains("显卡"))
                list2.remove(obj);
        }
        System.out.println(list2);

        // 方法三：对list3遍历，但是对list4进行remove
        System.out.println("list3 & list4");
        System.out.println(list3);
        for (int i = 0; i < list3.size(); i++) {
            String obj = list3.get(i);
            if (obj.contains("显卡"))
                list4.remove(obj);
        }
        System.out.println(list4);

        // 错误：因为list本身元素被删除之后，其内容会改变，对应索引也改变
        System.out.println("list5");
        System.out.println(list5);
        for (int i = 0; i < list5.size(); i++) {
            String obj = list5.get(i);
            if (obj.contains("显卡"))
                list5.remove(obj);
        }
        System.out.println(list5);

    }
}
```

打印结果

```Plain
list1
[3060显卡, AMD, 5060显卡, 显卡, Java教程, AirPods, 4090显卡]
[AMD, Java教程, AirPods]
list2
[3060显卡, AMD, 5060显卡, 显卡, Java教程, AirPods, 4090显卡]
[AMD, Java教程, AirPods]
list3 & list4
[3060显卡, AMD, 5060显卡, 显卡, Java教程, AirPods, 4090显卡]
[AMD, Java教程, AirPods]
list5
[3060显卡, AMD, 5060显卡, 显卡, Java教程, AirPods, 4090显卡]
[AMD, 显卡, Java教程, AirPods]
```

# 总结

1.ArrayList是未指定数据类型的时候可以放入不同的数据类型元素。

2.ArrayList的长度是可变的，因此在进行遍历的时候需要留意。