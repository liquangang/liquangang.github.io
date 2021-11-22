---
title: String、StringBuffer、StringBuilder
date: 2021-11-22 22:50:43
tags: 面试
categories:
- [interview, interview-java]
---

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
