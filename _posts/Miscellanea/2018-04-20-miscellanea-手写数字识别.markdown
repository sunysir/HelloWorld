---
layout:     post
title:      "手写数字识别"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-19 11:00:00
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


[data](file:///img/data")




