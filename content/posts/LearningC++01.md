---
title: "LearningC++01"
date: 2021-07-25T15:33:31+08:00
---

# C++學習筆記

[toc]

## 標頭檔

* **<bits/stdc++.h>** 是萬能標頭檔，有了他就不用寫其他的標頭檔
* **using name std;** 有了它就可以不用一直帶上函式庫的全名(std::)

```c++=
#include<bits/stdc++.h>
using namespace std;
```

**但上面的作法會讓程式跑的速度變慢，可以使用以下方法**

* sync_with_stdio 式可以兼容 stdio 的意思，這是 C++ 為了可以兼容C所做的一個設定
* cin.tie 這是將 cin 跟 cout 綁定的意思
* endl 是 換行 加上 flush(清空緩衝區)，換成'\n'，速度會快上許多

```C++=
ios::sync_with_stdio(0);
cin.tie(0); 
cout<<"Hello"<<'\n';
```

## 輸入

### stringstream

* stringstream 應用

  * int -> string

  ```C++=
  string convert;
  stringstream ss;
  int number=123456;
  ss<<number;
  ss>>convert;
  ```

  * string -> int

  ```C++=
  string numstr="123";
  int num;
  stringstream ss;
  ss<<numstr;
  ss>>num;
  ```

  * 清空

  ```C++=
  ss.str("");
  ss.claer;
  ```

  * 檢查是否轉型成功

  ```C++=
  stringstream ss("12.0505");
  double d;
  ss<<d;
  if(!ss) cout<<"error type"<<endl;
  else cout<<d<<endl;
  ```

  * 一串字串中有多組int(用空格切字串)

  ```C++=
  string s="13 -456 6566 121 48";
  stringstream ss(s);
  int a;
  while(ss>a){
      cout>>a>>endl;
  }
  ```

### sscanf

* 利用 sscanf 取得部分字串(篩選)

  * **[]** 中放要讀取的字元範圍，如 [a-z],[^=]
  * **^** 是**反**的意思
  * **\* 是**所有**
  * **\*[^]** 是跳過符合的字串

  ```c++=
  char str[10];
  char st2[10];
  cin>>str;
  sscanf(str,"%[^-]",st2);
  cout<<st2<<endl;
  //input:123-ABC
  //output:123
  ```

  ```C++=
  char str[10];char st2[10];cin>>str;sscanf(str,"%*[^-]-%s",st2);cout<<st2<<endl;//input:123-ABC//output:ABC
  ```

## 輸出

### 格式對齊

1. setw(n)
   * n規定輸出的格數，若n小於輸出的位數則會被忽視

```C++=
cout<<setw(3)<<1<<endl;
//  1
cout<<setw(3)<<12345<<endl;
//12345
```

2. setfill(char)

```C++=
    string s="qwe";
    cout<<setw(5)<<setfill('*')<<s;
    //**qwe
```