---
layout:     post
title:      "Numpy02_pandas"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-16 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---


#### pandas

> **pandas是numpy的一种工具，该工具是为了解决数据分析任务而创建的**

- **数据分析三剑客**

		import numpy as np
		import pandas as pd
		from pandas import Series,DataFrame



- **Series**
> **Series类似于一位数组的对象，由两部分组成：**
 
	- values： adarray类型数据
	- index ： 相关数据的索引标签
	- s.loc[index] = value : 根据键取值
	- s.iloc[原始索引index] = value：根据原始列表索引值去值
	- s.size: 长度
	- s.values: 值
	- s.index: 键
	- s.add(s1,fill_value=0)：含有nan值的列表相加


			import numpy as np
			import pandas as pd
			from pandas import Series,DataFrame
			n1 = np.array(["语文","数学","英语"])
			n2 = np.array([120,140,110])
			data = Series(data=n2, index=n1)
			print(data)

			ou：	语文    120
					数学    140
					英语    110
					dtype: int32

			data = Series(['i','love','you'])
			print(data)

			ou：0       i
				1    love
				2     you
			
			data = Series({"语文":120,"数学":145,"英语":70})
			print(data)


			ou:	 数学    145
					英语     70
					语文    120
					dtype: int64

			
			data.isnull()  #面向对象
			pd.isnull(data)#面向过程

			数学    False
			英语    False
			语文    False
			dtype: bool

			in：s1 = Series([1,2,3,4])
				list1 = [True,True,False,False]
				print(s1[list1])
			ou：0    1
				1    2
				dtype: int64

 			#两个列表相加运算处理
			n1 = np.array([1,2,np.nan,4,5])
			n2 = np.array([3,4,5,6,np.nan])
			
			s1 = Series(n1)
			s2 = Series(n2)
			s3 = s1.add(s2,fill_value=0)
			print(s3)

			ou：0     4.0
				1     6.0
				2     5.0
				3    10.0
				4     5.0
				dtype: float64



- **DataFrame**

> **DataFrame就是多行Series摞在一起**
> 
> **df = DataFrame(columns=列索引，indexs=行索引，data=矩阵)**
> 
> **行索引：df.loc[index]**
> 
> **列索引：df[列索引]**
> 
> **具体值访问： df.loc[行索引][列索引] df[列索引][行索引] df[列索引,行索引]**
> 
> **df的切片操作，df.loc[行切片，列切片]  df.iloc[行切片，列原始索引切片]**

> **DataFrame可以进行聚合操作df.sum(),df.mean()**


			import numpy as np
			import pandas as pd
			from pandas import Series,DataFrame
			n1 = np.array([[150,0],[150,0],[150,0],[300,0]])
			columns = ["张三", "李四"]
			index = ["语文","数学","英语","理综"]
			data = DataFrame(columns=columns,index=index,data=n1)
			print(data)
			#行索引
			print(data.loc["语文"])
			#列索引
			print(data["张三"])


			ou：    	  张三  李四
					语文  150   0
					数学  150   0
					英语  150   0
					理综  300   0

					张三    150
					李四      0
					Name: 语文, dtype: int32

					语文    150
					数学    150
					英语    150
					理综    300
					Name: 张三, dtype: int32
			


			n1 = np.array([[150,0,15],[150,0,12],[150,0,13],[300,0,58]])
			columns = ["张三", "李四","王五"]
			index = ["语文","数学","英语","理综"]
			data = DataFrame(columns=columns,index=index,data=n1)
			print(data)
			print(data.loc[:,"王五":"王五"].sum())
			print(data["张三"])

			ou:     张三  李四  王五
				语文  150   0  15
				数学  150   0  12
				英语  150   0  13
				理综  300   0  58

				#sum后的结果
				王五    98  
				dtype: int64

				语文    150
				数学    150
				英语    150
				理综    300
				Name: 张三, dtype: int32




