# MST


# MST

## dijkstra
<!--more-->
- 固定一點，找該點與其他點之最短路徑

  ![Dijkstra_Animation](/picture/Dijkstra_Animation.gif)

```C++
#include<bits/stdc++.h>
using namespace std;
#define INF 0x3f3f3f3f
const int MAX = 10;
bool visit[MAX] = {false};
int adj[MAX][MAX], dist[MAX];
void addEdge(int p1, int p2, int w) {
    adj[p1][p2] = w;
}
void dijkstra(int start) {
    for(int i = 0; i < MAX; ++i) {
        visit[i] = false;
        dist[i] = INF;//初始設定
    }
    dist[start] = 0;//設定原點
    for(int i = 0; i < MAX; ++i) {
        int mini_dist = INF, mini_node = -1;
        for(int j = 0; j < MAX; ++j) {
            if (!visit[j] && dist[j] < mini_dist) {
                mini_node = j;
                mini_dist = dist[j];//找到距離最短
            }
        }
        if(mini_node == -1) break;//沒找到，代表所有點都取過
        visit[mini_node] = true;//標示已取
        for(int j = 0; j < MAX; ++j) {
            if(!visit[j] && adj[mini_node][j] != 0 && dist[j] > dist[mini_node] + adj[mini_node][j])
                dist[j] = adj[mini_node][j] + dist[mini_node];//對其他點做鬆弛
        }
    }
}
int main() {
    int T;
    cin >> T;
    memset(adj, 0, sizeof(adj));
    while(T--) {
        int p1, p2, w;
        cin >> p1 >> p2 >> w;
        addEdge(p1, p2, w);
    }
    int start = 0;
    dijkstra(start);
    for(int i = 0; i < MAX; ++i) cout << dist[i] << endl;
    return 0;
}
```


