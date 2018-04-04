---
layout:     post
title:      "键盘匹配"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-01 11:00:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
正则表达式秒解决
<img src="/img/KeyboardRow.jpg"/>

python代码

	import re
	class Solution:
	    def findWords(self, words):
	        list1 = []
	        rep = r"[qwertyuiop]+|[asdfghjkl]+|[zxcvbnm]+"
	        def input_1(words):
	            for i in words:
	                res = re.match(rep, i, re.I)
	                if res.span()[1] == len(i):
	                    list1.append(i)
	            return list1
	        list1 = input_1(words)
	        return list1
	words = ["Hello", "Alaska", "Dad", "Peace"]
	s = Solution()
	list1 = s.findWords(words)
	print(list1)
	            
        
	
	


