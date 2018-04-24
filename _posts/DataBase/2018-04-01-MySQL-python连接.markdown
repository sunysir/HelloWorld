---
layout:     post
title:      "python连接数据库"
subtitle:   " \"Hello World, Hello Blog\""
date:        2018-04-10 11:00:00
author:     "suny"
catalog: true
categories: MySQL
tags:
    - 笔记
---
python连接数据库首先安装第三方库pymysql

在cmd中输入

		pip install pymysql

很简单直接上代码吧





		
		import pymysql
		#连接数据库 参数1：服务器地址，参数2：账号，参数3：密码，参数4：数据库名，参数5：设置编码
		db = pymysql.connect("localhost","root","123456","test",charset = "utf8")
		#创建游标
		cursor = db.cursor()
		#没有成功执行数数据库回滚db.rollback()
		try:
		    #正常的sql语句跟直接操作数据库没区别
		    sql = "INSERT INTO classinfo VALUES (0,'qq',2)"
		    #执行sql语句
		    cursor.execute(sql)
		    #执行增删改查的时候必须要提交一下
		    db.commit()
		except:
		    print("回滚了")
		    db.rollback()
		#关闭游标和数据库
		cursor.close()
		db.close()


上面实现了连接数据，但是每次使用都需要调用重复数据，因此很有必要封装一下起名叫DBUtils吧


		
DBUtiles.py


		import pymysql
		class DBUtiles(object):
		    def __init__(self, url, username, password, dbName):
		        self.url = url
		        self.username = username
		        self.password = password
		        self.dbname = dbName
		    def connect(self):
		        #连接数据库 参数1：服务器地址，参数2：账号，参数3：密码，参数4：数据库名，参数5：设置编码
		        self.db = pymysql.connect(self.url ,self.username ,self.password ,self.dbname ,charset = "utf8")
		        #创建游标
		        print("数据库连接成功...")
		        self.cursor = self.db.cursor()
		        #没有成功执行数数据库回滚db.rollback()
		    def sqlContext(self,sql):
		        self.connect()
		        try:
		            #执行sql语句
		            self.cursor.execute(sql)
		            #执行增删改查的时候必须要提交一下
		            self.db.commit()
		            print(self.cursor.fetchall())
		        except:
		            print("回滚了")
		            self.db.rollback()
		    #关闭游标和数据库
		    def close(self):
		        self.cursor.close()
		        self.db.close()
