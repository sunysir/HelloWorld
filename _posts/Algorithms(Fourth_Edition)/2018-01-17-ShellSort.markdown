---
layout:     post
title:      "希尔排序"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-01-16 20:16:00
author:     "suny"
catalog: true
categories: Algorithms
tags:
    - 笔记
---
# 希尔排序

> **希尔排序就是插入排序的升级版，其更高效的原因是它权衡了子数组的规模性和有序性。它首先把数组分为N-h组(其中N为数组元素个数，这个h可以自己看情况定)，然后把h小组对应的数进行排序，使其小规模有序，最后在大规模进行排序。**

**上图。。。**

<img src="/img/ShellSort.jpg"/>

java代码

	package shellSort;

	public class ShellSort {
		public static void main(String[] args) {
			Comparable[] a = {'z', 'l', 'c', 'b', 'f', 'e', 'k', 'g', 'm', 'a'};
			sort(a);
			show(a);
		}
		
		public static void sort(Comparable[] a){
			int h = 1;
			int N = a.length;
			//把数组分为N-h组
			while(h <= N/2)h = 3*h+1;
			//各组分别排序最后h=1时为总体排序
			while(h>=1){
				for(int i = h; i < N; i++){
					for(int j = i; j >= h && less(a[j], a[j-h]); j-=h){
						exch(a, j-h, j);
					}
				}
				h = h/3;
			}
		}
		
		public static boolean less(Comparable a, Comparable b){
			return a.compareTo(b)<0;
		}
		public static void exch(Comparable[] arr, int i, int j){
			Comparable temp;
			temp = arr[i];
			arr[i] = arr[j];
			arr[j] = temp;
		}
		public static void show(Comparable[] a){
			for(int i = 0; i < a.length; i++){
				System.out.print(a[i]+"  ");
			}
		}
		public static boolean isSorted(Comparable[] a){
			for(int i = 1; i < a.length; i++){
				if(less(a[i], a[i-1])){
					return false;
				}
			}
			return true;
		}
	}


