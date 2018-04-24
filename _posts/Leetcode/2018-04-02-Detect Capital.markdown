---
layout:     post
title:      "单词检查"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-02 11:00:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
使用正则表达式分分钟解决
<img src="/img/DetectCapital.jpg"/>

python代码

	import re
	class Solution:
	    def detectCapitalUse(self, word):
	         rule = r"[a-z]+|[A-Z][a-z]+|[a-z]+|[A-Z]+"
	         if re.match(rule, word).span() == (0, len(word)):
	              return True
	         else:
	               return False
	word = "USA"
	s = Solution()
	res = s.detectCapitalUse(word)
	print(res)

	
	


