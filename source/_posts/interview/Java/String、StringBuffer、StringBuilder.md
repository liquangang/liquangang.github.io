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
#### 下面这段代码的输出结果？
```
    String a = "hello2"; 　　
    String b = "hello" + 2; 　　
    System.out.println((a == b));
```
* true, 编译期间"hello" + 2被优化为hello2，所以两个对象都指向了同一个常量地址

#### 下面这段代码输出结果？
```
    String a = "hello2"; 　  
    String b = "hello";       
    String c = b + 2;       
    System.out.println((a == c));
```
* false，因为有对象引用，所以c指向的地址是在堆中，而a和b都是指向了常量地址

#### 下面这段代码的输出结果？
```
String a = "hello2";   　
final String b = "hello";       
String c = b + 2;      
System.out.println((a == c));
```
* true，final变量会在编译期间替换成具体的值，即c="hello"+2，所以a和c指向了同一个常量地址

#### 下面这段代码的输出结果？
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
* false，b是通过调用方法赋值，调用方法需要在运行时执行，所以c保存的地址是在运行时确定，而a保存的地址在编译时已经确认

#### 下面这段代码的输出结果？
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
* false、false、false、true，intern作用是运行时在常量池中查找，有返回一个该常量的引用，没有创建一个常量，然后返回一个该常量的引用

#### String str = new String("abc")创建了哪些对象？
* 类加载时创建了"abc"对象，代码执行时创建了str对象

#### 下面这段代码1）和2）的区别是什么？
```
public class Main {
    public static void main(String[] args) {
        String str1 = "I";
        //str1 += "love"+"java";        1)
        //str1 = str1+"love"+"java";    2)      
    }
}
```
* 1中只有一次append操作，2中有两次
* 1中的字符串会在编译期间被合并
* 1的效率比2高

#### String是不是基本数据类型?
* 不是基本数据类型，继承Object


#### String str="i"与 String str=new String(“i”)一样吗？
* 不一样，str="i"会分配到常量池里面，new String(“i”)会创建一个新对象

#### 如何将字符串反转？
* 方案1：将字符串按字符放到栈中，然后从栈中输出
* 方案2：StringBuffer 或 StringBuilder 的 reverse 成员方法
* 方案3：利用toCharArray方法转化成数组，然后倒序输出
* 方案4：利用 String 的 CharAt 方法倒序输出
* 方案5：利用递归加二分实现
```
public String testStringReverse(String string) {
        if (string.length() <= 1) {
            System.out.println("----" + string + "-----");
            return string;
        }

        String leftString = string.substring(0, string.length()/2);
        String rightString = string.substring(string.length()/2, string.length());
        String reverseString = testStringReverse(rightString) + testStringReverse(leftString);
        System.out.println("====" + reverseString + "=====");
        return reverseString;
    }
```

#### String 类的常用方法都有那些？
* 长度相关：
  * public int length()
* 数组相关：
  * public byte[] getBytes()
  * public char[] toCharArray()
  * 按照regex分割为字符串数组：public String[] split(String regex)
* 判断相关：
  * public boolean isEmpty()
  * public boolean equals(Object anObject)
* 查找相关：
  * public char charAt(int index)
* 变更相关：
  * public String replace(char oldChar, char newChar)
