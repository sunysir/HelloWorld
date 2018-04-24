---
layout:     post
title:      "十转二翻转在转十进制"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-05 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/MaxConsecutiveOnes.jpg"/>

python代码
	
    class Solution:
    def findComplement(self, num):
        temp = num;list1 = [];str1 = "";n = 0;res = 0
        #十进制转二进制
		while num > 0:
            temp = num%2
            num = num//2
            #转成二进制然后翻转
			if temp == 1:
                temp = '0'
            else:
                temp = '1'
            str1 = str1+temp
        #二进制转十进制
		for i in str1:
            res += int(i)*(2**n)
            n+=1       
        return res
	            
	s = Solution()
	num = s.findComplement(1)
	print(num)

	
	


