---
layout:     post
title:      "py基础02"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-03-20 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 生活
---




**py单元测试模块**

python代码
	
	----
	test1包
	----
	def sum(a, b):
    	return a + b 
	def sub(a, b):
    	return a - b 
	----
	test包
	----
	import unittest
	from test1 import sum
	from test1 import sub
	
	class myUnitTest(unittest.TestCase):
	    def setUp(self):
	        print("start")
	    def tearDowm(self):
	        print("end")
	
	    def test_sum(self):
	        self.assertEquals(sum(1,2), 3, "error!" )
	
	    def test_sub(self):
	        self.assertEquals(sub(1,2), -1, "error!" )
	    
	if __name__ == "__main__":
	    unittest.main()
	---
	run结果
	---
	start

	Warning (from warnings module):
	  File "C:\Users\suny\Desktop\test.py", line 14
	    self.assertEquals(sub(1,2), -1, "error!" )
	DeprecationWarning: Please use assertEqual instead.
	.start
	.
	----------------------------------------------------------------------
	Ran 2 tests in 0.016s
	
	OK
	---
	----
	test1包
	----
	def sum(a, b):
    	return a + b +1
	def sub(a, b):
    	return a - b -1
	----
	---
	run结果
	---
	Traceback (most recent call last):
	  File "C:\Users\suny\Desktop\test.py", line 14, in test_sub
	    self.assertEquals(sub(1,2), -1, "error!" )
	AssertionError: -2 != -1 : error!
	
	======================================================================
	FAIL: test_sum (__main__.myUnitTest)
	----------------------------------------------------------------------
	Traceback (most recent call last):
	  File "C:\Users\suny\Desktop\test.py", line 11, in test_sum
	    self.assertEquals(sum(1,2), 3, "error!" )
	AssertionError: 4 != 3 : error!
	
	----------------------------------------------------------------------
	Ran 2 tests in 0.024s
	
	FAILED (failures=2)

---

---

**TCP/IP基础**
> **TCP是建立可靠的连接，并保障通信双方都能够以流的形式去发送接收数据，需要三次握手才能够建立通讯**

**模拟客户端向服务器发送请求**

python代码

	import socket
	Date = []
	#创建socket客户端
	#参数1：ip协议标准,socket.AF_INET为ip协议4标准 AF_INET6为ip协议6标准
	#参数2：表示流的传输形式
	clientSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
	#连接服务器
	clientSocket.connect(("www.baidu.com",80))
	#向服务器发送请求
	clientSocket.send(b"GET / HTTP/1.1\r\nHOST:www.baidu.com\r\nConnection:close\r\n\r\n")
	f = open("C:/Users/suny/Desktop/baidu.html", "wb")
	#接受内容
	while True:
	    tempDate = clientSocket.recv(1024)
	    if tempDate:
	        Date.append(tempDate)
	        f.write(tempDate)
	    else:
	        break
	f.close()
	#把头和体分别存到两个html文件中
	f1 = open("C:/Users/suny/Desktop/head.html", "w",encoding='UTF-8')
	f2 = open("C:/Users/suny/Desktop/body.html", "w",encoding='UTF-8')
	newDate = (b"".join(Date)).decode(encoding="utf-8")
	(head,body) = newDate.split("\r\n\r\n",1)
	for each_line in head:
	    f1.writelines(each_line)
	for each_line in body:
	    f2.writelines(each_line)
	    
	f1.close()
	f2.close()

**模拟服务器**

python代码

	import socket
	#创建服务器
	serviceSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
	#绑定服务ip地址并设定端口号
	serviceSocket.bind(("172.30.14.4", 8001))
	#设置连接用户数量
	serviceSocket.listen(5)
	socketClient,socketAddress = serviceSocket.accept()
	print("连接上了一个用户...")
	print(str(socketClient),socketAddress)
	while True:
	    #接受发送信息需要使用客户端连接的套接字socketClient,而不能使用没有任何连接的服务器套接字serviceSocket
	    clientContext = socketClient.recv(1024)
	    print("客户端说:%s"%str(clientContext.decode("utf-8")))
	    servContext = input("服务器说: ")
	    socketClient.send(servContext.encode("utf-8"))

---

---

**UDP**
> **UDP是面向无连接的协议，使用UDP协议时，不需要建立连接，只需要知道对方的IP地址和端口号，就可以直接发送数据包，但是对面能不能接收到就不管了。虽然UDP传输数据不可靠，但是其优点就是传输速度比TCP要快很多，对要求不高的数据可以使用UDP进行传输**

**模拟UDP服务器**

python代码

	import socket
	#创建服务器
	udpServer = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
	#绑定服务器IP地址并设置端口号
	udpServer.bind(("172.30.14.4", 8001))
	while True:
	    #data位接受到的数据,address为客户端IP地址及端口号
	    data,address = udpServer.recvfrom(1024)
	    print("客户端说: %s"%data.decode("utf-8"))

**模拟UDP客户端**

python代码

	import socket

	clientSocket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
	#连接服务器
	clientSocket.connect(("172.30.14.4",8001))
	while True:
	    data = input("客户端说:")
	    clientSocket.send(data.encode("utf-8"))








