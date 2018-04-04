---
layout:     post
title:      "win32com安装以及配置"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-01-03 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 生活
---




**https://sourceforge.net/projects/pywin32/files/pywin32/**

找下载量最高的 资源相对较好

没找到路径说明下载的版本不对，重下

安装完成之后


- 将python安装目录下的Lib\site-packages添加到PYTHONPATH环境变量 

- 将python安装目录Lib\site-packages\pywin32_system32下的文件拷贝到系统system32目录下，这样就可以解决导入pywin32模块时报找不到模块问题
- 安装成功cmd中可以运行pywin32，但是pycharm中还是无法识别解决办法**https://www.cnblogs.com/hackpig/p/8186214.html**
	


