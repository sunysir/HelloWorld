---
layout:     post
title:      "py基础01"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-03-10 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 生活
---




## 请写出一段Python代码实现删除一个list里面的重复元素

想了想自己写了一个，感觉效率好低

python代码
	
	a = [1,2,2,4,4,5,6,5,7,8,2,2,2,9,0,6,6,6,6,11,6,1,11,2,2,2,2]
	def set(arr):
	    count = 0
	    list1 = []
	    flag = 0
	    for i in arr:
	        count += 1
	        for j in range(count,len(arr)):
	            if(j > len(arr)-1):
	                break
	            if arr[j] == i:
	                arr.pop(j)
	                flag+=1
	    if flag == 0:
	         return
	            
	    set(arr)
                
	set(a)
	print(a)

python自带set函数

方法1：	
		
		set(a)
		print(a)
方法2：

		b = {}
		b = b.fromkeys(a)
		c = list(b.keys())
		print(c)

---


---


**python复制对象使用** 

- 标签 = copy.copy(对象) 

- 标签 = copy.deepcopy(对象)

第一种是镜像跟随复制前的对象一起变化

第二种是把对象完全复制一份，独立存在，不受前对象影响

---

---

**python自带的数据结构**

分为可变和不可变

- 可变的有 	 ---------列表 字典 集合
- 不可变的有 	  ------元组 字符串 数

---

---

**私有成员变量的set、 get 方法**

把成员变量弄成private是封装的一种形式。便于控制对成员变量的赋值。使用set方法，提供对外访问方式，就是因为可以在访问方式中添加逻辑判断语句。对访问数据进行操作，提高代码健壮性。 而get方法多用于取值。

python中私有成员变量为变量名前面加__双下划线

get方法优化

@property

def 私有变量（无下划线）（self）：
	return self.__私有变量

set方法优化

@私有变量.setter
def 私有变量（无下划线）（self，形参）：
	self.__私有变量 = 形参

到时候就可以直接调用该私有变量了 ，不需要setget方法了

---
---

__slots__ = (--,--,--) -->元组
限制给类中动态添加的属性

动态添加方法

	class P():
		pass
	def A(self):
		---
	p = P()
	p.A = A
	P.A(A)

简便方法

	From types import MethodType
	p.A = MethodType(A, p)
	p.A -->调用方法

---
---
	

导入有序字典
	
	from collections import OrderedDict

---
---

map函数

	map(fuc, 参数1，参数2，...)#参数带入到函数中返回一个迭代器
	list1 = [1,2,3,4]	
	list1 = list(map(str, list1))
	print(list1)
	>>>['1', '2', '3', '4']
	list1 = set(map(str, list1))
	print(list1)
	>>>{'4', '2', '1', '3'}

---
---

reduce函数
	
> from functools import reduce

	reduce(fuc, list) #fuc必须有两个参数
	相当于
		temp = fuc(list[0],list[1])
		temp = fuc(temp, list[3])
		....
		最后返回一个值
		---		
		例子
		from functools import reduce
		list1 = [1,2,3,5,6]
		def add(a,b):
		    return a+b
		add1 = reduce(add, list1)
		print(add1)
		>>>17

字符串转数字

	def charToInt(char`   char为key类型`):
    return {"0":0, "1":1, "2":2, "3":3, "4":4, "5":5, "6":6, "7":7, "8":8, "9":9}[char  `char为key类型`]
	print(charToInt('9'))

filter函数

	filter(func, list1)#根据fuc返回的bool值判断是否剔除False则剔除
	---
	例子
	def isOdd(num):
	if num % 2 == 0:
		return False
	else:
		return True
	list1 = [1,2,3,4,5,6,7,8]
	list1 = list(filter(isOdd, list1))
	print(list1)
	>>>[1, 3, 5, 7]

sort函数

	list.sort()#对列表进行排序
	list2 = sort(list, key = func, reverse = True)#函数属性可以自行编写  reverse为True则对列表进行翻转排序

strip()函数

去掉字符串首尾指定字符  默认为空白字符空格回车制表符等等  [\f\n\r\t]

	a = "\tiamsuny! i am a good man!"
	print(a)
	a = a.strip()
	print(a)
	a = a.strip("!")
	print(a)
	>>>	        iamsuny! i am a good man!
		iamsuny! i am a good man!
		iamsuny! i am a good man

---


		a = [1,2,3,4]
		b = a
		b.append(5)
		print(a,b)
		>>> a = [1,2,3,4,5]
			b = [1,2,3,4,5]

	
	
	


