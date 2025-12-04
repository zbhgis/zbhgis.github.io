


# 前言

1.之前学过，因此本文是个人复习笔记，为视频的总结以及个人思考，可能不是很详细。

2.教程是b站黑马程序员的JAVASE基础课程，笔记中的大部分图片来自于视频中的PPT截图。

3.Java环境为Java SE 17.0.3.1，IntelliJ IDEA版本为2025.2

https://www.bilibili.com/video/BV1Cv411372m/?vd_source=3b69b85b41f42a9e26b3a8a195228a36

# 内容概览

1.本文内容主要包括数组的基本使用与操作

2.笔记对应视频54-61节

# 更新记录

无

# 方法的创建

方法是一种结构，可以把一段代码封装成一个功能，以便重复调用，即函数。

修饰符 返回值类型 方法名(形参列表){

...

return 返回值;

}

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512042144097.png)

形参不能给初始值；其存在可有可无；多个形参必须用英文逗号隔开；

方法有几个形参，调用方法的时候就要传几个形参；

如果返回值类型为void，则不需要return；

方法在类中放前或后都可以，但是一个方法不能定义在另一个方法。

方法中return下面的语句为无效代码。

```Java
package com.zbhgis.method;

public class MethodDemo1 {
    public static void main(String[] args) {
        printHello();
        System.out.println();
        printHellos(3);
        System.out.println();
        System.out.println(getHello());
        System.out.println();
        System.out.println(getHellos(3));
        System.out.println();
    }

    public static void printHello(){
        System.out.println("Hello");
    }

    public static void printHellos(int times){
        for (int i = 0; i < times; i++) {
            System.out.println("Hello");
        }
    }

    public static String getHello(){
        return "Hello";
    }

    public static String getHellos(int times){
        String s = "";
        for (int i = 0; i < times; i++) {
            s += "Hello\n";
        }

        return s;
    }
}
```

打印结果

```Plain
Hello

Hello
Hello
Hello

Hello

Hello
Hello
Hello
```

## 方法的执行原理

方法在栈内存中执行，先进后出，保证一个方法调用完另一个方法后可以回来。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512042144291.png)

基本类型的参数传递是值传递，传输的是实参存储的值的副本。

先把类及其中定义的方法加载到方法区，main方法先执行，首先进入栈内存，先定义变量a等于10，将a其中的值拷贝到方法的形参中；之后执行change()，change()加载到栈内存中，此时change接收到的值为10，在该方法中打印a的值为10，将方法中的a赋值为20，再次打印a的值为20；此时change()执行完毕在栈内存中清理，继续执行main()，打印main()中a的值为10，main()执行完毕在栈内存中清理。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512042144652.png)

引用类型的参数传递是值传递，传输的是指向实参的地址值。

先把类及其中定义的方法加载到方法区，main方法先执行，首先进入栈内存，先定义变量arrs等于{10,20,30}，即在堆内存中开辟空间，将堆内存中的地址传给栈内存中的arrs，再将arrs其中的值，即地址拷贝到方法的形参中；之后执行change()，change()加载到栈内存中，此时change接收到的值为数组地址，在该方法中打印arrs[1]的值为20，将arrs[1]指向的数组元素赋值为222，再次打印arrs[1]的值为222；此时change()执行完毕在栈内存中清理，继续执行main()，打印main()中arrs[1]指向的数组算，由于其已经被改变为222，因此打印结果也为222，main()执行完毕在栈内存中清理。

