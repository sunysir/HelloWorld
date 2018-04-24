---
layout:     post
title:      "Numpy01"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-15 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 生活
---

- **ndarrayAPI**


		import numpy as np
		n1 = np.array([1,2,3])
		# print(n1)
		n2 = np.ones((2,3),dtype=int)
		# print(n2)
		n3 = np.eye(3,3,dtype=int) #np.eye(x1,x2,dtype=int，1/-1) 几个x代表几行几列单位矩阵1代表1右移-1代表左移一位
		#print(n3)
		n4 = np.linspace(0,100,20) #np.linspace(start,end,n) start到end范围等分n分生成一个列表
		# print(n4)
		n5 = np.arange(0,95,10) #np.arange(start,end,n) 生成start到end步长为n的一个列表
		# print(n5)
		n6 = np.random.randint(1,20,3) #np.random.randint(start,end,n) 生成start到end范围内n个随机数
		print(n6)
		n7 = np.random.randn(3,3)   #np.random.randn(x1,x2,...)几个数代表几维
		# print(n7)
		n8 = np.random.random(10)   #np.random.random(n) 生成n个0-1的随机数
		# print(n8)
		n9 = np.ones((3,3),dtype=int)
		# print(n9)
		n10 = np.zeros((3,3),dtype=int)
		# print(n10)
		n11 = np.full((3,3),fill_value=0,dtype=int)
		print(n11)

- **ndarray属性**

	- **ndim：维度**
	- **shape：形状**
	- **size：长度**
	- **dtype：元素类型**


		import numpy as np
		n1 = np.random.random(10)
		print(n1.size,n1.dtype,n1.shape,n1.ndim)	

- **多维数组的切片**

		[1:,1:]  二维数组的切片

		n11 = np.random.randn(3,3)
		print(n11)
		#第三行第二列开始切片
		print(n11[2:,1:]) 

	    >>>
		[[ 0.92124302  0.16665547  1.94053302]
	    [ 0.07277247  0.63885215 -0.86742746]
		[-0.94445058  0.52956157  0.28216491]]
	    [[0.52956157 0.28216491]]

- **变形**

n1.reshape((row,column))将列表变为相应维度
	
	import numpy as np
	n1 = np.random.randint(100,150,25)
	print(n1)
	print(n1.reshape((5,5)))

- **级联**

		import numpy as np
		n1 = [1,2,3]
		n2 = [4,5,6]
		#axis 0表示一维方向，1表示二维方向
		n3 = np.concatenate((n1,n2),axis=0)
		print(n3)
		#横向级联
		n4 = np.hstack((n1,n2))
		print(n4)
		#纵向级联
		n5 = np.vstack((n1,n2))
		print(n5)

- **切分**
- 

		import numpy as np
		n1 = np.random.randint(10,15,36).reshape((6,6))
		#参数1：列表  参数2：切分成几份 参数3：axis：0表示x方向，1表示y方向
		n2 = np.split(n1,2,axis=1)
		#参数1：列表  参数2：切分成3份，3之前一份，3,4之间一份，4之后一份
		n3 = np.split(n1,(3,4))
		print(n1)
		print(n2)
		print(n3)
 		>>>
 		 n1
		 [[12 10 10 13 12 10]
		 [14 13 13 13 10 13]
		 [12 10 11 11 12 11]
		 [14 14 12 14 13 13]
		 [10 10 11 11 14 14]
		 [10 13 11 11 10 14]]
		n2
		[array([[12, 10, 10],
		       [14, 13, 13],
		       [12, 10, 11],
		       [14, 14, 12],
		       [10, 10, 11],
		       [10, 13, 11]]), array([[13, 12, 10],
		       [13, 10, 13],
		       [11, 12, 11],
		       [14, 13, 13],
		       [11, 14, 14],
		       [11, 10, 14]])]
 		n3
		[array([[12, 10, 10, 13, 12, 10],
		       [14, 13, 13, 13, 10, 13],
		       [12, 10, 11, 11, 12, 11]]), array([[14, 14, 12, 14, 13, 13]]), array([[10, 10, 11, 11, 14, 14],
		       [10, 13, 11, 11, 10, 14]])]

- **聚合函数**

	- **n1.max()  矩阵之和**
	- **n1.min()  矩阵之差**
	- **n1.argmax() 矩阵中最大值index**
	- **n1.argmin() 矩阵中最小值index**
	- **n1.mean()   矩阵平均值**
	- **np.all() 矩阵中全为True 返回True**
	- **np.any() 矩阵中有一个为True，返回True**
	- **np.nan numpy中的空值**
	- **np.nansum(n1) 忽略n1中的空值**
	- **np.dot(n1,n2) 矩阵之积**	


		
			import numpy as np
			n1 = np.array([1,2,3])
			#最大值
			print(n1.max())
			#最小值
			print(n1.min())
			#最大值坐标
			print(n1.argmax())
			#最小值坐标
			print(n1.argmin())
			#平均值
			print(n1.mean())
			n2 = np.array([True,False,False,False])
			n3 = np.array([False,False,False,False])
			n4 = np.array([True,True,True,True])
			#np.all() 列表中所有为True才为True 否则False
			print(np.all(n4))
			print(np.all(n2))
			print(np.all(n3))
			#np.any()列表中有一个值为True就返回True
			print(np.any(n2))
			print(np.any(n3))
			print(np.any(n4))
	
			ou：	3
					1
					2
					0
					2.0
					True
					False
					False
					True
					False
					True
			
			#numpy中使用np.nan表示空值，其类型是float类型，可以进行运算，但其计算结果都是nan
			np.nan 表示 None
			
			n1 = np.array([1,2,3,np.nan])
			print(n1.sum())
			#当数组中有空值求和需要忽略空值
			print(np.nansum(n1))
			>>> nan
				6.0
	
	
			#矩阵之积
	
				in:	 n1 = np.array([1,2,3])
						n2 = np.array([[4],[5],[6]])
						print(np.dot(n1,n2))
	
				ou: 	[32]



- **广播机制**
		
	- 规则1：为缺失的维度补1
	- 规则2：固定缺失元素用已有值填充
			
			n1 = np.array([[1,2,3],[7,8,9]])
			n2 = np.array([4,5,6])
			print(n1+n2)

			ou：
				[[ 5  7  9]
 				[11 13 15]] 

- **排序**

	- n1.sort() #改变原列表进行排序
	- np.sort(n1) # 不改变原列表返回一个新的排过序的列表
	- np.partition(n1，n) # 不改变原列表返回一个新的部分排序的列表 n为正数时为正数下标索引前面部分进行排序


				
				n1 = np.array([11,2,56,1,8,34,12])
				# n1.sort()
				n2 = np.sort(n1)
				n3 = np.partition(n1,3
		
				ou：	[11  2 56  1  8 34 12]
						[ 1  2  8 11 12 34 56] 
						[ 2  1  8 11 56 34 12]

		


---


			
			import numpy as np
			import pandas as pd
			from matplotlib import pyplot as plt
			#把图片解析成三维数组[上下,左右,颜色rbg]
			img_data = plt.imread(r"C:\Users\suny\Desktop\msx.png")
			img_show = plt.imshow(img_data)
			plt.show()
			#ndarray数组切片
			img_data = img_data[::1,::-1]
			img_show = plt.imshow(img_data)
			plt.show()
			img_data = img_data[::1,::-1,::-1]
			img_show = plt.imshow(img_data)
			plt.show()





<img src="/img/msx.jpg"/>



---



