---
title: Linux常用命令总结
date: 2021-09-09 10:26:09
tags: 编程
categories:
- [Linux]
---

### cat
* 显示文件最后10行：cat filename | tail -n 10
* 显示文件前10行：cat filename | head -n 10
* 从10行开始显示，显示10行以后的所有行：cat filename | tail -n +10
* 显示10行到50行：cat filename | head -n 50 | tail -n +10  
* 在filename1 和 filename2中查找xxx关键字：cat filename1 filename2 | grep xxx
* 模糊匹配aaaa开头的文件并在这些文件中查找xxx关键字：cat aaaa*.log | grep xxx
* 模糊匹配aaaa开头的文件并在这些文件中查找xxx关键字统计出现次数：cat aaaa*.log | grep xxx -c 













  


    

    



