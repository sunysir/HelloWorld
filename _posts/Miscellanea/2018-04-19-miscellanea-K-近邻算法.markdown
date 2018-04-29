---
layout:     post
title:      "K-近邻算法(KNN)"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-19 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---


#### KNN

> **简单地说，K-近邻算法采用测量不同特征值之间的距离方法进行分类（k-Nearest Neighbor，KNN)。
> 优点：精度高、对异常值不敏感、无数据输入假定。**
> **缺点：时间复杂度高、空间复杂度高。**
> **--1、当样本不平衡时，比如一个类的样本容量很大，其他类的样本容量很小，输入一个样本的时候，K个临近值中大多数都是大样本容量的那个类，这时可能就会导致分类错误。改进方法是对K临近点进行加权，也就是距离近的点的权值大，距离远的点权值小。 **
> **--2、计算量较大，每个待分类的样本都要计算它到全部点的距离，根据距离排序才能求得K个临近点，改进方法是：先对已知样本点进行剪辑，事先去除对分类作用不大的样本。**
> 
> **适用数据范围：数值型和标称型**
> **-- 标称型：标称型目标变量的结果只在有限目标集中取值，如真与假(标称型目标变量主要用于分类)**
> **--数值型：数值型目标变量则可以从无限的数值集合中取值，如0.100，42.001等 (数值型目标变量主要用于回归分析)**


python简单测试（分类）



			import numpy as np
			import pandas as pd
			from sklearn.neighbors import KNeighborsClassifier
			#预测该学生是好学生还是坏学生 GPA,获奖数,六级分数
			#训练需要的数据
			x_train = [[2.0,0,250],[4.0,8,600],[3.5,5,425],[3.0,2,400],[2.8,1,350],[2.3,4,250],[2.7,3,425],[1,0,250]]
			y_train = ["bad","good","good","mid","mid","bad","mid","bad"]
			#导入模型n_neighbors默认参数为5
			knnclf = KNeighborsClassifier(n_neighbors=5)
			#导入数据进行训练
			knnclf.fit(x_train,y_train)
			#预测数据
			data = knnclf.predict([[1,0,200],[2.0,0,400]])
			print(data)


python sklearn包的KNN鸢尾花测试数据



			import sklearn.datasets as datasets
			from sklearn.neighbors import KNeighborsClassifier
			from matplotlib import pyplot as plt
			from matplotlib.colors import ListedColormap
			import numpy as np
			#导入鸢尾花训练数据
			iris = datasets.load_iris()
			#取数据前两位为训练数据，target为鸢尾花颜色结果
			data = iris.data[:,:2]
			target = iris.target
			#导入KNN分类模型
			knffc = KNeighborsClassifier(n_neighbors=5)
			#导入数据进行训练
			knffc.fit(data,target)
			#创建测试数据
			x_min = data[:,0].min();x_max = data[:,0].max()
			y_min = data[:,1].min();y_max = data[:,1].max()
			x_list = np.arange(x_min,x_max,0.01)
			y_list = np.arange(y_min,y_max,0.01)
			xx,yy = np.meshgrid(x_list,y_list)
			x_list = xx.ravel();y_list = yy.ravel()
			test = np.c_[x_list,y_list]
			#导入测试数据预测结果
			res = knffc.predict(test)
			cmap = ListedColormap(["#ff0000","#00ff00","#0000ff"])
			#绘制离散图
			plt.scatter(x_list,y_list,c=res)
			plt.scatter(data[:,0],data[:,1],c=target,cmap=cmap)
			plt.show()


<img src="/img/KNNyuanweihua.jpg">