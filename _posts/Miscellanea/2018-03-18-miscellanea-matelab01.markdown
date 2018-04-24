---
layout:     post
title:      "Matelab面向对象学习笔记"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-01-04 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---

>**类定义  classdef  end**

>**属性定义 properties  end**

>**依赖属性定义  properties(dependent)   end**

>**隐藏属性  properties(Hidden)  ---> properties(Hidden=true)   end**

>**方法定义  methods  end**

整体结构框架 （文件名必须与类名相同）

	classdef A < handle
    properties
        a
        b
    end
    properties(Dependent)
       c
    end
    methods
        function obj = day01(a, b)
            obj.a = a
            obj.b = b
        end
        function c = get.c(obj)
            c = sqrt(a+b)
        end  

---

>**由于matelab是弱类型解释性语言，不能通过参数数目不同自动选择调用哪个函数，因此要自己去手动判断**

代码段  **nargin**

	 function obj = day01(age, name)
            if nargin == 0
                obj.age = 100
                obj.name = 'suny2'
            elseif nargin == 2
                obj.age = age
                obj.name = name
            end
        end

继承 classdef A < B

A继承B

代码段

	classdef day01_sub < day01
	    properties
	        gender
	    end
	    methods
	        function obj = day01_sub(age,name,gender)
	            obj = obj@day01   --->继承day01的前两个属性
	            obj.gender = gender
	        end
	    end
	end

---


	