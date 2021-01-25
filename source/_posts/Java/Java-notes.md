---
title: Java_notes
date: 2021-01-23 11:06:35
tags: [Java]
---

<!-- more -->

# Java快速入门

## Java简介

- JDK：Java Development Kit
- JRE：Java Runtime Environment

简单地说，JRE就是运行Java字节码的**虚拟机**。但是，如果只有Java源码，要编译成Java字节码，就需要JDK，因为JDK除了**包含**JRE，还提供了编译器、调试器等开发工具。

  二者关系如下：

```ascii
    ┌─    ┌──────────────────────────────────┐
    │     │     Compiler, debugger, etc.     │
    │     └──────────────────────────────────┘
   JDK ┌─ ┌──────────────────────────────────┐
    │  │  │                                  │
    │ JRE │      JVM + Runtime Library       │
    │  │  │                                  │
    └─ └─ └──────────────────────────────────┘
          ┌───────┐┌───────┐┌───────┐┌───────┐
          │Windows││ Linux ││ macOS ││others │
          └───────┘└───────┘└───────┘└───────┘
```

## Java程序基础

`int[] ns = new int[5];`

## 流程控制

#### if判断

`==`表示“引用的**对象**是否相等”，浮点数判断相等不能直接用

使用`equals()`判断引用类型**内容**相等，注意避免`NullPointerException`。

#### for each循环

`for each`循环可以直接遍历数组的每个元素；

```
int[] ns = { 1, 4, 9, 16, 25 };
for (int n : ns) {
	System.out.println(n);
}
```

## 数组操作

#### 遍历数组

遍历数组可以使用`for`循环，`for`循环可以访问数组索引，`for each`循环直接迭代每个数组元素，但无法获取索引；

使用`Arrays.toString()`可以快速获取数组内容。

#### 排序

排序前

```ascii
                   ┌──────────────────────────────────┐
               ┌───┼──────────────────────┐           │
               │   │                      ▼           ▼
         ┌───┬─┴─┬─┴─┬───┬────────┬───┬───────┬───┬──────┬───┐
ns ─────>│░░░│░░░│░░░│   │"banana"│   │"apple"│   │"pear"│   │
         └─┬─┴───┴───┴───┴────────┴───┴───────┴───┴──────┴───┘
           │                 ▲
           └─────────────────┘
```

排序后，原来的3个字符串在**内存**中均没有任何变化，但是`ns`数组的每个元素**指向**变化了。

```ascii
                   ┌──────────────────────────────────┐
               ┌───┼──────────┐                       │
               │   │          ▼                       ▼
         ┌───┬─┴─┬─┴─┬───┬────────┬───┬───────┬───┬──────┬───┐
ns ─────>│░░░│░░░│░░░│   │"banana"│   │"apple"│   │"pear"│   │
         └─┬─┴───┴───┴───┴────────┴───┴───────┴───┴──────┴───┘
           │                              ▲
           └──────────────────────────────┘
```

# 面向对象编程

Java是一种面向对象的编程语言。面向对象编程，英文是Object-Oriented Programming，简称OOP。

## 面向对象基础

在OOP中，`class`和`instance`是“模版”和“实例”的关系；

### 方法 

在方法内部，可以使用一个隐含的变量`this`，它始终指向当前实例。因此，通过`this.field`就可以访问当前实例的字段。

### 方法重载

方法重载是指多个方法的方法名相同，但各自的参数不同；

重载方法返回值类型应该相同。

### 继承

#### 区分继承和组合

`Student`和`Book`的关系是has关系。

- 继承是面向对象编程的一种强大的代码复用方式；
- Java只允许单继承，所有类最终的根类是`Object`；
- `protected`允许子类访问父类的字段和方法；
- 子类的构造方法可以通过`super()`调用父类的构造方法；
- 可以**安全地向上转型**为更抽象的类型；
- 可以强制向下转型，最好借助`instanceof`判断；
- 子类和父类的关系是is，has关系不能用继承。

### 多态

在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为覆写（Override）。

- 子类可以覆写父类的方法（Override），覆写在子类中改变了父类方法的行为；
- Java的方法调用总是作用于运行期对象的实际类型，这种行为称为多态；
- `final`修饰符有多种作用：
  - `final`修饰的方法可以阻止被覆写；
  - `final`修饰的class可以阻止被继承；
  - `final`修饰的field必须在创建对象时初始化，随后不可修改。

