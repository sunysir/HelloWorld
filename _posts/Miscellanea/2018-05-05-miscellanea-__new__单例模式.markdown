---
layout:     post
title:      "__new__实现单例"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-05-05 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---

			class A:
			    _flag = None
			    #cls可以随便取 代表 class类本身
			    def __new__(cls,name):
			        if not cls._flag:
			            #__new__方法创建实例
			            cls._flag = object.__new__(cls)
			        #返回标记，这样每次创建对象仅实例化第一次，之后一直调用标记中存储的那个第一次创建的实例
			        return cls._flag
			    def __init__(self,name):
			        self.name = name
			        print("我是{0}".format(name))
			
			a = A("suny")
			b = A("suny1")
			print(a == b)

			in：a = A("suny")
				b = A("suny1")
				print(a == b)

			ou：我是suny
				我是suny1
				True