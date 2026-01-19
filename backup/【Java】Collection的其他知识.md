

个人主页：https://github.com/zbhgis

[TOC]



# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m

# 内容概览

1.本文内容主要包括可变参数，Collection的一些api，以及一个综合案例的实现

2.笔记对应视频142~144节

# 更新记录

无

# 可变参数

一种特殊形参，定义在方法、构造器的形参列表，可以不传数据，或传单个或多个数据，或传数组

数据类型...参数名称

注意事项：

可变参数本质是一个数组；一个形参列表中可变参数只有有一个，并放在最后

Sets5.java

```Java
package com.zbhgis.sets;

import java.util.Arrays;

public class Sets5 {
    public static void main(String[] args) {
        test();
        test(1);
        test(1, 2, 3);
        test(new int[]{1, 2, 3, 4});
    }

    private static void test(int... num) {
        System.out.println(num.length);
        System.out.println(Arrays.toString(num));
    }
}
```

打印结果

```Plain
0
[]
1
[1]
3
[1, 2, 3]
4
[1, 2, 3, 4]
```

# Collection常用的静态方法 

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202601152023821.png)

Sets6.java

```Java
package com.zbhgis.sets;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Sets6 {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        Collections.addAll(list, 7, 4, 1, 8, 5, 2);
        System.out.println(list);

        Collections.shuffle(list);
        System.out.println(list);
        Collections.shuffle(list);
        System.out.println(list);

        Collections.sort(list);
        System.out.println(list);
    }
}
```

打印结果

```Plain
[7, 4, 1, 8, 5, 2]
[4, 2, 8, 7, 1, 5]
[7, 5, 4, 8, 2, 1]
[1, 2, 4, 5, 7, 8]
```

# 综合案例

斗地主案例的实现

Card.java

```Java
package com.zbhgis.sets;

public class Card {
    private String number;
    private String color;
    private int size;

    public Card() {
    }

    public Card(String number, String color, int size) {
        this.number = number;
        this.color = color;
        this.size = size;
    }

    @Override
    public String toString() {
        return color + number;
    }

    public String getNumber() {
        return number;
    }

    public void setNumber(String number) {
        this.number = number;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public int getSize() {
        return size;
    }

    public void setSize(int size) {
        this.size = size;
    }
}
```

Room.java

```Java
package com.zbhgis.sets;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class Room {
    private List<Card> allCards = new ArrayList<>();

    public Room() {
        String[] numbers = {"3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"};
        String[] colors = {"♠", "♥", "♣", "♦"};
        int size = 0;

        for (String number : numbers) {
            size++;
            for (String color : colors) {
                Card c = new Card(number, color, size);
                allCards.add(c);
            }
        }
        Card c1 = new Card("", "S", ++size);
        Card c2 = new Card("", "B", ++size);
        Collections.addAll(allCards, c1, c2);
        System.out.println("新牌：" + allCards);
    }

    public void start() {
        // 洗牌
        Collections.shuffle(allCards);
        System.out.println("洗牌后：" + allCards);

        List<Card> P1 = new ArrayList<>();
        List<Card> P2 = new ArrayList<>();
        List<Card> P3 = new ArrayList<>();

        // 发牌
        for (int i = 0; i < allCards.size() - 3; ) {
            Card c1 = allCards.get(i++);
            P1.add(c1);
            Card c2 = allCards.get(i++);
            P2.add(c2);
            Card c3 = allCards.get(i++);
            P3.add(c3);
        }

        // 给玩家的牌排序
        sortCard(P1);
        sortCard(P2);
        sortCard(P3);

        // 看牌
        System.out.println("P1" + P1);
        System.out.println("P2" + P2);
        System.out.println("P3" + P3);

        // 最后三张牌
        List<Card> lastThreeCards = allCards.subList(allCards.size() - 3, allCards.size());
        System.out.println("底牌：" + lastThreeCards);

        // 抢地主
        P1.addAll(lastThreeCards);
        sortCard(P1);
        System.out.println("P1新牌：" + P1);
    }

    private void sortCard(List<Card> cards) {
        Collections.sort(cards, new Comparator<Card>() {
            @Override
            public int compare(Card o1, Card o2) {
                return o2.getSize() - o1.getSize();
            }
        });
    }
}
```

GameDemo.java

```Java
package com.zbhgis.sets;

public class GameDemo {
    public static void main(String[] args) {
        Room m = new Room();
        m.start();
    }
}
```

打印结果

```Plain
新牌：[♠3, ♥3, ♣3, ♦3, ♠4, ♥4, ♣4, ♦4, ♠5, ♥5, ♣5, ♦5, ♠6, ♥6, ♣6, ♦6, ♠7, ♥7, ♣7, ♦7, ♠8, ♥8, ♣8, ♦8, ♠9, ♥9, ♣9, ♦9, ♠10, ♥10, ♣10, ♦10, ♠J, ♥J, ♣J, ♦J, ♠Q, ♥Q, ♣Q, ♦Q, ♠K, ♥K, ♣K, ♦K, ♠A, ♥A, ♣A, ♦A, ♠2, ♥2, ♣2, ♦2, S, B]
洗牌后：[♥5, ♣K, ♥J, ♣4, B, ♣5, ♣6, ♠10, ♥3, ♣3, S, ♦8, ♦6, ♥10, ♥A, ♣A, ♦J, ♥K, ♠8, ♥2, ♦7, ♥8, ♦K, ♣Q, ♦4, ♣J, ♠J, ♦Q, ♣7, ♠5, ♠4, ♦9, ♠3, ♣8, ♦5, ♣10, ♣9, ♠2, ♠7, ♥Q, ♦3, ♠6, ♠A, ♦10, ♥9, ♦A, ♦2, ♥7, ♥4, ♠K, ♣2, ♠9, ♠Q, ♥6]
P1[♣A, ♠A, ♦A, ♦Q, ♥Q, ♣9, ♠8, ♥8, ♣8, ♣6, ♦6, ♥5, ♣4, ♦4, ♠4, ♥4, ♣3]
P2[B, S, ♥2, ♠2, ♦2, ♣K, ♦K, ♠K, ♦J, ♣J, ♠10, ♥10, ♦10, ♦9, ♣7, ♦5, ♦3]
P3[♣2, ♥A, ♥K, ♣Q, ♥J, ♠J, ♣10, ♥9, ♦8, ♦7, ♠7, ♥7, ♠6, ♣5, ♠5, ♥3, ♠3]
底牌：[♠9, ♠Q, ♥6]
P1新牌：[♣A, ♠A, ♦A, ♦Q, ♥Q, ♠Q, ♣9, ♠9, ♠8, ♥8, ♣8, ♣6, ♦6, ♥6, ♥5, ♣4, ♦4, ♠4, ♥4, ♣3]
```

# 总结

这些api多练就会了