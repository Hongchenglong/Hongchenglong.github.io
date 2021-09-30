---
title: Java面经
date: 2021-02-09 13:11:16
tags:
categories:
---

<meta name="referrer" content="no-referrer"/>
<!-- more -->

# Java SE

## Java基础（一）

### Java和PHP的区别？

PHP专注于Web开发，在Web后台开发PHP优于Java；Java比较全面，在数据库访问方面强于PHP。

Java适合于开发大型的应用系统，应用的前景比较广阔，系统易维护、可复用性较好。

### 简单描述一下正则表达式及其用途。

在编写处理字符串的程序时，经常需要**查找符合某些复杂规则的字符串**。正则表达式就是用于描述这些规则的工具。

### Java中是如何支持正则表达式操作的？

Java中的`String`类提供了支持正则表达式操作的方法，包括：matches()、replaceAll()、replaceFirst()、split()。此外，Java中可以用`Pattern`类表示正则表达式对象，它提供了丰富的API进行各种正则表达式操作，如compile。

### 比较一下Java和JavaSciprt？

Java与JavaScript是两个公司开发的不同的两个产品。

- 面向对象和基于对象

Java是一种真正的面向对象的语言，即使是开发简单的程序，必须设计对象；

JavaScript是基于对象（Object-Based）和事件驱动（Event-Driven）的编程语言，用来制作与网络无关的，与用户交互作用的复杂软件。

- 编译和解释

Java的源代码在执行之前，必须经过编译；

JavaScript无需编译，由浏览器解释执行。

- 强类型和弱类型变量

Java采用强类型变量检查，即所有变量在编译之前必须作声明；

JavaScript中变量是弱类型的，甚至在使用变量前可以不作声明，在运行时检查推断其数据类型。

### Java中如何跳出当前的多重嵌套循环？

在最外层循环前加一个标记如A，然后用`break A`，可以跳出多重循环，类似goto。

### &和&&的区别？

&运算符有两种用法：(1)按位与&；(2)逻辑与&&。

&&运算符是**短路与**运算。如果&&左边的表达式的值是false，右边的表达式会被直接短路掉，不会进行运算。

### int和Integer有什么区别？

Java是一个近乎纯洁的面向对象编程语言，==为了编程的方便引入了基本数据类型==，但是为了能够将这些基本数据类型当成==对象==操作，Java为每一个基本数据类型都引入了对应的==包装类型==（wrapper class），**int的包装类就是Integer**，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以**相互转换**。

### 在web应用开发过程中经常遇到输出某种编码的字符，如iso8859-1等，请你讲讲如何输出一个某种编码的字符串？

`String str = new String("字符串".getBytes("ISO-8859-1"), "GBK");`

### String和StringBuffer的区别

String类为不可变对象，每次操作String都会建立新的对象来保存新的值。

StringBuffer是可变对象，实例化后，只对这一个对象操作。

### String是最基本的数据类型吗?

基本数据类型包括byte、short、int、long、float、double、char、boolean。

java.lang.String类是final类型的，因此不可以继承这个类、不能修改这个类。为了提高效率节省空间，我们应该用StringBuffer类。

## Java基础（二）

###  请你谈谈大O符号(big-O notation)并给出不同数据结构的例子

大O符号表示一个程序运行时所需要的渐进时间复杂度上界。

### 请你讲讲数组(Array)和列表(ArrayList)的区别？什么时候应该使用Array而不是ArrayList？

Array和ArrayList的不同点：
Array可以包含基本类型和对象类型，ArrayList只能包含对象类型。
Array大小是固定的，ArrayList的大小是动态变化的。
ArrayList提供了更多的方法和特性，比如：addAll()，removeAll()，iterator()等等。

对于基本类型数据，集合使用自动装箱来减少编码工作量。但是，当处理固定大小的基本数据类型的时候，这种方式相对比较慢。

### 请你解释什么是值传递和引用传递？

值传递是对基本型变量而言的,传递的是该变量的一个副本,改变副本不影响原变量.
引用传递一般是对于对象型变量而言的,传递的是该对象地址的一个副本, 并不是原对象本身。所以对引用对象进行操作会同时改变原对象。

### 请你讲讲Java支持的数据类型有哪些？什么是自动拆装箱？

基本数据类型包括byte、short、int、long、float、double、boolean、char。

自动装箱是Java编译器在基本数据类型和对应的对象包装类型之间做的一个转化。比如：把int转化成Integer，double转化成Double，等等。反之就是自动拆箱。

###  请你解释为什么会出现4.0-3.6=0.40000001这种现象？

