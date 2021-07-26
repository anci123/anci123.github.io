---
title: "StarCoder暑訓week1"
tags: ["Starcoder暑訓","C++"]
categories: ["競程練題"]
date: 2021-07-26T23:10:40+08:00
draft: false
---
# 搜尋/排序/貪心
## 教材
### 線上教材
|教材|說明|
|----|----|
|[師大碼賽客：排序/貪心/二分搜](https://drive.google.com/file/d/1_7Ch2G52jH8fHqlO_Atmjp9smAnvq9R4/view)|子緯學長的教學講義（詳盡的新手入門）|
|[北一女培訓：排序](https://web.fg.tp.edu.tw/~tfgcsblog/blog/wp-content/uploads/2010/12/Training-2-Sorting-All.pdf)|六種排序法的程式與簡介|
|[建中培訓 (第4/6/7節)](https://tioj.ck.tp.edu.tw/uploads/attachment/5/12/1_2.pdf)|4. 排序STL / 6.貪心 / 7.二分搜|
|[台大資訊之芽：貪心](https://www.csie.ntu.edu.tw/~sprout/algo2019/ppt_pdf/week05/greedy.pdf)|貪心法與理論 / Huffman Tree|
|[成大競程培訓 (單元5/6)](https://nckuacm.github.io/2019/)|5.二分搜 / 6.三種排序|

### 線上影片


|影片|說明|
|---|---|
|[台大孔令傑老師：二分搜尋法](https://youtu.be/QVj81KR-_Hk)|7 分鐘學會二分搜尋法|
|[看舞蹈學排序法](https://www.youtube.com/user/AlgoRythmics/videos)|以舞蹈呈現各種排序法的運作過程|
|[台大陳縕儂老師：貪心](https://youtu.be/Q6VyP6P4ukA)|50 分鐘的正規演算法課程 (CLRS課本)|

### 演算法視覺化

| 演算法                                                       |                                    |
| ------------------------------------------------------------ | ---------------------------------- |
| [線性搜尋與二分搜尋](https://www.cs.usfca.edu/~galles/visualization/Search.html) | 以動畫呈現兩種搜尋法的運作過程     |
| [排序](https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html) | 以動畫呈現六種排序演算法的運作過程 |

## 題目

### A [ Flip Sort](https://vjudge.net/contest/446298#problem/A) [UVA 10327](https://vjudge.net/problem/UVA-10327/origin)

- 題目
  - 給一些未排序過的數字，將該數列由小到大排好，只能跟相鄰的數字交換，輸出最少要交換幾次
- 作法
  - bubble sort

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  int main(){
      int N=0;
      while(cin>>N){
          int n[N],ope=0;
          for(int i=0;i<N;++i) cin>>n[i];
          for(int i=0;i<N;++i){
              for(int j=N-1;j>i;--j){
                  if(n[j-1]>n[j]){
                      swap(n[j-1],n[j]);
                      ++ope;
                  }
              }
          }
          cout<<"Minimum exchange operations :"<<' '<<ope<<endl;
      }
      return 0;
  }
  ```

### B [ Age Sort](https://vjudge.net/contest/446298#problem/B) [UVA 11462](https://vjudge.net/problem/UVA-11462/origin)

- 題目
  - 將未排序的數列從小到大排好
- 作法
  - sort 函式
- Code
```C
#include<bits/stdc++.h>
using namespace std;
int main(){
    int N=0;
    while(cin>>N && N){
        int n[N]={0};
        for(int i=0;i<N;++i) cin>>n[i];
        sort(n,n+N);
        for(int i=0;i<N-1;++i) cout<<n[i]<<' ';
        cout<<n[N-1]<<endl;
    }
    return 0;
}
```

### C [ Conformity](https://vjudge.net/contest/446298#problem/C) [UVA 11286](https://vjudge.net/problem/UVA-11286/origin)

- 題目

  - 一列(五個)課程為一個組合，輸出最多人選的課程組合的人數，若有多個組合的人數等於最大值則相加

- 作法

  - 將課程排序後形成一組字串，每個組合就是一串字串，並用map記錄該組合的人數，最後記錄最大值，加上所有最多人選的組合的人數

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  int main(){
      map<string,int> studentNumber;
      int N=0;
      while(cin>>N && N){
          int max=0,total=0;
          studentNumber.clear();
          while(N--){
              vector<string> courseId;
              string s;
              for(int j=0;j<5;++j) cin>>s, courseId.push_back(s);
              sort(courseId.begin(),courseId.end());
              s.clear();
              for(int j=0;j<5;++j) s+=courseId[j];
              ++studentNumber[s];
          }
          for(auto it=studentNumber.begin();it!=studentNumber.end();++it) if(it->second>max) max=it->second;
          for(auto it=studentNumber.begin();it!=studentNumber.end();++it) if(it->second==max) total+=max;
          cout<<total<<endl;
      }
  
      return 0;
  }
  ```

  

### D [ Guessing Game](https://vjudge.net/contest/446298#problem/D) [UVA 10530](https://vjudge.net/problem/UVA-10530/origin)

- 題目

  - 猜數字，輸入會給數字並說目標是比該數大或小或是猜對了，若是該敘述錯誤則判斷為說謊

- 作法

  - 紀錄目標數可能在的區間，判斷是否說謊

- Code

  ```C
  #include <bits/stdc++.h>
  using namespace std;
  int main() {
      int n;
      while(scanf("%d ", &n) != EOF && n != 0) {
          int s = 1, e = 10;
          string str;
          while(getline(cin, str) && str != "right on") {
              if(str == "too high") e = min(e, n - 1);
              else if(str == "too low") s = max(s, n + 1);
              scanf("%d ", &n);
          }
          if(n >= s && n <= e) cout << "Stan may be honest\n";
          else cout << "Stan is dishonest\n";
      }
      return 0;
  }
  ```

###  E [ Ancient Cipher](https://vjudge.net/contest/446298#problem/E) [UVA 1339](https://vjudge.net/problem/UVA-1339/origin)

- 題目

  - 判斷第一串字串能否轉換成第二串字串(檢查字母出現頻路是否相同)

- 作法

  - 紀錄子母出現次數並排序，檢查其出現頻率是否相同

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  int main()
  {
      char s1[105];
      char s2[105];
      int len;
      bool isOk;
      while(cin >> s1 >> s2){
          isOk = true;
          len = strlen(s1);
          int cnt1[26]={0};
          int cnt2[26]={0};
          for(int i = 0; i < len;++i){
              int curC1 = s1[i] - 'A';
              int curC2 = s2[i] - 'A';
              cnt1[curC1]++;
              cnt2[curC2]++;
          }
          sort(cnt1, cnt1 + 26);
          sort(cnt2, cnt2 + 26);
  
          for(int i = 0 ; i < 26;++i){
              if(cnt1[i] != cnt2[i]){
                  isOk = false;
                  break;
              }
          }
          if(isOk) cout << "YES" <<endl;
          else cout << "NO" << endl;
      }
      return 0;
  }
  ```

  

### F [ Bridge Hands](https://vjudge.net/contest/446298#problem/F) [UVA 555](https://vjudge.net/problem/UVA-555/origin)

- 題目

  - 輸入會表示從誰開始發牌及卡牌的資訊，輸出每個人的手牌並依照題目的規定排序手牌

- 作法

  - 模擬發牌過程，並在最後為每個人牌好手牌

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  
  int main(){
      char s=0;
      char sit[4]={'S','W','N','E'};
      while(cin>>s && s!='#'){
          map<int,string> cards[4];
          int start=0;
          string str,line;
          for(int i=0;i<4;++i) if(s==sit[i]) start=i;
          for(int i=0;i<2;++i){
              cin>>line;
              str+=line;
          }
          for(int j=0;j<str.length();j+=2){
              ++start;
              if(start>=4) start=0;
              string t="  ";
              t[0]=str[j];t[1]=str[j+1];
              int id=0;
              char c=t[0];
              if(c=='C') id=100;
              else if(c=='D') id=200;
              else if(c=='S') id=300;
              else if(c=='H') id=400;
              c=t[1];
              if(isdigit(c)) id+=(t[1]-'0');
              else if(c=='T') id+=10;
              else if(c=='J') id+=11;
              else if(c=='Q') id+=12;
              else if(c=='K') id+=13;
              else if(c=='A') id+=14;
              cards[start][id]=t;
          };
          for(int i=0;i<4;++i){
              cout<<sit[i]<<':';
              for(auto it=cards[i].begin();it!=cards[i].end();++it) cout<<" "<<it->second;
          cout<<endl;
          }
      }
      return 0;
  }
  ```

### G [ Vito's Family](https://vjudge.net/contest/446298#problem/G) [UVA 10041](https://vjudge.net/problem/UVA-10041/origin)

- 題目

  - 找到從某棟房子出發，拜訪每一戶的最短距離

- 作法

  - 找出中位數，算出所有距離的和

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  int main(){
      int t=0;
      cin>>t;
      while(t--){
          int N=0,s,house,dis=0,size;
          cin>>N;
          vector<int> street;
          while(N--){
              cin>>s;
              street.push_back(s);
          }
          sort(street.begin(),street.end());
          size=street.size();
          house=street[size/2];
          for(auto i:street) dis+=abs(house-i);
          cout<<dis<<endl;
      }
      return 0;
  }
  ```

### H [ Shoemaker's Problem](https://vjudge.net/contest/446298#problem/H) [UVA 10026](https://vjudge.net/problem/UVA-10026/origin)

- 題目
  - 輸入會提供每項工作的編號、天數及罰金，算出能使罰金最少的工作順序

- 作法

  - 算出每個工作的權重(罰金/天數)，並由大到小排序

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  typedef struct{
      double cp;
      int num;
  }work;
  bool cmp(work a,work b){
      if(a.cp>b.cp) return true;
      else return false;
  }
  int main(){
      int t,N;
      string s;
      cin>>t;
      getline(cin,s);
      getline(cin,s);
      while(t--){
          cin>>N;
          work w[N];
          for(int i=0;i<N;++i){
              double time,fine,cp;
              cin>>time>>fine;
              cp=fine/time;
              w[i].cp=cp;
              w[i].num=i+1;
          }
          sort(w,w+N,cmp);
          for(int i=0;i<N-1;++i) cout<<w[i].num<<" ";
          cout<<w[N-1].num<<endl;
          if(t>0) cout<<endl;
      }
      return 0;
  }
  ```

### I [The Bus Driver Problem](https://vjudge.net/contest/446298#problem/I) [UVA 11389](https://vjudge.net/problem/UVA-11389/origin)

- 題目
  - 輸入會給公車牌班的時數，若超過規定時數就要給加班費，找出最少加班費的安排

- 作法

  - 先將時數排序過，再將一組時數顛倒過後配對在一起並相加，計算出加班費

- Code

  ```C
  #include<bits/stdc++.h>
  using namespace std;
  int main(){
      int n,d,r;
      while(cin>>n>>d>>r && n && d && r){
          int m,a,time=0,auth=0;
          vector<int> mor;
          vector<int> aft;
          for(int i=0;i<n;++i) cin>>m,mor.push_back(m);
          for(int i=0;i<n;++i) cin>>a,aft.push_back(a);
          sort(mor.begin(),mor.end());
          sort(aft.begin(),aft.end());
          for(int i=0;i<n;++i){
              int total=mor[i]+aft[n-i-1];
              if(total>d) auth+=(total-d)*r;
          }
          cout<<auth<<endl;
      }
      return 0;
  }
  ```

### J [Watering Grass](https://vjudge.net/contest/446298#problem/J) [UVA 10382](https://vjudge.net/problem/UVA-10382/origin)

- 題目
  - 找出最小需要幾個 sprinkler，灑水範圍才能覆蓋整個草坪
- 作法
  - 轉成一維，算區間覆蓋
  - 貪心法
  - 區間覆蓋

- Code

  ```C
  #include <bits/stdc++.h>
  using namespace std;
  #define F first
  #define S second
   
  bool cmp(pair<double, double> a, pair<double, double> b) {
      if (a.first == b.first)
          return a.second > b.second;
      else
          return a.first < b.first;
  }
   
  int main() {
      int n;
      double p, r; // position, radius
      double l, w, dx;
       
      while (cin >> n >> l >> w) {
          w /= 2.0;
          vector<pair<double, double> > v;
          for (int i=0; i<n; i++) {
              cin >> p >> r;
              if (r > w){ //排除沒用的噴水頭
                  dx = sqrt(r*r - w*w);
                  v.push_back({p-dx, p+dx}); //轉換成區間覆蓋問題
              }
          }
          sort(v.begin(), v.end(), cmp);
           
          int ans = 0;
          double right = 0.0;
          for (int i = 0; i < v.size(); i++){
              if (v[i].F > right) break;
              for (int j = i+1; j < v.size() && v[j].F <= right; j++){
                  if (v[j].S > v[i].S){
                      i = j;
                  }
              }
              ans++;
              right = v[i].S;
              if (right >= l) break;
          }
           
          if (right >= l) cout << ans << endl;
          else cout << endl;
      }
      return 0;
  }
  ```

### K [ Ultra-QuickSort](https://vjudge.net/contest/446298#problem/K) [UVA 10810](https://vjudge.net/problem/UVA-10810/origin)

- 題目

  - 算出最小交換次數

- 作法

  - merge soert
  - BIT

- Code

  ```C
  #include <bits/stdc++.h>
  using namespace std;
  long long ans = 0;
  long long a[500005];
  void mergeSort(long long *arr, int len) {
      if(len <= 1) return;
      int leftLen = len / 2, rightLen = len - leftLen;
      long long *leftArr = arr, *rightArr = arr + leftLen;
      mergeSort(leftArr, leftLen);
      mergeSort(rightArr, rightLen);
      static long long tmp[500005];
      long long tmpLen = 0, l = 0, r = 0;
      while(l < leftLen && r < rightLen) {
          if(leftArr[l] < rightArr[r]) tmp[tmpLen++] = leftArr[l++];
          else {
              tmp[tmpLen++] = rightArr[r++];
              ans += leftLen - l;
          }
      }
      while(l < leftLen) tmp[tmpLen++] = leftArr[l++];
      while(r < rightLen) tmp[tmpLen++] = rightArr[r++];
      for(int i = 0; i < tmpLen; ++i) arr[i] = tmp[i];
  }
  int main() {
      int n;
      while(cin >> n && n) {
          ans = 0;
          for(int i = 0; i < n; ++i) cin >> a[i];
          mergeSort(a, n);
          cout << ans << endl;
      }
      return 0;
  }
  ```

  

