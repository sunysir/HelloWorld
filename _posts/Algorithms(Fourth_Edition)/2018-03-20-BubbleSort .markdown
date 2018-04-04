---
layout:     post
title:      "冒泡排序"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-03-20 19:00:00
author:     "suny"
catalog: false
categories: Algorithms
tags:
    - 笔记
---
# 冒泡排序
> **顾名思义，冒泡排序就是第一个数和第二个数比，比第二个数大则交换，然后，第二个数和第三个数比，以此类推，直接最后一个数比较完为止。废话连篇（No picture say JB），上图。**

<img src="/img/BubbleSort.jpg"/>


从图中可以看出该算法最大时间复杂度为O（n^2）

python代码 
	
	a = [10,1,6,8,2,4,3,24,12,9]
	def change(arr,i , j):
	    temp = arr[i]
	    arr[i] = arr[j]
	    arr[j] = temp
	def BubbleSort(arr):
	    for i in range(len(a)-1):
	        for j in range(len(a)-i-1):
	            if a[j] > a[j+1]:
	                change(a, j, j+1)
	BubbleSort(a)           
	print(a)
	

