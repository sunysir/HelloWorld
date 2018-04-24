---
layout:     post
title:      "金牌银牌铜牌"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-02 13:00:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---

<img src="/img/RelativeRanks.jpg"/>

- 最开始的暴力解法<font color = "red">(Time Limit Exceeded)</font>

python代码 时间复杂度O(n^2)

	class Solution:
    def findRelativeRanks(self, nums):
         if len(nums) >= 10000:
              return
         pos = 0; list1 = [];list2 = ["Gold Medal", "Silver Medal", "Bronze Medal"]
         count = 0
         for j in range(len(nums)):
              max = 0;
              for i in range(len(nums)):
                  if type(nums[i]) != int:
                       continue
                  if max <= nums[i]:
                       max = nums[i]
                       pos = i
              list1.append(pos)
              nums[pos] = -1
              if j <= 2:
                   nums[list1[j]] = str(list2[j])
              else:
                   nums[list1[j]] = str(j+1)        
         return nums
        
	
	nums = [1,2,3,4,5]
	s = Solution()
	res = s.findRelativeRanks(nums)
	print(res)


通过枚举enumerate和map函数优化 时间复杂度O(n)

python代码


	class Solution:
    def findRelativeRanks(self, nums):
		#枚举倒序排序的nums列表遍历返回的迭代器转换成字典 {num值，枚举数字+1} 得出最大值：1 第二大：2....
         pos = {n:i+1 for i,n in enumerate(sorted(nums, reverse = True))}
         def func(x):
              if pos[x] == 1:
                   return "Gold Medal"
              elif pos[x] == 2:
                   return "Silver Medal"
              elif pos[x] == 3:
                   return "Bronze Medal"
              else:
                   return pos[x]
		#map函数将列表中值依次在函数func中运行返回新结果列表
         return list(map(func, nums))
               
        

	nums = [1,2,3,4,5]
	s = Solution()
	res = s.findRelativeRanks(nums)
	print(res)
	


