---
layout:     post
title:      "正则表达式"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-03-20 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---





#### 正则表达式概述

> **正则表达式通常是用来检索，替换那些符合某个模式(规则)的文本。自python1.5起提供了re模块，它提供了perl风格的正则表达式，re模块使得python语言拥有全部的正则表达式功能。**

- **re.match(pattern, string, flags) **
- **re.search(pattern, string, flags)**
- **re.findall(pattern, string, flags)**

> **pattern：匹配字符串的规则，既正则表达式 string：需要用字符串匹配的字符串**
> 
> **re.match()方法是尝试从字符串的起始位置开始匹配，以对象的形式返回值，如果起始位置匹配不上，则匹配失败**
> **re.search()方法是检索整个字符串，以对象的形式返回第一个匹配项**
> 
> **re.findall()方式是检索整个字符串，以元组的形式返回全部匹配项的位置**
> 
> **re.I     忽略大小写
>
  re.M	   多行匹配，影响 ^ 和 $
>
  RE.L	做本地化识别（LOCALE-AWARE）匹配
>
 **RE.S	使 . 匹配包括换行在内的所有字符**

> 
  RE.U	根据UNICODE字符集解析字符。这个标志影响 \W, \W, \B, \B.
>
  RE.X	该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。**




python代码演示

	---
	r1 = re.match("www", "www.baidu.com")
	print(r1.span())
	>>> (0, 3)
	---
	r2 = re.match("www", "Www.baidu.com")
	print(r2)
	>>> None
	r2 = re.match("www", "Www.baidu.com",re.I)
	print(r2)
	>>> <_sre.SRE_Match object; span=(0, 3), match='Www'> #返回的是对象
	---
	r3 = re.match("www", "baidu.www.com")
	print(r3)
	>>> None
	---
	r4 = re.search("www", "baidu.www.com.www")
	print(r4.span())
	>>> <_sre.SRE_Match object; span=(6, 9), match='www'>
	---
	r5 = re.findall("www", "baidu.www.com.www")
	print(r5)
	>>> ['www', 'www']
	---

#### 匹配单个字符和数字

- **. 表示匹配任意字符,除了换行符**

- **[0-9] \d  表示匹配0到9中的任意数字**

- **[^0-9] \D   表示匹配非数字的任意字符**
 
- **[a-z]表示匹配任意小写字母**
 
- **[A-Z]表示匹配任意大写字母**
 
- **[2578]表示匹配3、5、7、8中任意数字**
 
- **[a-zA-Z0-9_] \w 表示匹配任意大小写字母数字以及下划线**

- **[^a-zA-Z0-9_] \W  表示匹配除了任意大小写字母数字以及下划线其他所有字符**

- **^取反符号[^abc]表示除了abc的所有字符，[^a-z]表示除了小写字母以外的所有字符**

- **\s 表示匹配任何空白字符， 包括空格、换页符、换行符、回车、制表符等等，等价于[\f\n\r\t]**

- **\S 表示匹配任何非空白字符，等价于[^\f\n\r\t]**

#### 边界字符

- **^ 表示边界字符，表示字符的开头，注意与[ ]中的^意义不同**

- **$ 表示边界字符，表示字符的结尾**

- **\A 表示边界字符, 表示字符的开头，这里与^的区别是，在re.M的(多行匹配)模式下， ^在新行重新匹配，而在\A不会重新匹配**

- **\Z 表示边界字符，表示字符的结尾，这里与^的区别是，在re.M的(多行匹配)模式下， ^在新行重新匹配，而在\A不会重新匹配**

- **\b 放到单词结尾表示匹配单词的结尾，表示单词尾部与空格之间。放到单词开头，则表示匹配单词的开头。例如，er\b只能匹配never say中的er,而不能匹配nerve中的er**

- **\B 表示匹配非单词的结尾，例如，er\b只能匹配nerve中的er,而不能匹配never say中的er**

python代码测试

	import re
	str1 = "dabcabcdabcdaabcdab"
	print(re.findall(r"^abc", str1,re.M))
	print(re.findall(r"\Aabc", str1,re.M))
	print(re.findall(r"abc$", str1,re.M))
	print(re.findall(r"abc\Z", str1,re.M))
	print(re.findall(r"abc\b", str1,re.M))
	print(re.findall(r"abc\B", str1,re.M))
	>>> []
		[]
		[]
		[]
		[]
 

#### 字符数量匹配

- **x? 匹配0个或者1个（非贪婪模式）** 

- **x+匹配至少一个（贪婪模式）****

- **x*匹配0个或者多个（贪婪模式）**

- **x{n}匹配n个x**

- **x{n,}匹配至少n个x**

- **x{n，m}匹配至少n个x至多m个x**

- **x | y匹配x或者y**


