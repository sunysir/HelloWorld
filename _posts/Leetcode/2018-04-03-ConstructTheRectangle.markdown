---
layout:     post
title:      "最小长宽比"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-01 11:00:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---

<img src="/img/ConstructtheRectangle.jpg"/>

python代码

	import math
	class Solution:
	    def constructRectangle(self, area):
	        list1 = []
	        def fuc(area):
	            mid = int(math.sqrt(area))
	            while mid >= 1:
	                if mid == 1:
	                    list1.append(int(area/mid))
	                    list1.append(int(mid))
	                else:
	                    if area%mid == 0:
	                        list1.append(int(area/mid))
	                        list1.append(int(mid))
	                        mid = 0
	                mid-=1
	        fuc(area)
	        return list1
	
	s = Solution()
	res = s.constructRectangle(3)
	print(res)

优化后

	import math
	class Solution:
	    def constructRectangle(self, area):
	        mid = int(math.sqrt(area))
	        while True:
	            if area%mid == 0:
	                return [int(area/mid), int(mid)]
	            mid-=1
	
	s = Solution()
	res = s.constructRectangle(6)
	print(res)
		            
        
	
	


