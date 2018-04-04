---
layout:     post
title:      "插入排序"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-01-06 19:00:00
author:     "suny"
catalog: false
categories: Algorithms
tags:
    - 笔记
---
# 插入排序
> **顾名思义，插入排序就是取第一个数后面的数与第一个对比，如果比第一个数小，两个数就交换（插入第一个数之前），这样，数组中第一个数就变成了第二个数，而插入的那个数变成数组中第一个数，所以数组中前两个数就变成有序数组了，然后在取有序数组后面的一个数（对比数）与有序数组从后往前对比，如果比（对比数）大，两数进行交换，继续与前一个数对比，只要大就交换，小则终止，以此类推，直接最后一个数比较完为止。废话连篇（No picture say JB），上图。**

<img src="/img/InsertSort.jpg"/>


从图中可以看出该算法最大时间复杂度为O（n^2）

java代码 
	
	package insertSort;

	public class InsertSort1 {
	    public static void main(String[] args) {
	        Comparable[] a = {'a', 'd', 'c', 'b', 'f', 'e', 'k', 'g', 'm', 'l', 'j', 'h', 'i'};
	        sort(a);
	        show(a);
	    }
	
	    public static void sort(Comparable[] a){
	        for(int i = 1; i < a.length; i++){
	            for(int j = i; j > 0 && less(a[j], a[j-1]); j--){
	                exch(a, j, j-1);
	            }
	        }
	    }
	
	    public static void insert(Comparable[] a, int i, int j){
	        Comparable temp = a[j];
	        for(int k = j; k > i; k--){
	            a[k] = a[k-1];
	        }
	        a[i] = temp;
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

> 前面这种是倒序查找插入，我个人感觉从前面插入排序也差不多，比有序数组中的数小就插入前面，否则向后继续遍历，直到找到比数组中的数小则停止。

<img src="/img/InsertSort1.jpg"/>

java代码


	package insertSort;

	public class InsertSort {
	    public static void main(String[] args) {
	        Comparable[] a = {'a', 'd', 'c', 'b', 'f', 'e', 'k', 'g', 'm', 'l'};
	        sort(a);
	        show(a);
	    }
	
	    public static void sort(Comparable[] a){
	        for(int i = 1; i < a.length; i++){
	            for(int j = 0; j< i; j++){
	                if(less(a[i], a[j])){
	                    insert(a, j, i);
	                    break;
	                }
	            }
	        }
	    }
	
	    public static void insert(Comparable[] a, int i, int j){
	        Comparable temp = a[j];
	        for(int k = j; k > i; k--){
	            a[k] = a[k-1];
	        }
	        a[i] = temp;
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
