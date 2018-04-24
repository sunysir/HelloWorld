---
layout:     post
title:      "多线程多进程"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-09 11:00:00
author:     "suny"
catalog: true
categories: Miscellanea
tags:
    - 生活
---

<img src="/img/IDLE.jpg"/>

IDLE无法实现多进程，用cmd或者pycharm可以解决

#### 多线程与多进程概述
	
> **进程与进程之间是相互独立的，都会对全局上下文进行一次备份，互不影响，进程之中包含线程，一个线程之中的多个线程共享一个进程的数据，最初，CPU单线程，每运行一个程序，就必须要运行完才能进行下一个，后来进化之后，CPU同时处理多个程序，每个给一定时间，由于CPU处理速度非常快，使得人们根本察觉不到，好像是在同时运行，实则是有微妙级的延迟，再后来就出现了多线程，CPU可以并行处理多个程序，因此线程越多，就使得计算机在处理多任务时候约流畅，排除其他硬件因素。**




python测试代码

	import multiprocessing
	import os
	import time
	
	def run(name):
	    for i in range(100):
	        print("%s正在数数%s"%(name, i))
	        time.sleep(1)
	if __name__ == "__main__":
	    print("%d主进程开启"%os.getpid())
	    #创建一个子进程
	    p = multiprocessing.Process(target=run,args=('小明',))
	    p.start()
	    #当子进程执行结束后才会执行join后面的方法
	    p.join()
	    for i in range(100):
	        print("我正在数数%s"%i)
	        time.sleep(2)
	    print("主进程结束")

下面代码演示多线程直接数据不共享

	import multiprocessing
	import os
	import time
	num = 100
	def run(name):
	    global num
	    for i in range(100):
	        num+=1
	        print("%s正在数数%s"%(name, num))
	        time.sleep(1)
	if __name__ == "__main__":
	    print("%d主进程开启"%os.getpid())
	    #创建一个子进程
	    p = multiprocessing.Process(target=run,args=('小明',))
	    p.start()
	    #当子进程执行结束后才会执行join后面的方法
	    for i in range(100):
	        num+=1
	        print("我正在数数%s"%num)
	        time.sleep(1)
	    print("主进程结束")

		>>> 我正在数数101
			小明正在数数101
			我正在数数102
			小明正在数数102
			我正在数数103
			小明正在数数103
			我正在数数104
			小明正在数数104
			我正在数数105
			小明正在数数105
			我正在数数106
			小明正在数数106

可以看出主进程改变全局变量num和子进程调用全局变量完全独立互不干扰

**原因:在创建子进程时是对全局变量进行一个备份，因此父进程中的变量num和子进程中num根本就不是一个变量**

---

#### 进程池

> **预先创建好的空闲进程，管理进程会把工作分发到空闲进程来处理。管理进程负责创建资源进程，把工作交给空闲资源进程处理，回收已经处理完工作的资源进程。**


	import multiprocessing
	import os
	import time
	num = 100
	def run(name):
	    global num
	    for i in range(15):
	        num+=1
	        print("%s正在数数%s"%(name, num))
	if __name__ == "__main__":
	    print("%d主进程开启"%os.getpid())
	    #创建一个子进程
	    # p = multiprocessing.Process(target=run,args=('小明',))
	    # p.start()
	    pp = multiprocessing.Pool(2)
	
	    for i in range(6):
			#从进程池中取一个空闲进程，没有就等待忙碌状态的进程空闲
	        pp.apply_async(run, args=(str(i),))
	    pp.close()
		#当子进程执行结束后才会执行join后面的方法
	    pp.join()
	    for i in range(10):
	        num+=1
	        print("我正在数数%s"%num)
	    print("主进程结束")


#### 多线程

线程是进程的一个分支，每个进程至少有一个线程，一个进程的多个线程共享进程的所有上下文（资源），因此，不加线程锁的情况下很容易出现数据错乱


