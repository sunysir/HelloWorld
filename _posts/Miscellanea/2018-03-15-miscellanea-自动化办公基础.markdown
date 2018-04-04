---
layout:     post
title:      "py自动化办公基础"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-01-03 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 生活
---




## 通过pywin32实现word的自动化办公

- **打开并读写word**
	
	python 代码
			
		#请求调用word终端服务程序		
		word = win32com.client.Dispatch("word.Application")
		#通过word终端打开word文本
		doc = word.Documents.Open("path")
		#遍历word文件中的段落并打印	
		for paragraph doc.Paragraphs:
			line = paragraph.Range.Text
			print(line)
		#关闭word终端，和文本文档
		doc.Close()
		word.Quit()
- **word转换其他格式文件**
	
	命令代码
		
		wdFormatDocument = 0 
		wdFormatDocument97 = 0 
		wdFormatDocumentDefault = 16 
		wdFormatDOSText = 4 
		wdFormatDOSTextLineBreaks = 5 
		wdFormatEncodedText = 7 
		wdFormatFilteredHTML = 10 
		wdFormatFlatXML = 19 
		wdFormatFlatXMLMacroEnabled = 20 
		wdFormatFlatXMLTemplate = 21 
		wdFormatFlatXMLTemplateMacroEnabled = 22 
		wdFormatHTML = 8 
		wdFormatPDF = 17 
		wdFormatRTF = 6 
		wdFormatTemplate = 1 
		wdFormatTemplate97 = 1 
		wdFormatText = 2 
		wdFormatTextLineBreaks = 3 
		wdFormatUnicodeText = 7 
		wdFormatWebArchive = 9 
		wdFormatXML = 11 
		wdFormatXMLDocument = 12 
		wdFormatXMLDocumentMacroEnabled = 13 
		wdFormatXMLTemplate = 14 
		wdFormatXMLTemplateMacroEnabled = 15 
		wdFormatXPS = 18	

---

	
python实现功能代码		
			
	import win32com
	import win32com.client
	word = win32com.client.Dispatch("word.Application")
	doc = word.Documents.Open(path)
	doc.SaveAs(path, 17)
	doc.Close()
	word.Quit()	



---

- **创建word并写入内容**

	python代码
		
		import win32com
		import win32com.client
		#打开客户端
		word = win32com.client.Dispatch("word.Application")
		#显示客户端
		word.Visible = True
		#创建空文本
		doc = word.Documents.Add()
		#定位光标并填写内容
		r = doc.Range(0,0)
		r.InsertAfter("你一个好人\n")
		r.InsertAfter("但是我们不合适\n")
		doc.SaveAs("C:/Users/suny/Desktop/GoodManCard.doc")
		doc.Close()
		word.Quit()

---

- **读取xlsx文件**

所需方法
		
	excel = load_workbook(filename=path)# 打开文件
	excel.get_sheet_names()# 获得所有sheet
	sheet = excel.get_sheet_by_name(sheets[0])# 获得其中一个sheet
	sheet.max_row# sheet中的行
	sheet.max_column# sheet中的列
	sheet.cell(row = rowNum,column = columnNum).value# 定位单元格.value的值
	

	

python代码

	# 导入模块
	from openpyxl.reader.excel import load_workbook
	
	def readXlsxExcel(path):
	#   读取excel文件
	    excel = load_workbook(filename=path)
	#   获取所有的表
	    sheets = excel.get_sheet_names()
	#   根据表名,获取其中的一个表
	    sheet = excel.get_sheet_by_name(sheets[0])
	#   获取最大行数
	#     print(sheet.max_row)
	#   获取最大列数
	#     print(sheet.max_column)
	    sheetData = []
	    for rowNum in range(1,sheet.max_row+1):#遍历行
	        lineData = []
	#   遍历列
	        for columnNum in range(1,sheet.max_column+1):
	#   获取对应行中对应列的数据
	#             value = sheet.cell(row = rowNum,column = columnNum)
	            value = sheet.cell(row = rowNum,column = columnNum).value
	            # print(value)
	            lineData.append(value)
	        # print(lineData)
	        sheetData.append(lineData)
	
	    return  sheetData
	
	path = r"C:\Users\suny\Desktop\test.xlsx"
	#readXlsxExcel(path)
	print(readXlsxExcel(path))
	
---

**读取xls和xlsx文件

首先安装相关依赖包 
	
	pip install pyexcel
	pip install pyexecl-xls
	pip install pyexecl-xlsx
	pip install pyexecl-xlsxw

python代码

	# 导入有序字典
	from collections import OrderedDict
	from pyexcel_xls import get_data
	
	def readXlsxAndXlsData(path):
	    # 创建一个有序字典
	    dic = OrderedDict()
	    # 读excel文件
	    data = get_data(path)
	    for sheetName in data:
	        # 将数据取出来放到有序字典中
	        dic[sheetName] = data[sheetName]
	    return dic
	
	path = r"H:\01python个人备课\day16\test.xls"
	# readXlsxExcel(path)
	print(readXlsxAndXlsData(path))


