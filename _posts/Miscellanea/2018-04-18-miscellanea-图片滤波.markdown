---
layout:     post
title:      "图片滤波"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-18 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 笔记
---


- 滤掉低频波
> **利用PIL.Image对jpg格式图片进行滤波** 

			import numpy as np
			import matplotlib.pyplot as plt
			from numpy.fft import fft,ifft
			from PIL import ImageFilter
			from PIL import Image
			#导入图片
			img = Image.open(r"C:\Users\suny\Desktop\msx.jpg")
			#图片转换为npint8类型数据
			data = np.fromstring(img.tobytes(),dtype=np.int8)
			#傅里叶变换时域转换为频域
			fft_data = fft(data)
			#滤掉低频数据
			fft_data[np.where(np.abs(fft_data)<5e4)] = 0
			#频域转到时域
			ifft_data = ifft(fft_data)
			#去掉虚部
			data_real = np.real(ifft_data)
			#转为npint8数据类型
			data1 = np.int8(data_real)
			#转为图片格式
			img1 = Image.frombytes(mode=img.mode,size=img.size,data=data1)
			Image._show(img1)
			#图片->npint8->傅里叶转换->滤波->逆傅里叶变换->去掉虚部并转成npint8格式->转成图片并显示



	
<img src="/img/lvbo.jpg">

	
  


- 滤掉高频波


> **利用matplotlib.pyplot和numpy.fft.fft2,ifft2对png格式图片进行滤波**





			from PIL import Image
			import numpy as np
			from matplotlib import pyplot as plt
			from numpy.fft import fft,ifft
			#打开图片
			img_data = plt.imread(r"C:\Users\suny\Desktop\moonlanding.png")
			#傅里叶转换时域变频域
			fft_data = fft(img_data)
			#滤掉高频波
			for i in range(len(fft_data)):
			    fft_data[i][np.where(np.abs(np.array(fft_data[i]))>13)]=2
			#频域转为时域
			ifft_data = ifft(fft_data)
			#去掉虚部
			data_real = np.real(ifft_data)
			plt.imshow(data_real,cmap='gray')
			plt.show()


> **利用matplotlib.pyplot和scipy.packfft.fft2,ifft2对png格式图片进行滤波**


			

			from PIL import Image
			import numpy as np
			from matplotlib import pyplot as plt
			from scipy.fftpack import fft2,ifft2
			#打开图片
			img_data = plt.imread(r"C:\Users\suny\Desktop\moonlanding.png")
			#傅里叶转换时域变频域
			fft_data = fft2(img_data)
			#滤掉高频波
			fft_data[(np.abs(fft_data)>1e3)] = 100
			#频域转为时域并去掉虚部
			data = np.real(ifft2(fft_data))
			plt.imshow(data,cmap="gray")
			plt.show()



<img src="/img/quzao.jpg">