2进制的小数无法精确的表达10进制小数，计算机在计算10进制小数的过程中要先转换为2进制进行计算，这个过程中出现了误差。

### 请你讲讲一个十进制的数在内存中是怎么存的？

补码的形式。

### Lamda表达式的优缺点。

优点：1. 简洁。2. 非常容易并行计算。3. 可能代表未来的编程趋势。

缺点：1. 若不用并行计算，很多时候计算速度没有比传统的 for 循环快。（并行计算有时需要预热才显示出效率优势）2. 不容易调试。3. 若其他程序员没有学过 lambda 表达式，代码不容易让其他语言的程序员看懂。

```java
public int add(int x, int y) {
    return x + y;
}

(int x, int y) -> x + y 
```



### java8的新特性，请简单介绍一下

Lambda 表达式：Lambda允许把函数作为一个方法的参数

方法引用：可以直接引用已有Java类或对象（实例）的方法或构造器。

默认方法：一个在接口里面有了一个实现的方法。

### 说明符号“==”比较的是什么？

`==`对比两个对象基于内存引用，如果两个对象的引用完全相同（指向同一个对象）时，`==`操作将返回true，否则返回false。

`==`如果两边是基本类型，就是比较数值是否相等。

### 解释Object若不重写hashCode()的话，hashCode()如何计算出来的？

Object 的 hashcode 方法是本地方法，用C\C++实现的，该方法直接返回对象的 内存地址。

### 介绍一下map的分类和常见的情况

java为数据结构中的映射定义了一个接口java.util.Map;它有四个实现类,分别是HashMap、Hashtable、 LinkedHashMap和TreeMap.

`Map`主要用于存储健值对，根据键得到值，因此不允许键重复(重复了覆盖了),但允许值重复。

`Hashmap`是一个最常用的Map,它根据键的HashCode值存储数据,根据键可以直接获取它的值，具有很快的访问速度，遍历时，取得数据的顺序是完全随机的。 HashMap最多只允许一条记录的键为Null;允许多条记录的值为 Null;HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap;可能会导致数据的不一致。如果需要同步，可以用 Collections的synchronizedMap方法使HashMap具有同步的能力，或者使用ConcurrentHashMap。

`Hashtable`与 HashMap类似,它继承自Dictionary类，不同的是:它不允许记录的键或者值为空;它支持线程的同步，即任一时刻只有一个线程能写Hashtable,因此也导致了 Hashtable在写入时会比较慢。

`LinkedHashMap`是HashMap的一个子类，保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的.也可以在构造时用带参数，按照应用次数排序。在遍历的时候会比HashMap慢，不过有种情况例外，当HashMap容量很大，实际数据较少时，遍历起来可能会比 LinkedHashMap慢，因为LinkedHashMap的遍历速度只和实际数据有关，和容量无关，而HashMap的遍历速度和他的容量有关。

`TreeMap`实现SortMap接口，能够把它保存的记录根据键排序,默认是按键值的升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。

### 自增变量

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

### 单例模式

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

### 方法参数传递机制

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

### 递归与迭代

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

### 成员变量与局部变量

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

#### 考点

1）就近原则
2）变量的分类

- 成员变量：类变量、实例变量
- 局部变量

3）非静态代码块的执行：每次创建实例对象都会执行
4）方法的调用规则：调用一次执行一次

#### 区别

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

## 关键字

### Java里面的final关键字是怎么用的？

当用final修饰一个类时，表明这个类不能被继承；如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。

### 关于Synchronized和lock 

synchronized(同步)是Java的关键字，当它用来修饰一个方法或代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。

Lock是一个接口。

### 介绍一下volatile？

volatile关键字是用来保证有序性和可见性的。

### 请你介绍一下Syncronized锁，如果用这个关键字修饰一个静态方法，锁住了什么？如果修饰成员方法，锁住了什么？

...

## 面向对象（一）

###  若对一个类不重写，它的equals()方法是如何比较的？

比较对象的地址。

### 解释hashCode()和equals()方法有什么联系？

➀相等的对象必须具有相等的哈希码（散列码）。

➁如果两个对象的hashCode相同，它们并不一定相同。

### 什么是构造函数？什么是构造函数重载？什么是复制构造函数？

构造函数，即构造方法，用于创建对象时初始化对象。与类同名，无返回值。

构造函数重载：可以为一个类创建多个构造函数，每个构造函数必须有它自己唯一的参数列表。

...

### 方法重载(Overloading)和方法覆盖(Overriding)是什么意思？

