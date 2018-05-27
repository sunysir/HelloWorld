---
layout:     post
title:      "装饰器实现单例"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-05-05 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---


首先看看闭包



> **闭包(closure)是函数式编程的重要的语法结构。函数式编程是一种编程范式 (而面向过程编程和面向对象编程也都是编程范式)。在面向过程编程中，我们见到过函数(function)；在面向对象编程中，我们见过对象(object)。函数和对象的根本目的是以某种逻辑方式组织代码，并提高代码的可重复使用性(reusability)。闭包也是一种组织代码的结构，它同样提高了代码的可重复使用性**

闭包就是函数内部的函数可以使用外部函数的变量但是不可以修改，然后返回内部函数为最终结果



		def A(a):
		    def B(x):
		        c = a**2+x
		        return c
		    return B
		
		
		in: a = A(1)(3)
			print(a)
		ou: 4




同样闭包可以传入变量和类




		def A(cls):
		    def B(name):
		        return cls(name)
		    return B
		class C():
		    def __init__(self, name):
		        print("{0}同学你好".format(name))
		
		
		a = A(C)("suny")
		print(a)

		suny同学你好
		<__main__.C object at 0x02CBF230>





接着实现装饰器（标准三层嵌套的装饰器）


			def log(text):
			    def decorator(func):
			        result = func(*args,**kwargs)
			        def wrapper(*args,**kwargs):
			            print("{1}同学，这是{0}的日志".format(func.__name__,"suny"))
			            return result
			        return wrapper
			    return decorator
			
			@log("suny")
			def A():
			    print("我是A")
			
			in：A()
				print(A)
			ou：suny同学，这是A的日志
				我是A
				<function log.<locals>.decorator.<locals>.wrapper at 0x02ED0348>	


通过输出结果可以看出装饰器已经装饰成功，但是原函数的内存信息及属性都已经变成了装饰器函数的内存信息，因此这种装饰器的设计并不完善

			from functools import wraps
			def log(text):
			    def decorator(func):
			        result = func(*args,**kwargs)
			        def wrapper(*args,**kwargs):
			            print("{1}同学，这是{0}的日志".format(func.__name__,"suny"))
			            return result
			        return wrapper
			    return decorator
			
			@log("suny")
			def A():
			    print("我是A")
			
			in: A()
				print(A)
			ou: suny同学，这是A的日志
				我是A
				<function A at 0x02F10390>


导入from functools import wraps可以实现wrapper.\__name\__ == func.\__name\__等原函数的属性及内存地址存入装饰器函数中


装饰器实现单例模式（其实原理都是一样的，就是把第一次实例的对象放到标记位中，每次返回的都是那个标记中存储的第一次实例的对象）


		from functools import wraps
		def log(cls):
		        _instance = None
		        @wraps(cls)
		        def wrapper(*args,**kwargs):
		            if not _instance:
		                cls._instance = cls(*args,**kwargs)
		            return _instance
		        return wrapper
		
		@log
		class A():
		    def __init__(self,name):
		        print("我是{0}".format(name))
		
		in: a = A("suny")
			b = A("suny1")
			print(a is b)
		ou: 我是suny
			我是suny1
			True



