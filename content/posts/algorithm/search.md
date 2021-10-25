---
title: "Search"
date: 2021-08-16T17:32:34+08:00
draft: false
---
<!--more-->
# search
## binary search
* 跟中間的數字比較以判斷目標的落點，加速尋找的速度
* 回傳目標數的index
* 注意:搜尋前需要先排序過
![](https://i.imgur.com/uR0vWaY.png)
```C++
int binary_search(vector<int> sort,int target){
    int size=sort.size(),left=0,right=size;
    while(left<=right){
        int mid=(left+right)/2;
        if(target>sort[mid]) left=mid+1;
        else if(target<sort[mid]) right=mid-1;
        else if(target==sort[mid]) return mid;
    }
    return -1;
}
```
## dfs
- 拜訪所有點
```C++
int vector<vector<int>> E;
void dfs(int u, int dep) {
    for (auto v: E[u]) {
        if (vis[v]) continue;
        vis[v] = true;
        dfs(v, dep+1);
    }
}
```
### 擴展dfs
```C++
int dx[]={0,0,-1,1};
int dy[]={1,-1,0,0};
void dfs(int x,int y,char pre,char nex){
    if(x<0 || x>width-1) return;
    if(y<0 || y>height-1) return;
    if(paper[y][x]!=pre) return;
    paper[y][x]=nex;
    for(int i=0;i<4;++i) dfs(x+dx[i],y+dy[i],pre,nex);
}
```