方法重载：同一个类里面两个或者是多个方法的**方法名相同但是参数不同**的情况。

方法覆盖（重写）是说子类重新定义了父类的方法。方法覆盖必须有相同的方法名，返回类型和参数列表。覆盖者可能不会限制它所覆盖的方法的访问。

### 请说明Query接口的list方法和iterate方法有什么区别？

...

### 面向对象的"六原则一法则"

1. 单一职责原则：一个类只做它该做的事情。
2. 开闭原则：软件实体应当对扩展开放，对修改关闭。
3. 依赖倒转原则：面向接口编程。
4. 里氏替换原则：任何时候都可以用子类型替换掉父类型。
5. 接口隔离原则：接口要小而专，绝不能大而全。
6. 合成聚合复用原则：优先使用聚合或合成关系复用代码。
7. 迪米特法则：迪米特法则又叫最少知识原则，一个对象应当对其他对象有尽可能少的了解。

### 如何通过反射获取和设置对象私有字段的值？

...

### 说明重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？

方法的重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多态性，而后者实现的是运行时的多态性。

重载发生在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同或者二者都不同）则视为重载；重写（覆盖）发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的返回类型，比父类被重写方法更好访问，不能比父类被重写方法声明更多的异常（里氏代换原则）。

重载对返回类型没有特殊的要求。

### 两个对象值相同(x.equals(y) == true)，但却可有不同的hash code，该说法是否正确，为什么？

不对，如果两个对象x和y满足x.equals(y) == true，它们的哈希码（hash code）应当相同。Java对于eqauls方法和hashCode方法是这样规定的：(1)如果两个对象相同（equals方法返回true），那么它们的hashCode值一定要相同；(2)如果两个对象的hashCode相同，它们并不一定相同。

当然，你未必要按照要求去做，但是如果你违背了上述原则就会发现在使用容器时，相同的对象可以出现在Set集合中，同时增加新元素的效率会大大下降（对于使用哈希存储的系统，如果哈希码频繁的冲突将会造成存取性能急剧下降）。

### 内部类可以引用他包含类的成员吗，如果可以，有没有什么限制吗？

一个内部类对象可以访问创建它的外部类对象的内容。

类如果不是static的，那么它可以访问创建它的外部类对象的所有属性内部类；如果是static的，即为nested class，那么它只可以访问创建它的外部类对象的所有static属性一般普通类。

### Java语言如何进行异常处理，关键字：throws,throw,try,catch,finally分别代表什么意义？在try块中可以抛出异常吗？

一般情况下是用try来执行一段程序，如果出现异常，系统会抛出（throws）一个异常，这时候你可以通过它的类型来捕捉（catch）它，或最后（finally）由缺省处理器来处理。

用try来指定一块预防所有”异常”的程序。紧跟在try程序后面，应包含一个catch子句来指定你想要捕捉的”异常”的类型。throw语句用来明确地抛出一个”异常”。throws用来标明一个成员函数可能抛出的各种”异常”。finally为确保一段代码不管发生什么”异常”都被执行一段代码。

### 说明Java的接口和C++的虚类的相同和不同处。

...

### 判断当一个对象被当作参数传递给一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递?

???

值传递。Java只有值传递参数。当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。对象的内容可以在被调用的方法中改变，但对象的引用是永远不会改变的。

Java永远只有值传递，引用传递其实也是一个值传递，传递是一个地址的副本，

## 面向对象（二）

### interface和abstract class有什么区别?

1. 相同点
   两者都是抽象类，都不能实例化。

   interface实现类及abstrct class的子类都必须要实现已经声明的抽象方法。

2. 不同点

   interface需要实现，要用implements，而abstract class需要继承，要用extends。

   一个类可以实现多个interface，但一个类只能继承一个abstract class。

   interface强调特定功能的实现，而abstract class强调所属关系。

   尽管interface实现类及abstrct class的子类都必须要实现相应的抽象方法，但实现的形式不同。interface中的每一个方法都是抽象方法，都只是声明的 (declaration, 没有方法体)，实现类必须要实现。而abstract class的子类可以有选择地实现。

### Override和Overload的区别，Overloaded的方法是否可以改变返回值的类型?

方法的重写Override和重载Overload是Java多态性的不同表现。重写Override是父类与子类之间多态性的一种表现，重载Overload是一个类中多态性的一种表现。

重写是子类对父类方法的重新实现, 返回类型和参数列表都不能改变。
重载(overloading) 是在一个类里面，方法名相同，而参数不同。返回类型可以相同也可以不同。

### final, finally, finalize的区别