python测试代码

	import re
	str = "abcaabcaaaaaabbcabc"
	l1 = re.findall(r"a?", str)
	l2 = re.findall(r"a*", str)
	l3 = re.findall(r"a+", str)
	l4 = re.findall(r"a{3}", str)
	l5 = re.findall(r"a{2,}", str)
	l6 = re.findall(r"a{2,3}", str)
	l7 = re.findall(r"a|b", str)
	print(l1)
	print(l2)
	print(l3)
	print(l4)
	print(l5)
	print(l6)
	print(l7)
	>>> ['a', '', '', 'a', 'a', '', '', 'a', 'a', 'a', 'a', 'a', 'a', '', '', '', 'a', '', '', '']
		['a', '', '', 'aa', '', '', 'aaaaaa', '', '', '', 'a', '', '', '']
		['a', 'aa', 'aaaaaa', 'a']
		['aaa', 'aaa']
		['aa', 'aaaaaa']
		['aa', 'aaa', 'aaa']
		['a', 'b', 'a', 'a', 'b', 'a', 'a', 'a', 'a', 'a', 'a', 'b', 'b', 'a', 'b']


<br></br>

---

---

#### Demo

- 匹配电话号码

> **中国电信号段
133、149、153、173、177、180、181、189、199
中国联通号段
130、131、132、145、155、156、166、175、176、185、186
中国移动号段
134(0-8)、135、136、137、138、139、147、150、151、152、157、158、159、178、182、183、184、187、188、198**

python代码

	import re
	def phoneMatch(str):
	    rule = r"1[3,4,5,7,8]\d{9}"
	    res = re.match(rule,str)
	    if res != None:
	        return True
	    else:
	        return False
	    
	phone = "15104652756"
	res = phoneMatch(phone)
	print(res)

- 匹配QQ号

	腾讯QQ号从10000开始，目前最高11位

python代码

	import re
	def QQMatch(str):
	    rule = r"[1-9]\d{4,11}"
	    res = re.match(rule,str)
	    if res != None:
	        return True
	    else:
	        return False
	    
	QQ = "694190253"
	res = QQMatch(QQ)
	print(res)

-匹配邮箱

python代码

	import re
	def emailMatch(str):
	    rule = r"\w+@\w+\.[a-zA-Z]{2,3}"
	    res = re.match(rule,str)
	    if res != None:
	        return True
	    else:
	        return False
	    
	email = "a694190253@gmail.com"
	res = emailMatch(email)
	print(res)


匹配日期 （测试为考虑二月）

python代码
	
	import re
	def dateMatch(str):
	    rule = r"(19[7-9]\d|20[1]\d)[-]([0]\d|[1][1-2])[-]([0-2]\d|[3][0-1])"
	    res = re.match(rule,str)
	    if res != None:
	        return True
	    else:
	        return False
	    
	date = "2019-06-12"
	res = dateMatch(date)
	print(res)


#### 分割字符串



- **str.spilt(" ")升级版re.spilt(" +", str)可以使用贪婪模式**

python测试代码

	import re
	str3 = "you are   a good  man  but      we   are   not   suitable"
	str1 = re.split(" +",str3)
	str2 = str3.split(" ")
	print(str1)
	print(str2)
	>>> ['you', 'are', 'a', 'good', 'man', 'but', 'we', 'are', 'not', 'suitable']
		['you', 'are', '', '', 'a', 'good', '', 'man', '', 'but', '', '', '', '', '', 'we', '', '', 'are', '', '', 'not', '', '', 'suitable']

- **re.finditer("rule", str)返回一个迭代器**

python测试代码

	import re
	str3 = "you are   a good  man  but      we   are   not   suitable"
	iteror = re.finditer("are", str3)
	while True:
		#抛出迭代器异常
	    try:
	        info = next(iteror)
	        print(info)
	    except StopIteration as e:
	        break
	>>> <_sre.SRE_Match object; span=(4, 7), match='are'>
		<_sre.SRE_Match object; span=(37, 40), match='are'>

#### 字符串的替换

- re.sub("待替换字符str","替换字符rep","查找的字符串"string，匹配次数count)
- re.subn("待替换字符str","替换字符rep","查找的字符串"string，匹配次数count)
- **区别是第一个返回字符串string，而第二个返回一个记录了匹配个数的元组**

测试代码

	import re
	str1 = "i good love good you "
	print(re.sub("good", "very", str1))
	print(re.subn("good","very",str1,0))
	>>> i very love very you #返回字符串
		('i very love very you ', 2)#返回元组


#### 字符串分组
	
	rep = r"()()()"#括号中为局部正则表达式
	res = re.match(rep,string,flag)
	res = re.finall(rep,string,flag)
	res = re.search(rep,string,flag) 
	res.groups()返回一个元组，把各自括号内匹配到的字符串依次传入元组中
	res.group(n) n = 0表示返回整个匹配字符串 n = 1，2，3...表示第一个第二个....括号内的元素

测试代码
	
	import re
	str1 = "13704857429"
	rep = r"(1[3457])(\d{9})"
	res = re.match(rep, str1)
	print(res.group(0))
	print(res.group(1))
	print(res.group(2))
	>>> 3704857429  (type->str)
		13
		704857429
	

#### 正则表达式的预编译

当匹配次数过大的时候预编译的作用就体现出来了，只需要编译一次就可以解决问题

测试代码

	import re
	re_pho = re.compile(r"(1[3457])(\d{9})")
	str1 = "13704857429"
	res = re_pho.match(str1)
	print(res.group(0))
	print(res.group(1))
	print(res.group(2))
	>>> 3704857429  (type->str)
		13
		704857429