发生错乱的例子

	import threading
	import os
	import time
	num = 100
	def run(n):
	    global num
	    while num>0:
	        time.sleep(0.005)
	        num-=1
	        print("%s出票，剩余票数%d" % (threading.current_thread().name, num))
	if __name__ == "__main__":
	    print("%s主线程程开启"%(threading.current_thread().name))
	    #创建一个子进程
	    tt1 = threading.Thread(target=run, name="窗口1", args=(1,))
	    tt2 = threading.Thread(target=run, name="窗口2", args=(1,))
	    tt1.start()
	    tt2.start()
	    tt1.join()
	    tt2.join()
	    print("剩余票数%d"%num)
	    print("主进程结束")

		>>> 窗口1出票，剩余票数1
			窗口2出票，剩余票数0
			窗口1出票，剩余票数-1
			剩余票数-1
			主进程结束

**出现了-1这个票数，是因为当票数还剩1张的时候线程1还没运行到num-=1，这个时候CPU去临幸线程2了，因此线程2把剩余的1张票抢走了，在当CPU处理线程1的时候票已经没有了，因此出现了票为负数的情况**

---

#### 线程锁

**前面说了多线程会出现数据错乱的问题，怎么解决呢，加线程锁就可以了，线程锁阻止了多线程的并发执行，代码一旦加锁就只能以单线程的方式去执行，因此效率大大降低。**

- **lock = threading.Lock()**  **#创建一个线程锁**
- **lock.acquire()** **#上锁**
- **lock.release()** **#解锁**

python测试代码


	import threading
	import os
	import time
	num = 100
	def run(n):
	    global num
	    while True:
	        try:
				#上锁
	            lock.acquire()
	            if num > 0:
	                time.sleep(0.005)
	                num-=1
	                print("%s出票，剩余票数%d" % (threading.current_thread().name, num))
	            else:
	                break
	        finally:
	            #解锁
				lock.release()
	if __name__ == "__main__":
	    print("%s主线程程开启"%(threading.current_thread().name))
	    #创建一个线程锁
	    lock = threading.Lock()
	    #创建一个子进程
	    tt1 = threading.Thread(target=run, name="窗口1", args=(1,))
	    tt2 = threading.Thread(target=run, name="窗口2", args=(1,))
	    tt1.start()
	    tt2.start()
	    tt1.join()
	    tt2.join()
	    print("剩余票数%d"%num)
	    print("主进程结束")
		

		>>> 窗口2出票，剩余票数1
			窗口2出票，剩余票数0
			剩余票数0
			主进程结束

**上锁之后就不会出现票数为-1的情况了**

---

**python3提供了with方法，它会自动帮你上锁和解锁，非常方便**


			try:
				#上锁
	            lock.acquire()
	            if num > 0:
	                time.sleep(0.005)
	                num-=1
	                print("%s出票，剩余票数%d" % (threading.current_thread().name, num))
	            else:
	                break
	        finally:
	            #解锁
				lock.release()

			------------------------------------------------------

	使用with语句后

		with lock:
			if num > 0:
	                time.sleep(0.005)
	                num-=1
	                print("%s出票，剩余票数%d" % (threading.current_thread().name, num))
	            else:
	                break

- **死锁：由于可以存在多个锁，不同线程可以持不同的锁，并试图获取其他的锁，可能造成死锁，最终导致多线程只能挂起，只能靠操作系统强行终止。**