final 用于声明属性，方法和类，分别表示属性不可变，方法不可重写，类不可继承。
finally 是异常处理语句结构的一部分，表示总是执行。
finalize 是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源回收，例如关闭文件等。

### 面向对象的特征有哪些方面

1. 封装
	封装，即把过程和数据包围起来，对数据的访问只能通过已定义的界面。如私有变量，用set，get方法获取。封装保证了模块具有较好的独立性，使得程序维护修改较为容易。
2. 继承
	继承是一种联结类的层次模型，并且允许和鼓励类的重用，它提供了一种明确表述共性的方法。
3. 多态
	多态性是指允许不同类的对象对同一消息作出响应。
4. 抽象
	抽象，即忽略一个主题中与当前目标无关的那些方面，以便更充分地注意与当前目标有关的方面。

### Comparable和Comparator2个接口的作用和区别

作用：都是用来实现集合中元素的比较和排序

...

## 面向对象（三）

...

## 集合（一）

### 请说明List、Map、Set三个接口存取元素时，各有什么特点

List以特定索引来存取元素，可以有重复元素。Set不能存放重复元素（用对象的equals()方法来区分元素是否重复）。Map保存键值对（key-value pair）映射，映射关系可以是一对一或多对一。

### 阐述ArrayList、Vector、LinkedList的存储性能和特性

...

### 请判断List、Set、Map是否继承自Collection接口？

List、Set 是，Map 不是。Map是键值对映射容器，与List和Set有明显的区别，而Set存储的零散的元素且不允许有重复元素，List是线性结构的容器，适用于按数值索引访问元素的情形。

### 常用集合类以及主要方法？

List 的具体实现包括 ArrayList 和 Vector，它们是可变大小的列表，比较适合构建、存储和操作任何类型对象的元素列表。List 适用于按数值索引访问元素的情形。

Map 提供了一个更通用的元素存储方法。 Map 集合类用于存储元素对（称作"键"和"值"），其中每个键映射到一个值。

### Collection 和 Collections的区别

Collection是集合类的上级接口，继承与他的接口主要有Set 和List.
Collections是针对集合类的一个帮助类，他提供一系列静态方法实现对各种集合的搜索、排序、线程安全化等操作。

### HashMap和Hashtable的区别？ 

HashMap和Hashtable都实现了Map接口，因此很多特性非常相似。但是，他们有以下不同点：
HashMap允许键和值是null，而Hashtable不允许键或者值是null。
HashMap不是同步的，Hashtable是同步的。因此，HashMap更适合于单线程环境，而Hashtable适合于多线程环境。
HashMap提供了可供应用迭代的键的集合，因此，HashMap是快速失败的。另一方面，Hashtable提供了对键的列举(Enumeration)。

# Java Web

## Web编程基础

### JAVA应用服务器都有哪些？

Web服务器：Tomcat、Jetty

Java EE服务器：Bea Weblogic、JBoss

### 在什么情况下会使用assert？

assertion (断言)在软件开发中是一种常用的调试方式。

assertion检查通常在开发和测试时开启。在实现中，assertion就是在程序中的一条语句，它对一个 boolean表达式进行检查，一个正确程序必须保证这个boolean表达式的值为true。

### 1分钟之内只能处理1000个请求，你怎么实现，手撕代码?

限流的几种方法：计数器，滑动窗口、漏桶法、令牌桶

### 如何在链接里不输入项目名称的情况下启动项目？

在taomcat配置虚拟目录。

### JSP中的静态包含和动态包含的有哪些区别？

静态包含是通过JSP的include指令包含页面，动态包含是通过JSP标准动作<jsp:forward>包含页面。

静态包含是编译时包含，动态包含是运行时包含。

### 表达式语言（EL）的隐式对象以及该对象的作用

EL的隐式对象包括：pageContext、initParam（访问上下文参数）、param（访问请求参数）

### JSP有哪些内置对象？以及这些对象的作用分别是什么？

JSP有9个内置对象：
- request：封装客户端的请求，其中包含来自GET或POST请求的参数；
- response：封装服务器对客户端的响应；
- pageContext：通过该对象可以获取其他对象；
- session：封装用户会话的对象；
- application：封装服务器运行环境的对象；
- application：封装服务器运行环境的对象；
- out：输出服务器响应的输出流对象；
- config：Web应用的配置对象；
- page：JSP页面本身（相当于Java程序中的this）；
- exception：封装页面抛出异常的对象。

### 说说weblogic中一个Domain的缺省目录结构?比如要将一个简单的helloWorld.jsp放入何目录下,然后在浏览器上就可打入主机？

