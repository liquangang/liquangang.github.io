---
title: java-面试题
date: 2021-11-17 11:33:55
tags: 面试
categories:
- [面试]
---

## 面向对象、面向过程
### 面向对象：将数据和操作方法放到一起，作为一个相互依存的整体-对象，对象是人对具体事务抽象出来的概念
#### 对象：有自己独特个性的任何事物 
* 特点：
    * 继承：子类继承父类属性和方法
    * 封装：将不需要外接知道的内容隐藏起来，优点是实现了"高内聚、低耦合"；隐藏实现细节；对成员变量实现更精确控制  
    * 多态：一种行为具有多种表现形式，存在条件：继承、重写、父类引用指向子类对象
* 模板：类
* 组成：属性、方法

#### 优缺点：
* 优：
    * 适合大型系统
    * 易复用
    * 易拓展
    * 易维护
    * 低耦合
        
* 缺：
    * 较抽象
    * 性能差


### 面向过程：与面向对象相反，要按照执行过程自己实现所有功能细节
#### 优缺点：
* 优：
    * 适合小型系统
    * 易理解
    * 性能好
* 缺：
    * 不适合大型系统
    * 难复用
    * 难拓展
    * 难维护
    

## JDK、JRE、JVM
* JDK（Java Development Kit：开发Java程序）：
  * JRE（Java Runtime Environment：运行Java程序）：
    * JVM（Java Virtual Machine：实现Java程序跨平台运行）
    * 运行时需要的核心类库
  * 开发人员工具
    * 编译工具（javac.exe）
    * 运行工具（java.exe）
    
## ==、equals区别
* ==：判断的是两个变量对应的内存中的值是否相等，基本数据类型比较值，引用类型比较内存地址
* equals：不重写时与"=="功能一致，其在Object方法列表中，可重写该方法

## HashCode、equals区别
### 参考资料
* [参考文章1](https://www.jianshu.com/p/5a7f5f786b75)

### equals
* 特点：
    * 重写需要遵循java对该方法重写的规范（对称性、反射性、类推性、一致性、非空性）
    * 未重写时与"=="功能一致
    * 当某个类要在散列表中使用时，重写该方法的同时必须重写hashCode方法，否则该方法无效
    
### HashCode
* 作用：获取哈希码（散列码，为了提升散列表查找性能），该哈希码作用是确定该对象在哈希表中索引位置
* 特点：
    * 该方法在Object的方法，所以所有类都继承该方法
    * 该方法只在该对象被散列表（例如HashMap、HaskTable、HashSet）所使用时，才会使用到该方法，其他情况下没用
    * 该方法可以通过重写进行自定义
    
## final：用于修饰类、方法、数据，使其内存的内容不变
* 类：该类不能被继承
* 方法：该方法不能被重写。与private有相同功能
* 数据：
    * 基本数据类型、String：其值不能修改，String在修改时会重新创建一个对象，即其内存中的地址会指向新的对象，所以String被final修饰时，其值不能修改
    * 引用数据类型：该引用地址不能变，但地址指向的对象内部的变量可以变

## String、StringBuffer、StringBuilder
### 相关结论
* 字符串直接相加（"a" + "b"）性能高，间接相加（str1 + str2）性能低
* 多数场景下执行效率：StringBuilder > StringBuffer > String
* 使用场景：
    * string：简单字符串直接相加且改动少
    * stringBuilder：字符串操作比较多
    * stringBuffer：多线程且操作比较多

### String：常量字符串类
* 使用场景：简单常量字符串
* 特点：
    * 有新操作就会生成一个新对象
    * 性能较差
    * 被final修饰，不能被继承
    * 下面的情况，两个string对象指向同一个地址，JVM会优先查找常量池中有没有，有的话直接将已存在的地址赋值给新对象
    ```
    String string1 = "111";
    String string2 = "111";
    // true
    System.out.println(string1==string2);
    ```
    * 下面的情况，两个string对象是新开辟的内存空间，所以不相等
    ```
    String string1 = new String("111");
    String string2 = new String("222");
    // false
    System.out.println(string1==string2);
    ```
    
### StringBuffer：线程安全的可变字符串类
* 使用场景：需要频繁变化且需要线程安全
* 特点：
    * 每次变更都是在原来对象上去修改，不产生新对象
    * 大部分场景下性能比String好
    * 与StringBuffer基本相同，多了一个synchronized修饰，所以线程安全
    
### StringBuilder：线程不安全的可变字符串类
* 使用场景：不需要考虑线程安全问题场景，建议首选该类，然后是StringBuffer，然后是String
* 特点：
    * 与StringBuffer类似，不产生新对象
    * 大部分场景性能比StringBuffer更好
    
### string常见面试题
1、下面这段代码的输出结果？
```
    String a = "hello2"; 　　
    String b = "hello" + 2; 　　
    System.out.println((a == b));
```
* 答：true, 编译期间"hello" + 2被优化为hello2，所以两个对象都指向了同一个常量地址

2、下面这段代码输出结果？
```
    String a = "hello2"; 　  
    String b = "hello";       
    String c = b + 2;       
    System.out.println((a == c));
```
* 答：false，因为有对象引用，所以c指向的地址是在堆中，而a和b都是指向了常量地址

3、下面这段代码的输出结果？
```
String a = "hello2";   　 
final String b = "hello";       
String c = b + 2;      
System.out.println((a == c));
```
* 答：true，final变量会在编译期间替换成具体的值，即c="hello"+2，所以a和c指向了同一个常量地址

4、下面这段代码的输出结果？
```
public class Main {
    public static void main(String[] args) {
        String a = "hello2";
        final String b = getHello();
        String c = b + 2;
        System.out.println((a == c));
    }
     
    public static String getHello() {
        return "hello";
    }
}
```
* 答：false，b是通过调用方法赋值，调用方法需要在运行时执行，所以c保存的地址是在运行时确定，而a保存的地址在编译时已经确认

5、下面这段代码的输出结果？
```
public class Main {
    public static void main(String[] args) {
        String a = "hello";
        String b =  new String("hello");
        String c =  new String("hello");
        String d = b.intern();
         
        System.out.println(a==b);
        System.out.println(b==c);
        System.out.println(b==d);
        System.out.println(a==d);
    }
}
```
* 答：false、false、false、true，intern作用是运行时在常量池中查找，有返回一个该常量的引用，没有创建一个常量，然后返回一个该常量的引用

6、String str = new String("abc")创建了哪些对象？
* 答：类加载时创建了"abc"对象，代码执行时创建了str对象

7、下面这段代码1）和2）的区别是什么？
```
public class Main {
    public static void main(String[] args) {
        String str1 = "I";
        //str1 += "love"+"java";        1)
        //str1 = str1+"love"+"java";    2)      
    }
}
```
* 答：
    * 1中只有一次append操作，2中有两次
    * 1中的字符串会在编译期间被合并
    * 1的效率比2高
