---
layout:     post
title:      "485. Max Consecutive Ones"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-03 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/MaxConsecutiveOnes.jpg"/>

思路1：传统遍历

python代码

	class Solution:
    def findMaxConsecutiveOnes(self, nums):
        max = 0;count = 0
        for i in range(len(nums)):
			#判断连续的1最大数量并记录为max
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


思路2： 利用正则表达式，充分利用python现成函数（108ms）  1行搞定so easy

          
import re
class Solution:
    def findMaxConsecutiveOnes(self, nums):
        return max([len(num) for num in re.split(r"0+","".join(list(map(str, nums))))])
        
s = Solution()
num = s.findMaxConsecutiveOnes([1,1,0,1,1,1])
print(num)
           
	            
        
	
	


