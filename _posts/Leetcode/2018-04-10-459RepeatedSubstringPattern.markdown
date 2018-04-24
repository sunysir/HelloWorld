---
layout:     post
title:      "459.RepeatedSubstringPattern"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-10 14:12:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/RepeatedSubstringPattern.jpg"/>

思路1: 整个字符串的一半开始查找，找到子字符串在判断乘以之前的余数，看能否等于整字符串

python代码
	
	class Solution:
    def repeatedSubstringPattern(self, s):
		#从字符串的一半长度开始遍历，到长度为1为止
        for i in range((len(s)//2)+1)[:0:-1]:
			#子长度能否被整除
            if len(s)%i == 0:
                j = 0;k = i;count = 0;word = ""
				#字符串的开头和整除的数的开头开始匹配，成功则存储子字符串word，失败退出
                while j < i and k < len(s):
                    if s[j] == s[k]:
                        word+=s[j]
                        count+=1
                        j+=1
                        k+=1
                    else:
                        break
				#判断匹配的字符串长度是否和子符串长度一致
                if count == i:
					#若长度一致，则判断子字符串乘倍数是否等于整字符串
                    if word*(len(s)//i) == s:
                        return True
        return False
        
	s = Solution()
	res = s.repeatedSubstringPattern("aaaaa")
	print(res)  

思路2：字符串分成多个方块n **(n>=2)**，如果子字符串的倍数能组成整字符串，那整字符串的开头和结尾总能找到一个子字符串，因为将字符串乘以2，在去掉开头和结尾的一个字符，破坏掉开头和结尾的子字符串，看字符串里是否能找到整字符串。


	
	class Solution:
	    def repeatedSubstringPattern(self, s):
	        str1 = (s*2)[1:-1]
	        return str1.find(s) != -1
	        
	        
	s = Solution()
	res = s.repeatedSubstringPattern("aaaaa")
	print(res) 



	
	