![img](https://cdn.jsdelivr.net/gh/zbhgis/BlogImg@main/blog/202512042144340.png)

```Java
package com.zbhgis.method;

public class MethodDemo2 {
    public static void main(String[] args) {
        int a = 10;
        int[] arr = {10, 20, 30};
        changeInt(a);
        System.out.println("main:" + a);
        System.out.println();
        changeInt(arr[2]);
        System.out.println("main:" + arr[2]);
        System.out.println();
        changeArr(arr);
        System.out.println("main:" + arr[0]);
    }

    public static void changeInt(int a) {
        System.out.println("ChangeInt1:" + a);
        a = 20;
        System.out.println("ChangeInt2:" + a);
    }

    public static void changeArr(int[] arr) {
        System.out.println("ChangeArr1:" + arr[0]);
        arr[0] = 1;
        System.out.println("ChangeArr2:" + arr[0]);
    }
}
```

打印结果

```Plain
ChangeInt1:10
ChangeInt2:20
main:10

ChangeInt1:30
ChangeInt2:20
main:30

ChangeArr1:10
ChangeArr2:1
main:1
```

# 方法重载

一个类中，出现多个方法的名称相同，但是他们的形参列表（个数或类型或顺序）是不同的，即只与形参有关，那么这些方法就称为方法重载了。以下均是方法重载。

```Java
package com.zbhgis.method;

public class MethodDemo3 {
    public static void main(String[] args) {

    }

    public static void test() {

    }

    public static void test(int a) {

    }

    int test(int a, int b) {
        return 0;
    }

    void test(double a) {
        
    }

    void test(int b, double a) {

    }

    void test(double a, int b) {

    }
}
```

## return的单独使用

return; 可以用在无返回值的方法中，作用是立即跳出并结束当前方法的执行。

```Java
package com.zbhgis.method;

public class MethodDemo4 {
    public static void main(String[] args) {
        divide(10, 0);
        System.out.println();
        divide(10, 2);
    }

    public static void divide(int a, int b) {
        if (b == 0) {
            System.out.println("不可除");
            return;
        }
        int c = a / b;
        System.out.println("结果是：" + c);
    }
}
不可除

结果是：5
```

# 案例

## 求和

求某个范围内的整数之和

```Java
package com.zbhgis.method;

public class MethodDemo5 {
    public static void main(String[] args) {
        int start = 100;
        int end = 200;
        System.out.println(getSum(start, end));
    }

    private static int getSum(int start, int end) {
        int sum = 0;
        for (int i = start; i <= end; i++) {
            sum += i;
        }
        return sum;
    }
}
15150
```

## 数组比较

比较传入的两个数组是否相等

```Java
package com.zbhgis.method;

public class MethodDemo6 {
    public static void main(String[] args) {
        int[] arr1 = {};
        int[] arr2 = {};
        int[] arr3 = null;
        int[] arr4 = null;
        int[] arr5 = {1, 2, 4};
        int[] arr6 = {1, 2, 3};
        int[] arr7 = {1, 2, 4};

        System.out.println(isEqual(arr1, arr2));
        System.out.println(isEqual(arr1, arr3));
        System.out.println(isEqual(arr3, arr4));
        System.out.println(isEqual(arr5, arr6));
        System.out.println(isEqual(arr5, arr7));
    }

    public static boolean isEqual(int[] arr1, int[] arr2) {
        if(arr1 == null && arr2 == null){
            return true;
        }
        if(arr1 == null || arr2 == null){
            return false;
        }
        if(arr1.length != arr2.length){
            return false;
        }
        for (int i = 0; i < arr1.length; i++) {
            if (arr1[i] != arr2[i]) {
                return false;
            }
        }
        return true;
    }

}
true
false
true
false
true
```

## 方法重载案例

定义不同参数的方法输出自定义内容

```Java
package com.zbhgis.method;

public class MethodDemo7 {
    public static void main(String[] args) {
        win();
        win("我");
        win("我", 3);
    }

    public static void win() {
        System.out.println("赢了");
    }

    public static void win(String name) {
        System.out.println(name + "赢了");
    }

    public static void win(String name, int times) {
        System.out.println(name + "赢了" + times + "次");
    }
}
赢了
我赢了
我赢了3次
```

# 总结

1.方法在栈内存中执行，先进后出，保证一个方法调用完另一个方法后可以回来。

2.基本类型的参数传递，传递的是内容的副本；引用类型的参数传递，传递的是对象的地址。

3.方法重载是名称相同，但是形参列表不同。