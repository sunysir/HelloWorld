---
layout:     post
title:      "KNN人体动作识别"
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
				x_train = np.load(r"C:\Users\suny\Desktop\target\x_train.npy")
				y_train = np.load(r"C:\Users\suny\Desktop\target\y_train.npy")
				x_test = np.load(r"C:\Users\suny\Desktop\target\x_test.npy")
				y_test = np.load(r"C:\Users\suny\Desktop\target\y_test.npy")
				#创建KNN模型
				knfc = KNeighborsClassifier(n_neighbors=5)
				#进行训练
				knfc.fit(x_train,y_train)
				#数据进行预测
				y_ = knfc.predict(x_test)
				#求出真实度百分比
				# real_percent = (y_ == y_test).sum()/y_test.size
				# print(real_percent)
				max = 0;color = ["red","blue","orange","green","yellow","purple"]
				#绘制6种动作的波形图
				for j in range(1,7):
				    for i in x_test[np.where(y_ == j)]:
				        max += i
				    #取均值降维
				    x_ravel = max/len(x_test[np.where(y_ == j)])
				    x_plot = np.arange(1,562,1)
				    y_plot = x_ravel
				    #每种图形设置不同颜色
				    plt.plot(x_plot,y_plot,color= color[j-1])
				    plt.show()

<img src="/img/body.jpg">