...

### JSP有哪些动作? 这些动作的作用又分别是什么?

JSP 共有以下6种基本动作 
jsp:include：在页面被请求的时候引入一个文件。
jsp:forward：把请求转到一个新的页面。
jsp:useBean：寻找或者实例化一个JavaBean。
jsp:setProperty：设置JavaBean的属性。
jsp:getProperty：输出某个JavaBean的属性。 
jsp:plugin：根据浏览器类型为Java插件生成OBJECT或EMBED标记。

### 详细说明一下Request对象的主要方法是什么？

setAttribute(String name,Object)：设置名字为name的request的参数值
getAttribute(String name)：返回由name指定的属性值
getAttributeNames()：返回request对象所有属性的名字集合，结果是一个枚举的实例
removeAttribute(String name)：删除请求中的一个属性

### JSP四种会话跟踪技术分别是什么？

page域 数据在一个**页面**范围内有效，通过pageContext对象访问
request域 数据在一个**服务器**请求范围内有效，通过request对象访问
session域 数据在一次**会话**范围内容有效，通过session对象访问
application域 数据在一个**应用服务器**范围内有效，通过application对象访问

### JSP和Servlet有哪些相同点和不同点？另外他们之间的联系又是什么呢？

JSP全称Java Server Pages，是一种动态网页开发技术。它使用JSP标签在HTML网页中插入Java代码。标签通常以<%开头以%>结束。

Servlet(Servlet Applet):  是用JAVA编写的服务器端程序。主要用于交互式地浏览和修改数据，生成Web内容。

Servlet和JSP最主要的不同点在于，Servlet的应用逻辑是在Java文件中，并且完全从表示层中的HTML里分离开来。而JSP的情况是Java和HTML可以组合成一个扩展名为.jsp的文件。**JSP侧重于视图，Servlet主要用于控制逻辑。**

### JSP的内置对象以及该对象的使用方法。

request表示HttpServletRequest对象。它包含了有关浏览器请求的信息，并且提供了几个用于获取cookie, header, 和session数据的有用的方法。
response表示HttpServletResponse对象，并提供了几个用于设置送回浏览器的响应的方法（如cookies,头信息等）

### web.xml文件中可以配置哪些内容？

web.xml用于配置Web应用的相关信息，如：监听器（listener）、过滤器（filter）、Servlet、相关参数、会话超时时间、安全验证方式、错误页面等。

### 对Javaweb开发中的监听器的理解？

Java Web开发中的监听器（listener）就是application、session、request三个对象创建、销毁或者往其中添加修改删除属性时自动执行代码的功能组件。

### 过滤器有哪些作用？以及过滤器的用法又是什么呢?

过滤器是一个驻留在服务器端的Web组件，它可以截取客户端和服务器之间的请求与响应信息，并对这些信息进行过滤。

常见的过滤器用途主要包括：对用户请求进行统一认证、对用户的访问请求进行记录和审核、对用户发送的数据进行过滤或替换、转换图象格式。

## Web编程原理

### get和post请求，并且说说它们之间的区别？

①get请求用来从服务器上获得资源，而post是用来向服务器提交数据；
②get将表单中数据按照name=value的形式，添加到action所指向的URL 后面，并且两者使用"?"连接，而各个变量之间使用"&"连接；post是将表单中的数据放在**HTTP协议的请求头或消息体**中，传递到action所指向URL；
③get传输的数据要受到URL长度限制（1024字节）；而post可以传输大量的数据，上传文件通常要使用post方式；
④使用get时参数会显示在地址栏上，如果这些数据不是敏感数据，那么可以使用get；对于敏感数据还是应用使用post；

### 转发和重定向之间的区别？

```java
// servlet
request.getRequestDispatcher("new.jsp").forward(request, response); //转发到new.jsp
response.sendRedirect("new.jsp"); //重定向到new.jsp

// jsp
<jsp:forward page="apage.jsp" />
<%response.sendRedirect("new.jsp");
```

转发是服务器行为，重定向是客户端行为。

重定向，其实是两次request。

转发：以前的request中存放的变量不会失效，就像把两个页面拼到了一起。

重定向：以前的request中存放的变量全部失效，并进入一个新的request作用域。

### forward 和redirect的区别？

https://blog.csdn.net/weixin_37766296/article/details/80375106

1. 本质

    **forword转发是服务器上的行为，而redirect重定向是客户端的行为**
    
