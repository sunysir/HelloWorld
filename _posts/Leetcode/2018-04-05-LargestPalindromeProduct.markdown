---
layout:     post
title:      "两个N位数乘积的最大回文数"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-05 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/LargestPalindromeProduct.jpg"/>

python代码
第一时间想到的暴力解法 （ <font color = "red">Time Limit Exceeded</font>）

	class Solution:
    def largestPalindrome(self, n):
        palindrome = 0
        if n != 1:
            max_bit = 2*n
			#for循环生成回文数
            for i in range(pow(10,n-1),10**n)[::-1]:
                a = str(i)[::-1]
                palindrome = int(str(i) + "".join(a))
				#对每个回文数从10^(n)-1开始除进行判断，能整除则返回
                for i in range(pow(10,n-1),pow(10,n))[::-1]:
                    if palindrome/i > pow(10,n) :
                        break
                    if palindrome%i == 0:
                          mod = palindrome % 1337   
                          return mod
        else:
            return 9            
            
国外牛人写的效率超高的算法

注解：
	
 P = A x B --->P为回文数可以分解为**hix(10^n)+low** 其中low为hi的翻转， 要它为最大必须让A和B都尽量的大 A和B为10^n  n位给定的位数
 A = (10^n-i) ; B = (10^n-j)
 P = (10^n-i)x(10^n-j)
 P = 10^nx(10^n-i-j)+ij   令 a = i+j 
 P = 10^nx**(10^n-a)**+**ij** =(10^n)x**hi**+**low**
 --> hi = (10^n-a) low = ij = i(a-i) = ia-i^2
 --> i^2 - ia + low = 0
 --> (i-a/2)^2 = a^2/4-low  (a = i+j)
 -->  i-j = a^2-low^.5
 -->  因为i和j都为整数，所以i-j必为整数，所以 a^2-low^.5必为整数 当它第一次出现整数的时候比为最大回文数
完毕！鼓掌！！！

	class Solution(object):
    def largestPalindrome(self, n):
        if n==1: return 9
        for a in range(2, 9*10**(n-1)):
            hi=(10**n)-a
            lo=int(str(hi)[::-1])
            if a**2-4*lo < 0: continue
            if (a**2-4*lo)**.5 == int((a**2-4*lo)**.5):
                return (lo+10**n*(10**n-a))%1337
            
	s = Solution()
	max = s.largestPalindrome(2)
	print(max)

	            
        
	
	


