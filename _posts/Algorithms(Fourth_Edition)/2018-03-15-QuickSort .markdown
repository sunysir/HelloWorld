w---
layout:     post
title:      "快速排序"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-03-15 20:16:00
author:     "suny"
catalog: true
categories: Algorithms
tags:
    - 笔记
---
# 快速排序

> **快速排序，是对冒泡排序的一种改进。是通过一次排序将数组分为两部分，两部分内部数无序，但两部分的前部分不后部分内部所有的数都小，接着在将两部分的无序数在进行二分割，知道最后为一个数为止。**

**上图。。。**

<img src="/img/QuickSort.jpg"/>

python代码

	class Q_sort(object): 

	   def quick_sort(self, low, high, arr):
	       if low >= high:
	           return
	       low = self.sort(low, high, arr)
	       self.quick_sort(0, low-1, arr)
	       self.quick_sort(low+1, high, arr)
	
	       
	       
	   def change(self, a, b, arr):
	       temp = arr[a]
	       arr[a] = arr[b]
	       arr[b] = temp
	
	
	   def sort(self, low, high, arr):
	       base = arr[low]
	       while low < high:
		   while low < high and base < arr[high]:
		       hi -= 1
		   arr[lo] = arr[high]
		   while low < high and base > arr[low]:
		       low += 1
		   arr[high] = arr[low]
	       arr[low] = base
	       return low

      
	list1 = [98,2,5,24,12,85,56,47,13,1]               
	q = Q_sort()
	q.quick_sort(0, len(list1)-1, list1)
	print(list1)



