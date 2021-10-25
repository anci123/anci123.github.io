---
title: "Sort"
tags: ["algorithm","C++"]
categories: ["algorithm"]
date: 2021-08-16T17:32:43+08:00
draft: false
---
<!--more-->
# 搜尋
## 暴力搜尋法(窮舉)
1. 找到最大值及最小值
2. 設定一個i值從最小值開始遞增到最大值
3. 檢查陣列中是否有等於i值的數，全部列出
```C++
void brute_force(int array[], int size){
    int max_value = array[0];
    int min_value = array[0];
    for (int i=0;i<size;++i){
        max_value = max(max_value, array[i]);
        min_value = min(min_value, array[i]);
    }
    //找到最大及最小值
    for (int i=min_value; i<=max_value; ++i){
        for (int j=0; j<size; ++j) if (array[j] == i) cout << i<<" ";
        // 看看陣列裡面有沒有等於i的值，全部都列出來
    }
    cout<<endl;
}
```
## selection sort
* 找到最小(或最大)的數字的位置(index)，將它移到最前面
```C++
void selsction_sort(int *array,size){
  for(int i=0;i<size;++i){
    int min_index=i;
    for(int j=i+1;j<size;++j){
      if(a[j]<a[min_index]) min_index=j;
    }
    swap(a[i],a[min_index]);
  }
}
```
## bubble sort 泡沫排序
* 兩兩比較並交換
```C++
void bubble_sort(int array[], int size){
    for(int i=0;i<size;++i){
        for(int j=0;j<size-i-1;++j){
            if(array[j]>=array[j+1]) swap(array[j],array[j+1]);
        }
    }
}
```
## gnome sort 侏儒排序
* 優點:只需要一個while迴圈
* 遇到一個數小於前一個數時交換，index開始遞減，檢查前面是否有更小的數
* 圖例:
![](https://i.imgur.com/s87CE5z.gif)

```C++
void gnome_sort(int array[], int size){
    int i=0;
    while (i<size){
        if (i == 0 || array[i-1] <= array[i]) i++;
        else{
            swap(array[i-1], array[i]);
            i--;
        }
    }
}
```
## Insertion sort 插入排序
* 若是前面一個數比現在的數字大，就往後挪並覆蓋掉原本的數字(需要有另一數記住原本的數字)，以找到當前數字應該在的位置
* 過程需要大量向右挪移
* 結構如果是list 可直接插入
![](https://i.imgur.com/J0931yG.gif)
```C++
void insertion_sort(int array[], int size){
    for (int i=1; i<size; ++i){
        int pivot = array[i];
        int j;
        for (j=i; j>0; --j){
            if (pivot < array[j-1])
                array[j] = array[j-1];  // 將比較大的數往右挪
            else
                break;
        }
        array[j] = pivot;    // 挪移完後直接放入所在的位置
    }
}
```
## merge sort
1. 將數串不停對半分，直到單個數串只有一個數
2. 將分割好的數串按照大小分別從兩邊的數串填入數字到另一數串 

![](https://i.imgur.com/3JRSjI9.png)

* 遞迴版的merge sort
```C++
void merge(int arr1[],int arr2[],int merge[],int s1,int s2){
    int index=0,index1=0,index2=0;
    int a1[s1]={0},a2[s2]={0};
    for(int i=0;i<s1;++i) a1[i]=arr1[i];
    for(int i=0;i<s2;++i) a2[i]=arr2[i];
    while(index<s1+s2){
        if(index1<s1 && index2<s2){
            if(a1[index1]<=a2[index2]){
                merge[index]=a1[index1];
                ++index1;
            }
            else{
                merge[index]=a2[index2];
                ++index2;
            }
            ++index;
        }
        else{
            while(index1<s1){
                merge[index]=a1[index1];
                ++index1;
                ++index;
            }
            while(index2<s2){
                merge[index]=a2[index2];
                ++index2;
                ++index;
            }
        }
    }
    //填入數串
}
void merge_sort(int array[], int size){
    if(size<=1) return;
    int mid=size/2,newArr[size]={0};
    merge_sort(array,mid);
    merge_sort(&array[mid],size-mid);
    merge(array,&array[mid],array,mid,size-mid);
    //對半分，再組合在一起
}
```
## quick sort
* 選定一個樞紐(pivot)之後
* 將左邊大於樞紐的數跟右邊小於樞紐的數互換
![](https://i.imgur.com/dyJxKxK.png)
```C++
void quick_sort(int array[], int left, int right){
    //left: 最小的索引值:0，right:最大索引值ex:10-1=9
    if (left < right){
        // divide (partition)
        int pivot = array[(left+right)/2];  // pivot 可以隨便選
        int i = left - 1, j = right + 1;
        while (i < j){
            do ++i; while (array[i] < pivot);
            do --j; while (array[j] > pivot);
            if (i < j) swap(array[i], array[j]);
        }
        quick_sort(array, left, i-1);
        quick_sort(array, j+1, right);
        // 分別sort pivot兩邊的數串
    }
}
```

## counting sort
* 創建另一個新的大陣列，並初始化為零
* 依照原陣列中的數字，在新的陣列對應索引號的值加一
    (表示每個數字總共有幾個)
* 遍歷新的陣列，並依照紀錄的數字數量將數填回原陣列
* 缺點:只能記大於等於零的整數
* 優點:不需要計算
![](https://i.imgur.com/REvgXoQ.png)

```C++
void counting_sort(int array[], int size){
    int count[10000] = {0};
    for (int i=0; i<size; ++i) count[ array[i] ]++;
    // 紀錄對應的數字有幾個
    // 計數陣列的索引值大小順序，正是元素大小順序。
    for (int i=0, k=0; k<size; ++i) while (count[i]--) array[k++] = i;
}
```