### 抽象类

通过`abstract`定义的方法是抽象方法，它只有定义，没有实现。抽象方法定义了子类必须实现的接口规范；

### 接口

所谓`interface`，就是比抽象类还要抽象的纯抽象接口，因为**不能定义实例字段**。

`interface`的字段只能是`public static final`类型

### 静态字段和静态方法

所有实例共享一个静态字段。

不推荐用`实例变量.静态字段`去访问静态字段，推荐**用类名来访问静态字段**。

### 包

Java内建的`package`机制是为了避免`class`命名冲突；

JDK的核心类使用`java.lang`包，编译器会自动导入；

JDK的其它常用类定义在`java.util.*`，`java.math.*`，`java.text.*`，……；

包名推荐使用**倒置的域名**，避免冲突，例如`org.apache`。

包没有父子关系，`com.apache`和`com.apache.abc`是不同的包。

### 作用域

定义在一个`class`内部的`class`称为嵌套类（`nested class`）

如果不确定是否需要`public`，就不声明为`public`，即尽可能少地暴露对外的字段和方法。

把方法定义为`package`权限有助于测试，因为测试类和被测试类只要位于同一个`package`，测试代码就可以访问被测试类的`package`权限方法。

一个`.java`文件只能包含一个`public`类，但可以包含多个非`public`类。如果有`public`类，文件名必须和`public`类的名字相同。

`protected`作用于继承关系。定义为`protected`的字段和方法可以被子类访问，以及子类的子类

### classpath和jar

`classpath`是JVM用到的一个环境变量，它用来指示JVM如何搜索`class`。

因为Java是编译型语言，源码文件是`.java`，而编译后的`.class`文件才是真正可以被JVM执行的字节码。

jar包实际上就是一个zip格式的压缩文件，而jar包相当于目录。

>  如何创建jar包？

因为jar包就是zip包，所以，直接在资源管理器中，找到正确的目录，点击右键，在弹出的快捷菜单中选择“发送到”，“压缩(zipped)文件夹”，就制作了一个zip文件。然后，把后缀从`.zip`改为`.jar`，一个jar包就创建成功。

#### 小结

JVM通过环境变量`classpath`决定搜索`class`的路径和顺序；

不推荐设置系统环境变量`classpath`，始终建议通过`-cp`命令传入；

jar包相当于目录，可以包含很多`.class`文件，方便下载和使用；

`MANIFEST.MF`文件可以提供jar包的信息，如`Main-Class`，这样可以直接运行jar包。

## Java核心类

### 字符串和编码

- Java字符串`String`是不可变对象；
- 字符串操作不改变原字符串内容，而是返回新字符串；
- 常用的字符串操作：提取子串、查找、替换、大小写转换等；
- Java使用Unicode编码表示`String`和`char`；
- 转换编码就是将`String`和`byte[]`转换，需要指定编码；
- 转换为`byte[]`时，始终优先考虑`UTF-8`编码。

### StringBuilder

为了能高效拼接字符串，Java标准库提供了`StringBuilder`，它是一个可变对象，可以预分配**缓冲区**，这样，往`StringBuilder`中新增字符时，**不会创建新的临时对象**；

`StringBuilder`可以支持**链式操作**，实现链式操作的关键是返回实例本身；

### StringJoiner

用指定分隔符拼接字符串数组时，使用`StringJoiner`或者`String.join()`更方便；

用`StringJoiner`拼接字符串时，还可以额外附加一个“开头”和“结尾”。

### 包装类型

Java核心库提供的包装类型可以把基本类型包装为`class`；

自动装箱和自动拆箱都是在编译期完成的（JDK>=1.5）；

装箱和拆箱会影响执行效率，且拆箱时可能发生`NullPointerException`；

包装类型的比较必须使用`equals()`；

整数和浮点数的包装类型都继承自`Number`；

包装类型提供了大量实用方法。

### JavaBean

JavaBean是一种符合命名规范的`class`，它通过`getter`和`setter`来定义属性；

JavaBean主要用来传递数据，即把一组数据组合成一个JavaBean便于传输；

可以利用IDE快速生成`getter`和`setter`；

属性是一种通用的叫法，并非Java语法规定；

使用`Introspector.getBeanInfo()`可以获取属性列表。

### 枚举类

Java使用`enum`定义枚举类型，它被编译器编译为`final class Xxx extends Enum { … }`；

