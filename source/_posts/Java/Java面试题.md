---
title: Java面试题
date: 2021-03-15 10:23:53
tags: [Java]
categories: Java
---

<meta name="referrer" content="no-referrer"/>
<!-- more -->

# JavaSE

## 自增变量

```java
 public static void main(String[] args) {
        int i = 1;
        i = i++;
        int j = i++;
        int k = i + ++i * i++;
        System.out.println("i=" + i); // 4	
        System.out.println("j=" + j); // 1
        System.out.println("k=" + k); // 11 2+3*3
}
```

## 单例模式

Singleton：单例设计模式，即某个类在整个系统中只能有一个实例对象可被获取和使用的代码模式

1. 某个类只能有一个实例
	构造器私有化
2. 他必须自行创建实例
	自行创建，并且用静态变量保存
3. 必须自行向整个系统提供这个实例
    - 直接暴露(public)
    - 用静态变量的get方法
    

饿汉式 直接实例化

```java
public class Singleton1 {
    /**
     * 1、构造器私有化
     * 2、自行创建，并且用静态变量保存
     * 3、向外提供实例
     * 4、强调这是一个单例，我们可以用final修改
     */
    private Singleton1() {

    }
    public static final Singleton1 INSTANCE = new Singleton1();

}
```

懒汉式 单线程

```java
public class Singleton4 {
    /**
     * 1、构造器私有化
     * 2、用一个静态变量保存这个唯一的实例
     * 3、提供一个静态方法，获取这个实例对象
     */
    static Singleton4 instance;
    private Singleton4() {}

    public static Singleton4 getInstance() {
            if (instance == null) {
                instance = new Singleton4();
            }
            return instance;

    }
}
```

## 方法参数传递机制

```java
import java.util.Arrays;

public class Main {
	
    public static void main(String[] args) {
        int i = 1;
        String str = "hello";
        Integer num = 200;
        int[] arr = {1,2,3,4,5};
        MyData my = new MyData(); // 10

        change(i,str,num,arr,my);

        System.out.println("i= " + i); // 1
        System.out.println("str= " + str); // hello
        System.out.println("num= " + num); // 200
        System.out.println("arr= " + Arrays.toString(arr)); // 2,2,3,4,5
        System.out.println("my.a= " + my.a); // 11
    }
    
    public static void change(int j, String s, Integer n, int[] a, MyData m) {
        j += 1;
        s += "world";
        n += 1;
        a[0] += 1;
        m.a += 1;
    }
}
class MyData {
    int a = 10;
}
```

实参给形参赋值：

基本数据类型：数据值

引用数据类型：地址值 特殊类型：String、包装类对象具有不变性



Java语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

```
byte short int long float double char boolean
8	 16    32   64  32	  64 	 16   1
```

## 递归与迭代

> 有 n 步台阶，一次只能上 1 步或者 2 步，共有多少种走法？

```java
public class Step {

    @Test
    public void test() {
        long start = System.currentTimeMillis();
        System.out.println(iteration(40)); 
        long end = System.currentTimeMillis(); 
        System.out.println(end - start);
    }

    // 递归实现
    public int recursion(int n) {
      if(n < 1) {
          return 0;
      }
      if(n == 1 || n == 2) {
          return n;
      }
      return recursion(n - 2) + recursion( n - 1);
    }

    // 迭代实现
    // one 最后走一步 的走法 有：1 1 1, 2 1
    // two 最后走两步 的走法 有：1 2
    public int iteration(int n) {
        if(n < 1) {
            return 0;
        }
        if(n == 1 || n == 2) {
            return n;
        }
        int two = 1; // 一层台阶，有 1 走法, n 的前两层台阶的走法
        int one = 2; // 二层台阶，有 2 走法, n 的前一层台阶的走法
        int sum = 0; // 记录一共有多少中走法
        for(int i = 3; i <= n; i++) {
                sum = two + one;
                two = one;
                one = sum;
        }
        return sum;
    }
}
```

1. **递归** 当 n 等于 1 或者 2 时，走法就等于 n，从第三层台阶开始，每一层台阶为前两层台阶走法之和。
2. **迭代** 用 one、two 这两个变量来存储 n 的最后走一步和最后走两步，从第三层开始走，用 sum 来保存前两次的走法的次数，sum = two + one; 然后 two 移到 one，one 移到 sum 循环迭代。

总结：
1）方法调用自身称为递归，利用变量的原值推出新值称为迭代。
2）递归
优点：大问题转化为小问题，可以减少代码量，同时代码精简，可读性好；
缺点：递归调用浪费了空间，而且递归太深容易造成堆栈的溢出。
3）迭代
优点：代码运行效率好，因为时间复杂度为 O(n)，而且没有额为空间的开销；
缺点：代码不如递归简洁。

## 成员变量与局部变量

```java
/**
 * 成员变量和局部变量
 */
public class Exam6 {

    public static int s; // 成员变量，类变量
    int i; // 成员变量，实例变量
    int j; // 成员变量，实例变量

    {
        int i = 1;  // 非静态代码块中的局部变量
        i++;
        j++;
        s++;
    }

    public void test(int j) { // 局部变量
        j++;
        i++;
        s++;
    }

    public static void main(String[] args) { // 局部变量
        Exam6 obj1 = new Exam6(); // 局部变量
        Exam6 obj2 = new Exam6(); // 局部变量

        obj1.test(10);
        obj1.test(20);
        obj2.test(30);

        System.out.println(obj1.i + "," + obj1.j + "," + obj1.s); // 2 1 5
        System.out.println(obj2.i + "," + obj2.j + "," + obj2.s); // 1 1 5
    }
}
```

### 考点

1）就近原则
2）变量的分类

- 成员变量：类变量、实例变量
- 局部变量

3）非静态代码块的执行：每次创建实例对象都会执行
4）方法的调用规则：调用一次执行一次

### 区别

1）声明的位置
局部变量：方法体 { } 中、代码块 { } 中、形参
成员变量：类中的**方法外**

- **类变量 ：有 static 修饰**
- 实例变量：没有 static 修饰

2）修饰符
局部变量：final
成员变量：public、protected、private、final、static、volatile、transient

3）值存储的位置
局部变量：栈
实例变量：堆
类变量：方法区

4）作用域
局部变量：声明处开始，到所属的 } 结束
实例变量：在当前类中 `this.`（有时this. 可以省略），在其他类中 “对象名. ” 访问
类变量：在当前类中 `类名.`（有时类名. 可以省略），在其它类中 “类名.” 或 “对象名.” 访问

5）生命周期
局部变量：每一个线程，每一次调用执行都是新的生命周期
实例变量：随着对象的创建而初始化，随着对象的被回收而消亡，每一个对象的实例变量都是独立的
类变量：随着类的初始化而初始化，随着类的卸载而消亡，该类的所有对象的类变量是共享的