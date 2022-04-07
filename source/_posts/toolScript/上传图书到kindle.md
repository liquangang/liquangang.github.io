---
title: 上传图书到kindle
date: 2022-02-17 16:28:59
tags: 脚本工具
categories:
- [工具脚本]
---

### 配置以及获取相关信息
* 登录[该页面](https://www.amazon.cn/gp/digital/fiona/manage?ref_=hp_ss_qs_v3_dv_dc#/home/settings/payment)，然后在“个人文档设置”部分，增加自己使用发送电子书的邮箱到“”已认可的发件人电子邮箱列表”，该部分邮箱即为下文脚本中的发送邮箱
* 获取要发送到的邮箱，该邮箱跟上面的添加邮箱在同一个页面上，在“〖发送至Kindle〗电子邮箱”部分，该部分邮箱即为下文脚本中的接收邮箱
* 到发送邮箱里面开启SMTP服务器，此处我使用的是163，该部分请自行百度



### 示例脚本
```
# -*- coding: utf-8 -*-
import os
import smtplib  # 导入PyEmail
# 发送字符串的邮件
from email import encoders
from email.mime.application import MIMEApplication
from email.mime.base import MIMEBase
from email.mime.text import MIMEText
# 需要 MIMEMultipart 类
from email.mime.multipart import MIMEMultipart

SENDER = "fasongyouxiang@163.com" # 发送邮箱
RECEIVE = "jiehsouyouxiang1@kindle.cn;jiehsouyouxiang2@kindle.cn" # 接收邮箱，多个用分号隔开
PASSWORD = "youxiangmima" #邮箱密码
SERVER = "smtp.163.com" # smtp服务地址
SERVER_PORT = 994 # smtp服务器端口

# 邮件构建

def send(file_path):

    print("开始发送：", file_path)
    message = MIMEMultipart()
    message['From'] = SENDER  # 发送方
    message['To'] = RECEIVE  # 接收方

    # 构建邮件附件
    part = MIMEApplication(open(file_path, 'rb').read())
    part.add_header('Content-Disposition', 'attachment', filename=get_last_filename(file_path))
    message.attach(part)

    smtp = smtplib.SMTP_SSL(SERVER, SERVER_PORT)  # 实例化smtp服务器
    smtp.login(SENDER, PASSWORD)  # 发件人登录
    smtp.sendmail(SENDER, [RECEIVE], message.as_string())  # as_string 对 message 的消息进行了封装
    smtp.close()
    print("发送邮件成功：", file_path)

def get_last_filename(filename):
    return filename[filename.rindex('/') + 1: len(filename)]

def send_to_kindle():
    dir = os.walk(r"./ebook")
    for path, dir_list, file_list in dir:
        for file_name in file_list:
            if "DS_Store" not in file_name:
                send("./ebook/" + file_name)


if __name__=='__main__':
    send_to_kindle()
```