通过`name()`获取常量定义的字符串，注意不要使用`toString()`；

通过`ordinal()`返回常量定义的顺序（无实质意义）；

可以为`enum`编写构造方法、字段和方法

`enum`的构造方法要声明为`private`，字段强烈建议声明为`final`；

`enum`适合用在`switch`语句中。

```java
enum Weekday {
    MON(1), TUE(2), WED(3), THU(4), FRI(5), SAT(6), SUN(0);
}
```

### 纪录类

使用`String`、`Integer`等类型的时候，这些类型都是**不变类**，一个不变类具有以下特点：

1. 定义class时使用`final`，无法派生子类；
2. 每个字段使用`final`，保证创建实例后无法修改任何字段。

`public record Point(int x, int y) {}`

从Java 14开始，提供新的`record`关键字，可以非常方便地定义Data Class：

- 使用`record`定义的是不变类；
- 可以编写Compact Constructor对参数进行验证；
- 可以定义静态方法。

### BigInteger

`BigInteger`用于表示任意大小的整数；

`BigInteger`是不变类，并且继承自`Number`；

将`BigInteger`转换成基本类型时可使用`longValueExact()`等方法保证结果准确。

### BigDecimal

如果查看`BigDecimal`的源码，可以发现，实际上一个`BigDecimal`是通过一个`BigInteger`和一个`scale`来表示的，即`BigInteger`表示一个完整的整数，而`scale`表示小数位数；

`BigDecimal`用于表示精确的小数，常用于财务计算；

比较`BigDecimal`的值是否相等，必须使用`compareTo()`而不能使用`equals()`

### 常用工具类

#### Math

数学计算

#### Random

创建`Random`实例时，如果不给定种子，就使用系统当前时间戳作为种子，因此每次运行时，种子不同，得到的**伪随机数**序列就不同。

#### SecureRandom

安全的随机数，真随机数。种子是通过CPU的热噪声、读写磁盘的字节、网络流量等各种随机事件产生的“熵”。

# 异常处理

## Java的异常

Java使用异常来表示错误，并通过`try ... catch`捕获异常；

Java的异常是`class`，并且从`Throwable`继承；

`Error`是无需捕获的严重错误，`Exception`是应该捕获的可处理的错误；

`RuntimeException`无需强制捕获，非`RuntimeException`（Checked Exception）需强制捕获，或者用`throws`声明；

如果不想写任何`try`代码，可以直接把`main()`方法定义为`throws Exception`。也就声明了可能抛出所有的`Exception`，因此在内部就无需捕获了。代价就是一旦发生异常，程序会立刻退出。

## 捕获异常

使用`try ... catch ... finally`时：

- 多个`catch`语句的匹配顺序非常重要，子类必须放在前面；
- `finally`语句保证了有无异常都会执行，它是可选的；
- 一个`catch`语句也可以匹配多个非继承关系的异常。

## 抛出异常

调用`printStackTrace()`可以打印异常的传播栈，对于调试非常有用；

捕获异常并再次抛出新的异常时，应该持有原始异常信息；

通常不要在`finally`中抛出异常。如果在`finally`中抛出异常，应该原始异常加入到原有异常中。调用方可通过`Throwable.getSuppressed()`获取所有添加的`Suppressed Exception`。

## 自定义异常

抛出异常时，尽量复用JDK已定义的异常类型；

自定义异常体系时，推荐从`RuntimeException`派生“根异常”，再派生出业务异常；

自定义异常时，应该提供多种构造方法。

## NullPointerException

空指针异常

编写业务逻辑时，用空字符串`""`表示未填写比`null`安全得多。

## 断言

断言（Assertion）是一种调试程序的方式。在Java中，使用`assert`关键字来实现断言。

## JDK Logging

日志是为了替代`System.out.println()`，可以定义格式，重定向到文件等；

日志可以存档，便于追踪问题；

日志记录可以按级别分类，便于打开或关闭某些级别；

可以根据配置文件调整日志，无需修改代码；

Java标准库提供了`java.util.logging`来实现日志功能。

## Commons Logging

和Java标准库提供的日志不同，Commons Logging是一个第三方日志库，它是由Apache创建的日志模块。

Commons Logging是使用最广泛的日志模块；

Commons Logging的API非常简单；

Commons Logging可以自动检测并使用其他日志模块。