2. 地址栏

    forward：转发，从服务器转发。因此在客户端的浏览器地址里看不出url的变化
    redirect：重定向，在客户端重新定向了一次，因此在客户端能看出url的变化。

3. 数据共享
   由于在整个定向的过程中用的是同一个request，因此forward会将request的信息带到被重定向的jsp或者servlet中使用，即可以共享数据；redirect不能共享  
   
4. 运用

    forword：登录

    redirect：注销或跳转其他网站

### cookie 和 session 的区别？

Cookie 用于存储 Web 页面的用户信息，如账号、密码。

Session 用于存储关于用户会话（session）的信息。

1、cookie数据存放在客户的浏览器上，session数据放在服务器上。

2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗

考虑到安全应当使用session。

3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用COOKIE。

4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

# Java EE

## Spring(一)

### 简单介绍一下spring？

Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器框架。

Spring的模块大概分为6个。分别是：

1、Core Container（Spring的核心）【重要】

2、AOP（面向切面编程）【重要】

3、Messaging（消息发送的支持）

4、Data Access/Integration（数据访问和集成）

5、Web（主要是SpringWeb内容，包括MVC）【重要】

6、Test（Spring测试支持，包含JUint等测试单元的支持）



Java Bean是可复用的实体类。

### Spring中自动装配的方式有哪些？

...

### Spring中Bean的作用域有哪些？

singleton和prototype

### 什么是IoC和DI？并且简要说明一下DI是如何实现的？

IoC(Inversion of Control) 控制反转，DI(Dependency Injection)依赖注入

### Spring中BeanFactory和ApplicationContext的区别是什么？

BeanFactory是spring中比较原始，比较古老的Factory，所以BeanFactory无法支持spring插件，例如：AOP、Web应用等功能。

ApplicationContext是BeanFactory的子类，以一种更面向框架的工作方式以及对上下文进行分层和实现继承，并在这个基础上对功能进行扩展。

### springIOC原理是什么？如果你要实现IOC需要怎么做？请简单描述一下实现步骤？

...

### 依赖注入的方式有哪几种？以及这些方法如何使用？

1、Set注入 2、构造器注入 3、接口注入

### @Controller和@RestController的区别是什么？

@RestController注解相当于@ResponseBody ＋ @Controller合在一起的作用

### autowired 和resource区别是什么？

1、共同点

两者都可以写在字段和setter方法上。两者如果都写在字段上，那么就不需要再写setter方法。

2、不同点

（1）@Autowired

@Autowired为Spring提供的注解，需要导入包org.springframework.beans.factory.annotation.Autowired;只按照byType注入。

@Autowired注解是按照类型（byType）装配依赖对象

（2）@Resource

@Resource默认按照ByName自动注入，由J2EE提供，需要导入包javax.annotation.Resource。

## Spring(二)

### IOC和AOP是什么？

依赖注入的三种方式：（1）接口注入（2）Construct注入（3）Setter注入

控制反转（IoC）与依赖注入（DI）是同一个概念，引入IOC的目的：（1）脱开、降低类之间的耦合；（2）倡导面向接口编程、实施依赖倒换原则； （3）提高系统可插入、可测试、可修改等特性。

AOP（Aspect Oriented Programming），即面向切面编程，可以说是OOP（Object Oriented Programming，面向对象编程）的补充和完善。

### 如何理解AOP中的连接点（Joinpoint）、切点（Pointcut）、增强（Advice）、引介（Introduction）、织入（Weaving）、切面（Aspect）这些概念？

...

### AOP的原理是什么？

Spring AOP中的动态代理主要有两种方式，JDK动态代理和CGLIB动态代理。

### Spring框架为企业级开发带来的好处有哪些？

...

### Spring框架的优点都有哪些？

Spring是一个轻量级的DI和AOP容器框架，它的优点主要有以下几点：

Spring是一个非侵入式框架，其目标是使应用程序代码对框架的依赖最小化，应用代码可以在没有Spring或者其他容器的情况运行。

Spring提供了一个一致的编程模型，使应用直接使用POJO开发，从而可以使运行环境隔离开来。

Spring推动应用的设计风格向面向对象及面向接口编程转变，提高了代码的重用性和可测试性。

### Struts拦截器和Spring AOP有什么区别？

...

### 持久层设计要考虑的问题有哪些？请谈一下你用过的持久层框架都有哪些？

所谓"持久"就是将数据保存到可掉电式存储设备中以便今后使用，简单的说，就是将内存中的数据保存到关系型数据库、文件系统、消息队列等提供持久化支持的设备中。持久层就是系统中专注于实现数据持久化的相对独立的层面。

