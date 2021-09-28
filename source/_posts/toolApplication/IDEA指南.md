---
title: IDEA指南
date: 2021-08-31 10:39:05
tags: 编程
categories:
- [工具应用]
---

### IDEA简介
* 截止到2021.08.31，是全世界最流行的Java集成开发环境

### tips
#### 快捷键
* ctrl + alt + v：快速生成方法返回值接收代码
* /** + enter：生成javaDoc注释

### IDEA常见error
#### Error: java: System Java Compiler was not found in classpath
* Project Settings > Compiler > Java Compiler 
    * changed the drop down Use compiler from Javac to Eclipse
  
#### Error:java: source level should be comprised in between '1.3' and '1.9' (or '5', '5.0', ..., '9' or '9.0'): 12
* Preferences部分设置
    * Preferences > Compiler > Java Compiler > Use compiler, 选javac
    * Project bytecode version，选8，根据project sdk来确定
    * Target bytecode version，选8，与Project bytecode version保持一致
* Project structure部分设置
    * Project structure > project > project sdk，选择1.8
    * Project language level，选SDK default
    * Modules > source > language level, 选Project default

