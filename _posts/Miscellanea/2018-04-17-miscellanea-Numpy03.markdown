---
layout:     post
title:      "Numpy03"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-17 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---


- **去除重复值**

  **查看重复值df.duplicated(keep="first"/"last")**

		
			data = {"name":["A","B","A","C","A"],"val":[123,456,123,789,123]}
			df = DataFrame(data)
			print(df.duplicated(keep="first"))


   **返回一个新的DataFrame删除重复元素df1 = df.drop_duplicates(keep="first"/"last")**

			
		
			data = {"name":["A","B","A","C","A"],"val":[123,456,123,789,123]}
			df = DataFrame(data)
			df1 = df.drop_duplicates(keep="first")
			print(df,df1)


			df
			  name  val
			0    A  123
			1    B  456
			2    A  123
			3    C  789
			4    A  123
			df1  
			0    A  123
			1    B  456
			3    C  789



   **直接修改df1 = df.drop_duplicates(keep="first"/"last"，inplace=True)**

			
	df
	  name  val
	0    A  123
	1    B  456
	3    C  789 
	
	df1
	None


- **Series和DataFrame替换  *在Series中不能识别None，不要用，在DataFrame能用**
	- **map()创建一列**
	- **replace()替换数据**
	- **rename()替换索引**
	
**单值替换**


		data = {"name":["A","B","A","C","A"],"val":[123,456,123,789,123]}
		df = DataFrame(data)
		df1 = df.replace(to_replace="B",value="替换B") 或 df1 = df.replace("B","替换B")
		print(df,df1)

		df
		  name  val
		0    A  123
		1    B  456
		2    A  123
		3    C  789
		4    A  123
		df1
		  name  val
		0    A  123
		1  替换B  456
		2    A  123
		3    C  789
		4    A  123



**字典替换（就用这个）**


		data = {"name":["A","B","A","C","A"],"val":[123,456,123,789,123]}
		df = DataFrame(data)
		df1 = df.replace({"A":"B"})
		print(df,df1)


- **多值替换和上面相同**

		pass


	
 - **指定索引替换**
 > **就举例使用字典替换，其它方式同上pd1.replace({列索引:列索引中的值},期望值),通常会创建一个范围比较大的字典**

	
			columns = ("张三","李四")
			indexs = ["数学","语文","英语","理综"]
			data = [[104,140],[131,131],[64,99],[110,75]]
			pd1 = DataFrame(columns=columns, index=indexs, data=data)
			print(pd1.replace({"张三":131},150))

			ou：     张三   李四
				数学  104  140
				语文  150  131
				英语   64   99
				理综  110   75
				
				131->150


- **list1 = df[列索引].map(字典)新增一列**

> **跟pyhon中的map函数原理一样，找到DateFrame中的一列，把该列中的每个元素都带入映射返回一个映射后的新列**


- **map(自定义函数)通过自定义函数实现自己想要得到的映射关系**

		
	

			columns = ("张三","李四")
			indexs = ["数学","语文","英语","理综"]
			data = [[104,140],[131,131],[64,99],[110,75]]
			df1 = DataFrame(columns=columns, index=indexs, data=data)
			def add_g(arr):
			    return arr+20
			list1 = df1["张三"].map(add_g)
			print(list1)

			ou: 数学    124
				语文    151
				英语     84
				理综    130
				Name: 张三, dtype: int64
	
- **transform()和map()一样，但是不能传字典**


- **rename(index=字典，columns=字典)对索引进行替换**


- **df1.describe()#描述该表每列的所有聚合操作统计**


	

			columns = ("张三","李四")
			indexs = ["数学","语文","英语","理综"]
			data = [[104,140],[131,131],[64,99],[110,75]]
			df1 = DataFrame(columns=columns, index=indexs, data=data)
			
			print(df1.describe())	 

		    ou：               张三          李四
					count    4.000000    4.000000
					mean   102.250000  111.250000
					std     28.004464   29.892864
					min     64.000000   75.000000
					25%     94.000000   93.000000
					50%    107.000000  115.000000
					75%    115.250000  133.250000
					max    131.000000  140.000000



- **过滤异常数据**


		方法一：
		#创建一个正太分数组	
		n1 = np.random.normal(size=(1000,3))
		#创建DateFrame
		n1 = DataFrame(n1)
		#过滤掉绝对值大于2倍方差的值
		print(n1[(np.abs(n1)<=2*n1.std()).all(axis=1)])




		方法二：
		n1 = DataFrame(np.random.normal(size=(1000,3)))
		print(n1.drop(n1[(n1 >= 2*n1.std()).any(axis=1)]))

- **排序：take(原索引列表，axis=0/1)函数可以对索引进行排序，交换位置等**
- **取样：   take(原索引列表不全值，axis=0/1)可以拿到相应的行或列**
- **随机取样：take(np.random.randint()，axis=0/1)可以拿到相应的行或列np.random.permutation(n)随机排列**


		n1 = DataFrame(np.random.normal(size=(3,3)))
		print(n1.take([1,2],axis=0))


		          0         1         2
			1  0.395585  1.552626 -0.332990
			2 -0.016366  0.289071  0.723056

	
- **数据分类**

> **df.groupby(列索引)#返回以当前列索引为参考列进行同类分组**
> **df.groupby(列索引).groups#查看分组后的信息**
> **df.groupby(列索引).聚合函数 or df.groupby(列索引).apply(np.聚合函数) or df.groupby(列索引).transform(np.聚合函数)**
> **apply会根据分组情况返回值，去重 **
> **transform会自动匹配列索引返回值，不去重**


	
		