持久层框架有：
\- Hibernate
\- MyBatis

# 计算机网络

## 网络概述

### TCP协议、IP协议、HTTP协议分别在哪一层？

运输层，网络层，应用层。

---

网络七层模型：

  物理层，数据链路层，网络层，运输层，会话层，表示层，应用层

网络五层模型：

  物理层，数据链路层，网络层，运输层，应用层

![img](https://gitee.com/oeong/picgo/raw/master/images/20210316164355.jpeg)

## 网络层

### ARP协议和ARP攻击

ARP协议(地址解析协议): 将IP地址转换为MAC地址

ARP应答中的IP地址和MAC地址中的信息是可以伪造的，并不一定是自己的真实IP地址和MAC地址，由此，ARP欺骗就产生了。

### 什么是ICMP协议，它的作用是什么？

ICMP(Internet控制报文)协议。用于在IP主机、路由器之间传递控制消息。

### 交换机和的区别？

1、工作层次不同，一个是数据链路层，一个是网络层

2、寻址依据不同，一个基于MAC寻址，一个是基于IP寻址

3、交换机分割冲突域，不划分广播域。路由器既可分割冲突域也可分割广播域

4、转发的数据对象不同，交换机转发的是数据帧，路由器转发的是分组报文

## 运输层

### 3次握手

![image-20210422223427394](https://gitee.com/oeong/picgo/raw/master/images/20210422223429.png)

A发送SYN数据包请求连接；
B收到后回复ACK；
A收到后回复ACK

### 4次挥手

![image-20210422223346629](https://gitee.com/oeong/picgo/raw/master/images/20210422223348.png)

A发送FIN数据包请求断开连接；
B收到后回复ACK；
B发送FIN数据包要求反向断开连接；
A收到后回复ACK



【三次握手】
男：我们在一起吧
女：好的啊
男：好的，从现在开始吧
【四次挥手】
男：我们分手吧
女：我想一下
女：我们分手吧
男：好的，现在就结束吧

### TCP为什么要建立连接？

保证可靠传输。

### TCP为什么可靠一些

三次握手，超时重传，滑动窗口，拥塞控制。

### 哪种应用场景会使用TCP协议，使用它的意义

当对网络通讯质量有要求的时候，需要整个数据要准确无误的传递给对方。如HTTP、HTTPS、FTP等传输文件的协议，POP、SMTP等邮件传输的协议。

## 应用层

### HTTP请求中的304状态码的含义

304(未修改)自从上次请求后，请求的网页未修改过。

### SSL四次握手的过程

...

### HTTP1.1和1.0的区别

...

### HTTP请求，并说明应答码502和504的区别

OPTIONS：返回服务器针对特定资源所支持的HTTP请求方法。也可以利用向Web服务器发送'*'的请求来测试服务器的功能性。

HEAD：向服务器索要与GET请求相一致的响应，只不过响应体将不会被返回。这一方法可以在不必传输整个响应内容的情况下，就可以获取包含在响应消息头中的元信息。

GET：向特定的资源发出请求。

POST：向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的创建和/或已有资源的修改。

PUT：向指定资源位置上传其最新内容。

DELETE：请求服务器删除Request-URI所标识的资源。

TRACE：回显服务器收到的请求，主要用于测试或诊断。

CONNECT：HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。

虽然HTTP的请求方式有8种，但是我们在实际应用中常用的也就是get和post，其他请求方式也都可以通过这两种方式间接的来实现。

502：作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到**无效的响应**。

504：作为网关或者代理工作的服务器尝试执行请求时，**未能及时**从上游服务器（URI标识出的服务器，例如HTTP、FTP、LDAP）或者辅助服务器（例如DNS）收到响应。

### HTTP和HTTPS的区别

1. HTTPS需要申请CA证书
2. HTTP是明文传输，HTTPS是加密的安全传输
3. 端口不同，HTTP是80，HTTPS是443

### 浏览器从接收到一个URL，到最后展示出页面，经历了哪些过程。

1.DNS解析 2.TCP连接 3.发送HTTP请求 4.服务器处理请求并返回HTTP报文 5.浏览器解析渲染页面

### DNS的寻址过程

1、在浏览器中输入`www.oeong.com`域名，操作系统会先检查自己**本地的hosts文件**是否有这个网址映射关系，如果有，就先调用这个IP地址映射，完成域名解析。

2、如果hosts里没有这个域名的映射，则查找**本地DNS解析器**缓存，是否有这个网址映射关系，如果有，直接返回，完成域名解析。

3、如果hosts与本地DNS解析器缓存都没有相应的网址映射关系，首先会找TCP/IP参数中设置的首选DNS服务器，在此我们叫它**本地DNS服务器**，此服务器收到查询时，如果要查询的域名，包含在本地配置区域资源中，则返回解析结果给客户机，完成域名解析，此解析具有权威性。

4、如果本地DNS服务器也失效：

如果未采用转发模式（**迭代**），本地DNS就把请求发至**13台根DNS**，根DNS服务器收到请求后，会判断这个域名（如.com）是谁来授权管理，并返回一个负责该顶级域名服务器的IP，本地DNS服务器收到顶级域名服务器IP信息后，继续向该顶级域名服务器IP发送请求，该服务器如果无法解析，则会找到负责这个域名的下一级DNS服务器（如`www.oeong.com`)的IP给本地DNS服务器，循环往复直至查询到映射，将解析结果返回本地DNS服务器，再由本地DNS服务器返回解析结果，查询完成。

如果采用转发模式（**递归**），则此DNS服务器就会把请求转发至**上一级DNS服务器**，如果上一级DNS服务器不能解析，则继续向上请求。最终将解析结果依次返回本地DNS服务器，本地DNS服务器再返回给客户机，查询完成。

从客户端到本地DNS服务器是属于递归查询，而DNS服务器之间就是的交互查询就是迭代查询。

### 负载均衡 反向代理模式的优点、缺点

...

# 操作系统

## 操作系统概述

### 64位和32位的区别？

32位操作系统针对32位的CPU设计，64位操作系统针对64位的CPU设计。

1、运行能力不同。64位可以一次性可以处理8个字节的数据量，而32位一次性只可以处理4个字节的数据量，因此64位比32位的运行能力提高了一倍。
2、内存寻址不同。**64位最大寻址空间为2的64次方**，理论值直接达到了16TB，而32位的最大寻址空间为2的32次方，为4GB，换而言之，就是说32位系统的处理器最大只支持到4G内存，而64位系统最大支持的内存高达亿位数。 
3、运行软件不同。由于32位和64位CPU的指令集是不同的。所以需要区分32位和64位版本的软件。
为了保证兼容性，64位CPU上也能运行老的32位指令。于是实际上我们可以在64位CPU上运行32位程序，但是反过来不行。简而言之就是64位的操作系统可以兼容运行32位的软件，反过来32位系统不可以运行64位的软件。

### CentOS 和 Linux的关系？

CentOS是Linux众多得发行版本之一

## 进程的描述与控制

### 解释LINUX下的线程，GDI类

LINUX实现的就是基于核心轻量级进程的”一对一”线程模型，一个线程实体对应一个核心轻量级进程，而线程之间的管理在核外函数库中实现。

GDI类为图像设备编程接口类库。

### 进程和线程的区别是什么？

进程是运行中的程序，线程是进程内部的一个执行序列
进程是**资源**分配的基本单元，线程是**独立调度**的基本单位
进程间切换代价大，线程间切换代价小
进程拥有资源多，线程拥有资源少
多个线程共享进程的资源

开个QQ，开了一个进程。在QQ的这个进程里，传输文字开一个线程、传输语音开了一个线程、弹出对话框又开了一个线程。

### 系统线程数量上限是多少？

Linux 系统中单个进程的最大线程数有其最大的限制 PTHREAD_THREADS_MAX。

### 如何杀死一个进程？

- kill pid；系统发送一个signal,程序收到信号后，会先释放资源，再关闭程序。

- kill -9 pid；-9表示强制执行。

## 输入输出系统

### 介绍socket编程的三种通信模型，BIO，NIO，AIO 

- BIO：block IO同步阻塞式IO，就是我们平时使用的传统IO，特点是模式简单使用方便，并发处理能力低。

- NIO：new IO 同步非阻塞IO，是传统IO的升级，客户端和服务器通过channel（通道）通信，实现多路复用。

- AIO，异步非阻塞IO，异步IO的操作是基于事件和回调机制的。

# UML

**统一建模语言**(Unified Modeling Language，UML)是一种为面向对象系统的产品进行说明、可视化和编制文档的一种标准语言。

### UML中有哪些常用的图？

用例图（用来捕获需求，描述系统的功能，通过该图可以迅速的了解系统的功能模块及其关系）

类图（描述类以及类与类之间的关系，通过该图可以快速了解系统）

时序图（描述执行特定任务时对象之间的交互关系以及执行顺序，通过该图可以了解对象能接收的消息也就是说对象能够向外界提供的服务）。