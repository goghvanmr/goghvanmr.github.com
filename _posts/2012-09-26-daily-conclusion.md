---
layout: post
title: "Daily conclusion"
description: ""
category: Daily conclusion
tags: [Programming, Career]
---
{% include JB/setup %}

##Python and SQL

Mac真是一个好系统，我自从迁移到Mac之后，写代码也比以前写得多了很多，成为一个业余的编程高手的信心和兴趣空前高涨。Mac上对Python和SQLite3都有很好的支持，今天成功的将一个超小的个人项目的数据从文本文档迁移到了SQLite3上面。


Python由[sqlite3](http://docs.python.org/library/sqlite3.html)这个模块来提供对SQLite3的接口。下面是今天学到的一些小细节：

1. sqlite3.connect(“exemple.db”)函数用于连接数据库，如果数据库不存在，该函数还会新建数据库。
2. "create table if not exists"这句SQL语句的意思是，如果表不存在，则建立该表。
3. "select count(id) from Item"可以返回表内数据的个数。
4. 这个[地址](http://sql.1keydata.com/cn/)可以查阅SQL的语法。


##霸王别姬

真想不到陈凯歌拍的[霸王别姬](http://movie.douban.com/subject/1291546/)是如此牛逼的一部电影，非常喜欢，看完也非常难受。我的难受来自最近的社会习文和自身经历，因为我悲哀地发现，文革离我们并没有想象的那么远，它存在与爱国抗日自相残害活动中，它也存在与华为的残忍群面中……

最后我想对自己说，别着急，日拱一卒，先养成好的习惯，再去攻克宏大的目标。