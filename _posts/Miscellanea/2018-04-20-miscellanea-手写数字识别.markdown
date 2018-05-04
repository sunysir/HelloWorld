---
layout:     post
title:      "KNN手写数字识别"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-20 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---

#### 通过训练数据验证预测是实际相差百分比


pytho代码


				
				from sklearn.neighbors import KNeighborsClassifier
				from matplotlib import pyplot as plt
				from matplotlib.colors import ListedColormap
				import numpy as np
				x = [];x_test = []
				y = [];y_true = []
				#导入测试数据和验证数据
				for j in range(10):
				    for i in range(1,501):
				        img_data = plt.imread("C:/Users/suny/Desktop/exercise/data/"+str(j)+"/"+str(j)+"_"+str(i)+".bmp")
				        if i<400:
				            x.append(img_data.ravel())
				            y.append(j)
				        else:
				            x_test.append(img_data.ravel())
				            y_true.append(j)
				x_train = np.array(x)
				y_train = np.array(y)
				x_test = np.array(x_test)
				y_true = np.array(y_true)
				knffc = KNeighborsClassifier(n_neighbors=5)
				knffc.fit(x_train,y_train)
				y_ = knffc.predict(x_test)
				print((y_==y_true).sum()/y_true.size)
					
				#准确度在92%
				ou:0.9227722772277228		


#### 预测年收入大于50


			

			from sklearn.neighbors import KNeighborsClassifier
			from matplotlib import pyplot as plt
			from matplotlib.colors import ListedColormap
			import numpy as np
			import pandas as pd
			data = pd.read_csv(r"C:\Users\suny\Desktop\data\adults.txt")
			education = data["education"].unique();occupation = data["occupation"].unique()
			#将职位等字符串通过hash变成唯一数字
			for i,letter in enumerate(education):
			    value = sum([ord(k) for k in letter]) / 137
			    data = data.replace(to_replace=letter,value=value)
			for j,letter in enumerate(occupation):
			    value = sum([ord(k) for k in letter]) / 137
			    data = data.replace(to_replace=letter, value=value)
			x = [];x_test = []
			y = [];y_true = []
			for i in range(len(data)):
			    if i < 25000:
			        x.append([data.loc[i,"age"],data.loc[i,"education"],data.loc[i,"occupation"],data.loc[i,"hours_per_week"]])
			        y.append(data.loc[i,"salary"])
			    else:
			        x_test.append([data.loc[i,"age"],data.loc[i,"education"],data.loc[i,"occupation"],data.loc[i,"hours_per_week"]])
			        y_true.append(data.loc[i,"salary"])
			x_train = np.array(x);y_train = np.array(y);y_true = np.array(y_true);x_test = np.array(x_test)
			knffc = KNeighborsClassifier(n_neighbors=15)
			knffc.fit(x_train,y_train)
			y_ = knffc.predict(x_test)
			print((y_==y_true).sum()/y_true.size)

			#训练准确度在77%左右，由于数据特征采样较少
			ou:0.7760878190715513

