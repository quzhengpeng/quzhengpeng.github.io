---
layout: post
title: hiveserver2安装指南
date: 2019-11-12
categories: hive
tags: hive hiveserver2
---

## 配置 hive-site.xml

```xml
    <property>
        <name>hive.server2.thrift.port</name>
        <value>10000</value>
    </property>
    <property>
        <name>hive.server2.thrift.bind.host</name>
        <value>localhost</value>
    </property>
    <property>
        <name>hive.server2.long.polling.timeout</name>
        <value>5000ms</value>
    </property>
```

## 配置 core-site.xml

```xml
    <property>
        <!-- xxx 是连接 beeline 的用户，将 xxx 替换成自己的用户名即可 -->
        <!-- * 表示可通过超级代理 xxx 操作 hadoop 的用户、用户组和主机 -->
        <name>hadoop.proxyuser.xxx.hosts</name>
        <value>*</value>
    </property>
    <property>
        <name>hadoop.proxyuser.xxx.groups</name>
        <value>*</value>
    </property>
```

## 启动 hiveserver2 服务

`hive --service hiveserver2`

查看端口是否被使用 `sudo netstat -anp | grep 10000`

## 通过 beeline 连接hive

```bash
beeline
!connect jdbc:hive2://localhost:10000

beeline -u jdbc:hive2://localhost:10000 -n username -p passwd
```
