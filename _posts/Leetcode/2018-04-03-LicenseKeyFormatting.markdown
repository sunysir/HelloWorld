---
layout:     post
title:      "密匙重新排列"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-01 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/LicenseKeyFormatting.jpg"/>

**考察字符串大小写转换，字符串分割，字符串数组互相转换**
- **print(str.upper())          # 把所有字符中的小写字母转换成大写字母**
- **print(str.lower())          # 把所有字符中的大写字母转换成小写字母**
- **print(str.capitalize())     # 把第一个字母转化为大写字母，其余小写**
- **print(str.title())          # 把每个单词的第一个字母转化为大写，其余小写 **

python代码

	import re
	class Solution:
	    def licenseKeyFormatting(self, S, K):
	        str1 = "".join(re.split('-',S)).upper()
	        str1 = list(str1)
	        if len(str1)%K == 0:
	            num = len(str1)//K - 1
	        else:
	            num = len(str1)//K
	        ran = len(str1)
	        for i in range(num):
	            ran = ran - K
	            str1.insert(ran, "-")
	        str1 = "".join(str1)
	        return str1
	
	str1 = "2-5g-3-J"
	K = 2
	s = Solution()
	str1 = s.licenseKeyFormatting(str1, K)
	print(str1)            
            
	            
        
	
	


