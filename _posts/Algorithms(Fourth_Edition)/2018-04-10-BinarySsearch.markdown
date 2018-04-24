---
layout:     post
title:      "二分法查找"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-10 19:00:00
author:     "suny"
catalog: false
categories: Algorithms
tags:
    - 笔记
---

**二分法查找是最简单的查找方法之一，前提是数组必须是有序数组，每次去数组中间位置的值，比目标值大就对前半部分去中间位置值，反之对后半部分做同样操作，知道找到为止。**

python测试代码

	a = [1,4,7,13,45,56,78,89,101,202]
	def binary_search(arr, num):
	        max = len(arr);min = 0;
	        while True:
	            mid = (max+min)//2
	            if arr[mid] > num:
	                max = mid
	            elif arr[mid] < num:
	                min = mid
	            else:
	                return mid+1
	
	mid = binary_search(a, 101)    
	print(mid)

