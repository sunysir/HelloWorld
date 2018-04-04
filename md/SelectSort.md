#选择排序

>	**顾名思义，选择排序就是把通过遍历数组选择其中最小的数把其放到首位，然后在遍历数组首位之后的数组在选出最小值放到第二位，以此类推，直接最后一位为止。**

<img src="">

java代码
	
	package selectSort;

	public class SelectSort{
		public static void main(String[] args) {
			Comparable[] a = {1, 45, 32, 12, 34, 16, 85, 3, 8, 15};
			sort(a);
			show(a);
			
		}
		//排序方法
		public static void sort(Comparable[] a){
			for(int i = 0; i < a.length; i++){
				int min = i;
				for(int j = i+1; j < a.length; j++){
					if(less(a[j], a[min])){
						exch(a, j, min);
					}
				}
			}
		}
		public static boolean less(Comparable a, Comparable b){
			return a.compareTo(b)<0;
		}
		//数组中两个数交换方法
		public static void exch(Comparable[] arr, int i, int j){
			Comparable temp;
			temp = arr[i];
			arr[i] = arr[j];
			arr[j] = temp;
		}

		//数组显示方法
		public static void show(Comparable[] a){
			for(int i = 0; i < a.length; i++){
				System.out.print(a[i]+"  ");
			}
		}
		//检验数组是否已经有序方法
		public static boolean isSorted(Comparable[] a){
			for(int i = 1; i < a.length; i++){
				if(less(a[i], a[i-1])){
					return false;
				}
			}
			return true;
		}
	}



