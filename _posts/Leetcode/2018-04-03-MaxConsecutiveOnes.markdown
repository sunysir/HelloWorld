---
layout:     post
title:      "数组中连续的1最大值"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-01 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/MaxConsecutiveOnes.jpg"/>

python代码

	class Solution:
    def findMaxConsecutiveOnes(self, nums):
        max = 0;count = 0
        for i in range(len(nums)):
            if nums[i] == 1:
                count+=1
                if max < count:
                    max = count
            else:
                count = 0                     
        return max
	nums = [0]
	s = Solution()
	max = s.findMaxConsecutiveOnes(nums)
	print(max)            
            
	            
        
	
	


