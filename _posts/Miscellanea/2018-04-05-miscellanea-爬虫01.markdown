---
layout:     post
title:      "爬虫01"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-05 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---

> import urllib.request
  response = urllib.request.urlopen(path)#得到服务器相应
  response.read() 读取响应数据
  response.info() 得到响应体信息
  response.getcode() 得到相应状态 200ok
	
状态码
	
<img src="/img/http响应状态V1.png"/>

<img src="/img/http响应状态V2.png"/>

<img src="/img/http响应状态V3.png"/>

> url = response.geturl() #得到服务器地址

> newUrl = urllib.request.unquote(Url) # 对url地址进行解码
> newUrl1 = urllib.request.quote(newUrl) #对解码后的URL地址进行编码

	编码之后https%3A//www.google.com.hk/search%3Fq%3D%E5%9B%BE%E7%89%87%26newwindow%3D1%26safe%3Dstrict
	解码之后https://www.google.com.hk/search?q=图片&newwindow=1&safe=strict&tbm=isch&tbo=u&source=univ&sa=X&ved=0ahUKEwjHzfzTxaraAhWDlZQKHU35D2kQsAQIKw&biw=1600&bih=769
	经过url解码后就可以看到那一串16进制数名字叫图片

- 直接将URL相应的数据写入文件中

		urllib.request.urlretrieve(path1, filename = path2)

- 使用urlretrieve方法会产生缓存

		urllib.request.ulrcleanup()#清楚缓存


---
#### 爬去页面出现**UnicodeDecodeError: 'utf-8' codec can't decode byte 0x8b in position 1: invalid start byte**

这是因为有些网站进行了gzip压缩，最典型的就是sina，进行网页爬虫经常出现这个问题，那么为什么要压缩呢？

解释：
> **HTTP协议上的GZIP编码是一种用来改进WEB应用程序性能的技术。大流量的WEB站点常常使用GZIP压缩技术来让用户感受更快的速度。这一般是指WWW服务器中安装的一个功能，当有人来访问这个服务器中的网站时，服务器中的这个功能就将网页内容压缩后传输到来访的电脑浏览器中显示出来.一般对纯文本内容可压缩到原大小的40%.这样传输就快了，效果就是你点击网址后会很快的显示出来.当然这也会增加服务器的负载. 一般服务器中都安装有这个功能模块的。**

当我们打开网页之后按F12点network中的request headers中有这样一句代码
> Accept-Encoding:gzip, deflate, sdch

如果存在，删除即可解决。如果不存在可以导入gzip模块

> import gzip

在read()之后得到的data添加到gzip.decompress()方法中返回data就是正常的utf-8编码数据了，接着在decode()就可以了

> data=gzip.decompress(data)

#### 模拟浏览器，更改User-Agent  ---> 谷歌搜索  User-Agent大全

	import urllib.request
	import gzip
	url = "http://www.baidu.com"
	userAgent = "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36"
	RequestUrl = urllib.request.Request(url)
	RequestUrl.add_header("User-Agent", useragent)
	response = urllib.request.urlopen(RequestUrl)
	data = response.read()
	data = gzip.decompress(data)
	print(data)

#### get/post请求

**get请求**：直接将传递参数拼接到url后面，传给服务器
优点：传输速度快
缺点：数据量小（最大2KB），不安全

**post请求**：将数据打包，单独传输
优点：安全，数据量大
缺点：传输速度慢

post请求代码

	import urllib.request
	useragent = "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36"
	data = {
	         "pageNo":1,
	         "pageSize":20,
	         "serialIds":"2143,3404",
	         "v":"4.0.0"
	    }
	#urllib.parse.urlencode把键值对转换成pageNo=1&pageSize=20这种形式
	postData = urllib.parse.urlencode(data).encode('utf-8')
	requestUrl = urllib.request.Request("http://mrobot.pcauto.com.cn/v2/cms/channels/1", postData)
	requestUrl.add_header("User-Agent", useragent)
	response = urllib.request.urlopen(requestUrl)
	data = response.read().decode('utf-8')
	print(data)


#### Json

> json就是一种数据格式，实际就是字符串
> Json数据可以保存到文件，也可以用作网络的数据传输，轻量级数据
格式 {} 代表对象 
	[] 代表列表
	： left属性right值
	， 两个值的分割

- json.loads(str)  #将字符串转为字典
- json.dumps(dict) #将字典转换成字符串

测试代码

	import json
	jsonDate = '{"name":"suny","age":20, "gender":"man", "Hobby":["game", "coding", "sleep"]}'
	strToJson = json.loads(jsonDate)
	JsonTostr = json.dumps(jsonDate)
	print(type(strToJson))
	print(type(JsonTostr))
	>>> <class 'dict'>
		<class 'str'>
	
	
	
#### 爬虫基础demo

- 爬取贴吧内的QQ号

		import urllib.request
		import re
		QQList = []
		def spiter(urlPath, QQList):
			#匹配QQ号正则
		    rep = r"[Q]{1,2}.[1-8][0-9]{4,}|[1-8][0-9]{4,}[Q]{1,2}"
			#更换内核
		    userAgent = "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36"
		    urlRequest = urllib.request.Request(urlPath)
		    urlRequest.add_header("User-Agent", userAgent)
		    response = urllib.request.urlopen(urlRequest)
		    data = response.read().decode("utf-8")
		    data = re.findall(rep, data,re.I)
		    QQList+=data
		if __name__ == "__main__":
			#多页抓取
			for page in range(1,11):  
			    url = "http://bbs.tianya.cn/post-140-393974-"+str(page)+".shtml"
			    spiter(url, QQList)
			QQNumList = []
			#摘取纯QQ号
			for i in range(len(QQList)):
			    QQNum = re.findall(r'[1-8][0-9]{4,}', QQList[i])
			    QQNumList.append("".join(QQNum))
			print(QQNumList)



	