AB死锁案例

	import threading
	num = 0
	def run():
	    global num
	    while True:
	        if num%2 == 0:
	            with lockA:
	                print("%s在num=%s时获得A锁,num为偶数"%(threading.current_thread().name,num))
	                with lockB:
	                    print("%s在num=%s时获得B锁,num为偶数"%(threading.current_thread().name,num))
	        else:
	            with lockB:
	                print("%s在num=%s时获得B锁,num为奇数"%(threading.current_thread().name,num))
	                with lockA:
	                    print("%s在num=%s时获得A锁,num为奇数"%(threading.current_thread().name,num))
	        num+=1
	
	if __name__ == "__main__":
	    lockA = threading.Lock()
	    lockB = threading.Lock()
	    thread1 = threading.Thread(target=run, name = "线程01")
	    thread2 = threading.Thread(target=run, name="线程02")
	    thread1.start()
	    thread2.start()

	>>> 线程01在num=0时获得A锁,num为偶数
		线程01在num=0时获得B锁,num为偶数
		线程01在num=1时获得B锁,num为奇数
		线程01在num=1时获得A锁,num为奇数
		线程01在num=2时获得A锁,num为偶数
		线程02在num=2时获得B锁,num为奇数


 
 <font size="2">**从上面结果可以看出当线程01在执行到num=1之后，cpu开始处理线程02，这时线程02的num=1判断为奇数,这时cpu有转到线程01，线程01的num+=1变成2，判断为偶数获得A锁，这时cpu又转到线程02继续之前的奇数判断完的位置，此时显示获得奇数但num已经变成2，同时获得B锁，关键的地方到了··········线程01要想释放A锁就必须将A代码块中代码执行完，而执行完的前提是要获得B锁，反之线程02要想释放B锁需要获得A锁，这样就形成了死锁状态。**</font>

---



#### 信号量控制线程

> **信号量其实就是控制线程的并发数量，一个进程中最多可以同时开启线程的最大数量，比如线程池现在可以最多开启10个线程，而信号量控制在3，那么最多就只能同时开启三个线程，线程池中的剩余线程就只能被挂机，而没有信号量控制的时候，线程可以同时开启10个，但是超过10个，线程只能等待其他空闲线程**

	import threading
	import time
	import  random
	def run(i):
	    with semaphore:
	        #被信号量控制只能有三个线程同时开启，三个线程都没执行完则处于阻塞状态
	        print("%s%s开启了"%(threading.current_thread().name,i))
	        time.sleep(random.choice([1,3,5]))
	
	if __name__ == "__main__":
	    semaphore = threading.Semaphore(3)
	    for i in range(9):
	        #想要异步开启9个线程
	        thread = threading.Thread(target=run, args=("线程%s" % i,))
	        thread.start()

#### 延时线程


> **相当于一个定时器，规定时间开启进程**

	thread = threading.Timer(time,func)
	thread.start()
	在time时间后开启线程

#### 携程

> **协程，又称微线程，纤程，英文名Coroutine。协程的作用，是在执行函数A时，可以随时中断，去执行函数B，然后中断继续执行函数A（可以自由切换）。但这一过程并不是函数调用（没有调用语句），这一整个过程看似像多线程，然而协程只有一个线程执行。**

优点：

- 执行效率极高，因为子程序切换（函数）不是线程切换，由程序自身控制，没有切换线程的开销。所以与多线程相比，线程的数量越多，协程性能的优势越明显。
- 不需要多线程的锁机制，因为只有一个线程，也不存在同时写变量冲突，在控制共享资源时也不需要加锁，因此执行效率高很多。

测试代码

		import threading
		
		def func():
		    print("功能1执行了")
		    r = yield 1                     #yield 1相当于return 1 q区别：函数并没有返回而是指针指向下一个函数
		    print("功能2执行了r = %s"%r)   #前面的r可以当这个函数的形参，相当于func(r)
		    r = yield 2
		    print("功能3执行了")
		    r = yield 3
		    print("功能4执行了")
		    r = yield 4
		    print("功能5执行了")
		    r = yield 5
		if __name__ == "__main__":
		    m = func()
		    m.send(None) #开始必须传None使指针从头指针向下移一位
		    m.send("13")
		    print(next(m))#next(m)表示执行函数  有一个返回值yield（return）后面的值打印可以显示
		    print(next(m))