- **创建多行索引**
	- **隐式构造**
		> **就是在columns，indexs中从一个维数组变为多维数组** 
	- **显示创建（三种方式）**
	

	




				import numpy as np
				import pandas as pd
				from pandas import Series,DataFrame
				#隐式创建
				columns = [["张三","张三","李四","李四"],["期中","期末","期中","期末"]]
				indexs = ["数学","语文","英语","理综"]
				data = np.random.randint(50,150,size=(4,4))
				pd1 = DataFrame(columns=columns, index=indexs, data=data)
				print(pd1)
				#显示创建
				#1、数组方式创建和隐式创建类似
				columns = pd.MultiIndex.from_arrays([["张三","张三","李四","李四"],["期中","期末","期中","期末"]])
				indexs = ["数学","语文","英语","理综"]
				data = np.random.randint(50,150,size=(4,4))
				pd1 = DataFrame(columns=columns, index=indexs, data=data)
				print(pd1)
				#2、元组方式创建
				columns = pd.MultiIndex.from_tuples((("张三","期中"),("张三","期末"),("李四","期中"),("李四","期末")))
				indexs = ["数学","语文","英语","理综"]
				data = np.random.randint(50,150,size=(4,4))
				pd1 = DataFrame(columns=columns, index=indexs, data=data)
				print(pd1)
				#3、以产品方式创建（使用简单，推荐）
				columns = pd.MultiIndex.from_product([("张三","李四"),("期中","期末")])
				indexs = ["数学","语文","英语","理综"]
				data = np.random.randint(50,150,size=(4,4))
				pd1 = DataFrame(columns=columns, index=indexs, data=data)
				print(pd1)




- **堆的索引**

	- **列索引转行索引: pd.stack(level=0/1)...0是外层，1是第二层。。。**
	- **行索引转列索引: pd.unstack(level=0/1)**


- **pandas
- （默认纵向级联）**
	- **pd.concat((pd1,pd2),axis=0/1，ignore_index=False(默认)/True) #1横向0纵向  行列数不匹配会默认NAN值， ignore_index=True会把索引重复的值重新生成变成不重复**
	- **pd.concat((pd1,pd2),axis=0/1，keys=[A,B])  重复索引外层添加多级索引**
	- **pd.concat((pd1,pd2),join='outter'(默认)/'inner')#当设置成inner就值去重复索引进行级联而不是给不重复索引补NAN值，通常选择outner，因为不希望丢失数据**


			import matplotlib.pyplot as plt
			import pandas as pd
			import numpy as np
			from pandas import Series,DataFrame
			index = ['a','b','c','d','e']
			col = [1,2,3,4,5]
			def df(col, index):
			    return DataFrame(columns=col,index=index,data=[[i+str(j) for j in col] for i in index])
			df1 = df(col,index)
			df2 = df(col,index)
			print(pd.concat((df1,df2),axis=1))

			
			    1   2   3   4   5   1   2   3   4   5
				a  a1  a2  a3  a4  a5  a1  a2  a3  a4  a5
				b  b1  b2  b3  b4  b5  b1  b2  b3  b4  b5
				c  c1  c2  c3  c4  c5  c1  c2  c3  c4  c5
				d  d1  d2  d3  d4  d5  d1  d2  d3  d4  d5
				e  e1  e2  e3  e4  e5  e1  e2  e3  e4  e5

			
			print(pd.concat((df1,df2),axis=0))


				    1   2   3   4   5
					a  a1  a2  a3  a4  a5
					b  b1  b2  b3  b4  b5
					c  c1  c2  c3  c4  c5
					d  d1  d2  d3  d4  d5
					e  e1  e2  e3  e4  e5
					a  a1  a2  a3  a4  a5
					b  b1  b2  b3  b4  b5
					c  c1  c2  c3  c4  c5
					d  d1  d2  d3  d4  d5
					e  e1  e2  e3  e4  e5





			print(pd.concat((df1,df2),axis=1,keys="左右"))



					    左                   右                
					    1   2   3   4   5   1   2   3   4   5
					a  a1  a2  a3  a4  a5  a1  a2  a3  a4  a5
					b  b1  b2  b3  b4  b5  b1  b2  b3  b4  b5
					c  c1  c2  c3  c4  c5  c1  c2  c3  c4  c5
					d  d1  d2  d3  d4  d5  d1  d2  d3  d4  d5
					e  e1  e2  e3  e4  e5  e1  e2  e3  e4  e5

			#级联输入的索引
			my_index = pd.Index(data=[索引])
			print(pd.concat((df1,df2),axis=0,join_axes=[my_index]))

			my_index = pd.Index(data=[1])
			print(pd.concat((df1,df2),axis=0,join_axes=[my_index]))


