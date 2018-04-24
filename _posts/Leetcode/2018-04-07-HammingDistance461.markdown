---
layout:     post
title:      "461.HammingDistance"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-07 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/HammingDistance.jpg"/>

> **两个整数之间的汉明距离指的是这两个数字对应二进制位不同的位置的数目。**

给出两个整数 x 和 y，计算它们之间的汉明距离

python代码（弱智一样的写法）
	
    class Solution:
	    def hammingDistance(self, x, y):
	        count = 0
			#十进制转二进制
	        def tenTobin(x):
	            temp1 = x;list1 = [];
	            while temp1>0:
	                temp = temp1%2
	                temp1 = temp1//2
	                list1.insert(0, temp)
	            return list1
	        x = tenTobin(x)
	        y = tenTobin(y)
			#高位补零
	        if len(x) > len(y):
	            num = len(x)-len(y)
	            for i in range(num):
	                y.insert(0,0)
	        else:
	            num = len(y)-len(x)
	            for i in range(num):
	                x.insert(0,0)
	        for (i,j) in zip(x,y):
	            if i != j:
	                count+=1
	        return count

正常人的写法

	class Solution:
	    def hammingDistance(self, x, y):
	        """
	        :type x: int
	        :type y: int
	        :rtype: int
	        """
	        return bin(x^y).count('1')
	        
	                   

        
	s = Solution()
	a = s.hammingDistance(1,5)
	print(a)

	
	


