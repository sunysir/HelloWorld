---
layout:     post
title:      "找出二叉树中重复元素最多的节点值"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-01 11:00:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/FindModeinBinarySearchTree.jpg"/>

> **from collections import Counter模块**

python代码

	#Definition for a binary tree node.
	from collections import Counter 
	class TreeNode:
	    def __init__(self, x):
	         self.val = x
	         self.left = None
	         self.right = None
	
	class Solution:
	    def findMode(self, root):
	        count = 1
	        flag = 0
	        if root != None:
	            list1 = []
	            list2 = []
	            #前序遍历数组
	            def preoder(root):
	                list1.append(root.val)
	                if root.left != None:
	                    preoder(root.left)
	                if root.right != None:
	                    preoder(root.right)
	            preoder(root)
	            #Counter函数找出数组每个元素重复个数
	            list1 = (Counter(list1).most_common())
	            #筛选出列表中与最大重复个数相同的个数
	            for i in range(1, len(list1)):
	                if list1[0][1] == list1[i][1]:
	                    count+=1
	            #把重复数量最大的元素分别存到列表2中，并返回列表2
	            if count > 0:
	                while count:
	                    list2.append(list1[flag][0])
	                    count-=1
	                    flag+=1
	            return list2
	        else:
	            return []
	        
	root = TreeNode("");#root.right = TreeNode(2) ;root.right.left = TreeNode(3)             
	s = Solution()
	max = s.findMode(root)
	print(max)
	
	


