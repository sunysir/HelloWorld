---
layout:     post
title:      "重建二叉树"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-21 19:00:00
author:     "suny"
catalog: false
categories: Algorithms
tags:
    - 笔记
---

**递归方法，局部到整体，每个子节点当做整体分别判断左右两边的数组，根据中序遍历结果找到左右两边的子节点，再通过前序找到每个子节点的根节点。**

python测试代码

				# -*- coding:utf-8 -*-
				class TreeNode:
				    def __init__(self, x):
				        self.val = x
				        self.left = None
				        self.right = None
				class Solution:
				    # 返回构造的TreeNode根节点
				    def reConstructBinaryTree(self, pre, tin):
				        # write code here
				        def recreate(pre,tin):
				            #长度为0结束递归
				            if len(pre) != 0:
				                root = TreeNode(pre[0])
				            else:
				                return
				            if root != None:
				                #中序遍历位置标记创建
				                flag = 0
				                #找到中序遍历的标记位置
				                for i in tin:
				                    if i == root.val:
				                        flag = tin.index(i)
				                #分为左右两部分进入子函数继续递归
				                root.left = recreate(pre[1:flag+1],tin[:flag])
				                root.right = recreate(pre[flag+1:],tin[flag+1:])
				                return root
				        return recreate(pre,tin)
				    #前序遍历测试函数
				    def printf(self,root):
				        list1 = []
				        list1.append(root.val)
				        print(root.val)
				        if  root.left !=None:
				            self.printf(root.left)
				        if root.right != None:
				            self.printf(root.right)
				pre = [1,2,4,7,3,5,6,8]
				tin = [4,7,2,1,5,3,8,6]
				root = None
				s = Solution()
				root = s.reConstructBinaryTree(pre,tin)
				s.printf(root)