- **一对一级联**
	> **df3 = pd.merge(left=df1,right=df2,how="inner"/"outer")**
	> **df1和df2级联默认inner值级联所有数据都相同的 outer是把所有数据都级联在一起**
		

- **一对多级联**

	都一样

- **多对多级联**

	都一样

- **当所有列名既key都不相同时，需要使用left_on和right_on来指定合并参照**

 > **df3 = pd.merge(left_on=列名1,right_on=列名2,how="inner"(默认)/"outer"/"left"/"right")****

- **df1.index = df1[列名] #把该列作为索引**

		index = ['a','b','c','d','e']
		col = [1,2,3,4,5]
		def df(col, index):
			return DataFrame(columns=index,index=col,data=[[j+str(i) for j in index] for i in col])
		df1 = df(col,index)
		df2 = df(col,index)
		print(df1)
		df1.index = df1["a"]
		print(df1)

		ou：    a   b   c   d   e
			1  a1  b1  c1  d1  e1
			2  a2  b2  c2  d2  e2
			3  a3  b3  c3  d3  e3
			4  a4  b4  c4  d4  e4
			5  a5  b5  c5  d5  e5
			
			#将a左右行索引
			     a   b   c   d   e
			a                     
			a1  a1  b1  c1  d1  e1
			a2  a2  b2  c2  d2  e2
			a3  a3  b3  c3  d3  e3
			a4  a4  b4  c4  d4  e4
			a5  a5  b5  c5  d5  e5

- **当两个表索引完全不相同时正常合并就行不通了，但是正好某列与前表的索引有相同的数据，这样就可以把第一章表的索引和第二张表的某列进行合并使用：pd.merge(pd1,pd2,left_on="a",right=df2.index,suffixes=[左下标起别名，有下标起别名])**


			index = ['a','b','c','d','e']
			col = [1,2,3,4,5]
			def df(col, index):
				return DataFrame(columns=index,index=col,data=[[j+str(i) for j in index] for i in col])
			df1 = df(col,index)
			df2 = df(col,index)
			df2.index = df2["a"]
			df3 = pd.merge(df1,df2,left_on="a",right_index=True,suffixes=["df1","df2"])
			print(df3)

			
			ou：	a  a左  b左  c左  d左  e左  a右  b右  c右  d右  e右
				1  a1  a1  b1  c1  d1  e1  a1  b1  c1  d1  e1
				2  a2  a2  b2  c2  d2  e2  a2  b2  c2  d2  e2
				3  a3  a3  b3  c3  d3  e3  a3  b3  c3  d3  e3
				4  a4  a4  b4  c4  d4  e4  a4  b4  c4  d4  e4
				5  a5  a5  b5  c5  d5  e5  a5  b5  c5  d5  e5


- **条件查询**

	- **df3.query("姓名=='张三' & 语文>120")**


		
			column = ["姓名","语文","数学","英语","理综"]
			data = [["张三",120,113,50,30],["李四",120,34,89,80],["王五",20,50,89,56]]
			df1 = DataFrame(columns=column,data=data)
			data1 = [["张三",121,113,50,30],["赵小六",120,89,120,112]]
			df2 = DataFrame(columns=column,data=data1)
			df3 = pd.merge(df1,df2,how="outer")
			print(df3.query("姓名=='张三' & 语文>120"))

			ou：   姓名   语文   数学  英语  理综
				3  张三  121  113  50  30


- **去重**

	- **df.unique()#用于查询到多条重复数组，只需要知道每个重复数据的名字**



			column = ["姓名","语文","数学","英语","理综"]
			data = [["张三",120,113,50,30],["李四",120,34,89,80],["王五",20,50,89,56]]
			df1 = DataFrame(columns=column,data=data)
			data1 = [["张三",121,113,50,30],["赵小六",120,89,120,112]]
			df2 = DataFrame(columns=column,data=data1)
			df3 = pd.merge(df1,df2,how="outer")
			
			print(df3[df3["姓名"] == "张三"]["姓名"].unique() )


- **查看数据样本**

	- **df.head()**