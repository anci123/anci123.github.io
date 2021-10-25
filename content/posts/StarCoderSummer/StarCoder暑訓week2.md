---
title: "StarCoder暑訓week2"
tags: ["Starcoder暑訓","C++"]
categories: ["競程練題"]
date: 2021-08-04T16:30:24+08:00
draft: false
---
<!--more-->
# 基礎資料結構與STL 
## 模板連結
[STL]({{< ref "posts/algorithm/STL.md" >}})

## 內容大綱

| 資料結構                              | 簡要說明                                                   | C++ 內建            |
| ------------------------------------- | ---------------------------------------------------------- | ------------------- |
| 陣列                                  | 在記憶體中連續，支援隨機存取以及 O(1) 插入尾端             | std::vector         |
| 字串                                  | 以 ‘\0’ 結尾的字元陣列                                     | std::string         |
| 串列 linked list                      | 支援 O(1) 的插入與刪除                                     | std::list           |
| 堆疊 stack                            | 支援後進先出 (LIFO) 的存取模式                             | std::stack          |
| 佇列 queue                            | 支援先進先出 (FIFO) 的存取模式                             | std::queue          |
| 堆積 heap (  優先隊列 priority_queue) | 支援 O(logN) 的插入和 O(logN) 取出最大/小值                | std::priority_queue |
| 併查集 disjoint set                   | 有效率地合併兩個集合、有效率地查詢兩個元素是否屬於同一集合 | 無 (要自己寫)       |
| 平衡搜尋樹                            | 記錄 (鍵, 值) 對應關係，支援 O(logN) 的插入和查詢          | std::map            |
| 平衡搜尋樹                            | 實現「集合」，支援 O(logN) 的插入和查詢                    | std::set            |

## 教材

### 線上教材

| 教材                                                                                                                                         | 說明                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| [師大碼賽客：基礎資料結構/STL](https://drive.google.com/file/d/1XoAMrDslzOPR6THMBpW1Xt5xfc_9hnaA/view?usp=sharing)                           | 品新學長的教學講義（詳盡的STL語法示範與題目解說） |
| [板中培訓：STL](https://drive.google.com/file/d/1Gir6DKICVljhpfzW1_Q4Rhs81riPyIiW/view)                                                      | STL語法                                           |
| [建中培訓 (第3節)](https://tioj.ck.tp.edu.tw/uploads/attachment/5/12/1_2.pdf)                                                                | STL語法                                           |
| [北一女培訓：樹/二元樹/Heap/BST](http://web.fg.tp.edu.tw/~tfgcsblog/blog/wp-content/uploads/2010/12/樹狀結構TreeHeap.ppt)                    | 樹狀結構投影片                                    |
| [北一女培訓：並查集  (disjoint set)](http://web.fg.tp.edu.tw/~tfgcsblog/blog/wp-content/uploads/2016/07/06_1_進階資料結構_Disjoint_Set.pptx) | 並查集投影片                                      |
| [成大競程培訓 (單元2/3/4)](https://nckuacm.github.io/2019/)                                                                                  | 資結/STL/樹/圖                                    |

 

### 演算法視覺化

| 資料結構                                                                   | 說明                                                       |
| -------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [堆積 (heap)](https://www.cs.usfca.edu/~galles/visualization/Heap.html)    | 最小堆積的插入與取值動畫（圖形結構與陣列內容）：推薦！     |
| [並查集](https://www.cs.usfca.edu/~galles/visualization/DisjointSets.html) | 並查集的 union/find 操作動畫（圖形結構與陣列內容）：推薦！ |

 

## 題目練習

### 題目列表與提示

| 題目      | 題目需求                             | 採用結構                                       | 優先練習 |
| --------- | ------------------------------------ | ---------------------------------------------- | -------- |
|           |                                      |                                                |          |
| UVa 673   | 括號匹配與 LIFO 操作                 | std::stack                                     | v        |
| UVa 442   | 括號匹配與 LIFO 操作                 | std::stack                                     |          |
| UVa 12100 | 遍歷和 FIFO 操作                     | std::queue (加上 std::priority_queue 效率更高) | v        |
| UVa 245   | 取出第 n 個以及插入頭端              | std::list / std::deque / std::vector           |          |
| UVa 1203  | 插入與取出最小值                     | std::priority_queue                            | v        |
| UVa 11995 | 模擬 stack, queue, priority_queue    | std::stack, std::queue, std::priority_queue    | v        |
| UVa 10583 | 標準併查集操作                       | disjoint set                                   | v        |
| UVa 11987 | 併查集的變化題(值得思考)             | disjoint set                                   |          |
| UVa 1665  | 判斷連通塊數                         | disjoint set                                   |          |
| UVa 230   | 字串排序與搜尋                       | std::map / std::set                            | v        |
| UVa 1592  | 字串比較（將字串轉成數值以加快比較） | std::map                                       |          |

### A [Parentheses Balance](https://vjudge.net/contest/447620#problem/A) [UVA 673](https://vjudge.net/problem/UVA-673/origin)

- 題目

  - 判斷兩邊括號是否成對

- 作法

  - 運用stack，遇到右括號時將相應的左括號吐出來，最後檢查stack是否為空

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  int main() {
      int n;
      string str;
      cin >> n;
      cin.ignore();
      while(n--) {
          stack<char> s;
          getline(cin, str);
          for(auto i : str) {
              if(i == ']') {
                  if(!s.empty() && s.top() == '[') s.pop();
                  else s.emplace(i);
              }
              else if(i == ')') {
                  if(!s.empty() && s.top() == '(') s.pop();
                  else s.emplace(i);
              }
              else s.emplace(i);
          }
          cout << (s.empty() ? "Yes" : "No") << endl;
      }
      return 0;
  }
  ```

### B [ Matrix Chain Multiplication](https://vjudge.net/contest/447620#problem/B) [UVA 442](https://vjudge.net/problem/UVA-442/origin)

- 題目
  - 檢查該矩陣運算是否成立，若成立則輸出運算過程中總共要幾次乘法，計算方式為 n1\*n2\*m2
  
- ˊ作法
  - 運用stack
  
- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  typedef struct {
      int row;
      int col;
  } matrix;
  int main() {
      int n;
      char name;
      string str;
      matrix m;
      cin >> n;
      map<char, matrix> mTable;
      while(n--) cin >> name >> m.row >> m.col, mTable[name] = m;
      cin.ignore();
      while(getline(cin, str)) {
          bool error = false;
          int mult = 0;
          matrix a, b, result;
          stack<matrix> ms;
          if(str.length() <= 1) cout << '0' << endl;
          else {
              for(auto i : str) {
                  if(i == '(') continue;
                  if(i != ')') {
                      ms.emplace(mTable[i]);
                      continue;
                  }
                  if(ms.size() >= 2) {
                      b = ms.top();
                      ms.pop();
                      a = ms.top();
                      ms.pop();
                      if(a.col == b.row) {
                          mult += a.row * a.col * b.col;
                          result.row = a.row;
                          result.col = b.col;
                          ms.push(result);
                      }
                      else {
                          error = true;
                          break;
                      }
                  }
              }
              if(error) cout << "error" << endl;
              else cout << mult << endl;
          }
      }
      return 0;
  }
  ```

### C [ Printer Queue](https://vjudge.net/contest/447620#problem/C) [UVA 12100](https://vjudge.net/problem/UVA-12100/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  int main() {
      int n;
      cin >> n;
      while(n--) {
          priority_queue<int> pq;
          queue<int> q;
          int time, priority, job, ans = 0;
          cin >> time >> priority;
          for(int i = 0; i < time; ++i) {
              cin >> job;
              pq.push(job);
              q.push(job);
          }
          if(time == 1) cout << "1" << endl;
          else {
              while(1) {
                  if(q.front() == pq.top()) {
                      pq.pop();
                      q.pop();
                      ans++;
                      if(!priority) break;
                      else priority--;
                  }
                  else {
                      q.push(q.front());
                      q.pop();
                      if(!priority) priority = q.size() - 1;
                      else priority--;
                  }
              }
              cout << ans << endl;
          }
      }
      return 0;
  }
  ```

  

### D [Uncompress](https://vjudge.net/contest/447620#problem/D) [UVA 245](https://vjudge.net/problem/UVA-245/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  int main() {
      list<string> list;
      string str;
      stringstream ss;
      while(getline(cin, str) && str != "0") {
          string word = "";
          for(int i = 0; i < str.size(); ++i) {
              int index = 0;
              if(isdigit(str[i])) {
                  index = str[i] - '0';
                  while(isdigit(str[++i])) index = index * 10 + (str[i] - '0');
                  --i;
                  index--;
                  if(index < list.size()) {
                      auto it = list.begin();
                      while(index--) it++;
                      string temp = *it;
                      list.erase(it);
                      cout << temp;
                      list.push_front(temp);
                  }
                  else cout << ++index;
              }
              else if(!isalpha(str[i])) {
                  if(word.size() > 0)list.push_front(word);
                  word = "";
                  cout << str[i];
              }
              else if(isalpha(str[i])) {
                  cout << str[i];
                  word = word + str[i];
              }
          }
          if(word.size() != 0) list.push_front(word);
          cout << endl;
      }
      return 0;
  }
  ```



### E [ Argus](https://vjudge.net/contest/447620#problem/E) [UVA 1203](https://vjudge.net/problem/UVA-1203/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  typedef struct _item {
      int ID, period, time;
      bool operator < (const _item &a) const {
          return time > a.time || (time == a.time && ID > a.ID);
      }
  } item;
  
  int main() {
      int time;
      priority_queue<item> pq;
      item task;
      string str;
      vector<int> v;
      while(cin >> str && str != "#") {
          cin >> task.ID >> task.period;
          task.time = task.period;
          pq.push(task);
      }
      cin >> time;
      while(time--) {
          task = pq.top();
          pq.pop();
          cout << task.ID << endl;
          task.time += task.period;
          pq.push(task);
      }
      return 0;
  }
  ```

### F [ I Can Guess the Data Structure!](https://vjudge.net/contest/447620#problem/F) [UVA 11995](https://vjudge.net/problem/UVA-11995/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  int main() {
      int n, command, num;
      while(cin >> n) {
          stack<int> s;
          queue<int> q;
          priority_queue<int> pq;
          bool stack = true, queue = true, priority = true;
          while(n--) {
              cin >> command >> num;
              if(command == 1) {
                  if(stack) s.push(num);
                  if(queue) q.push(num);
                  if(priority) pq.push(num);
              }
              if(command == 2) {
                  if(stack) {
                      if(!s.empty() && s.top() == num) s.pop();
                      else stack = false;
                  }
                  if(queue) {
                      if(!q.empty()  && q.front() == num) q.pop();
                      else queue = false;
                  }
                  if(priority) {
                      if(!pq.empty() && pq.top() == num) pq.pop();
                      else priority = false;
                  }
              }
          }
          int count = 0;
          if(stack) count++;
          if(queue) count++;
          if(priority) count++;
          if(count > 1) cout << "not sure" << endl;
          else if(stack) cout << "stack" << endl;
          else if(queue) cout << "queue" << endl;
          else if(priority) cout << "priority queue" << endl;
          else cout << "impossible" << endl;
      }
      return 0;
  }
  ```

### G [ Ubiquitous Religions](https://vjudge.net/contest/447620#problem/G) [UVA 10583](https://vjudge.net/problem/UVA-10583/origin)

- Code

  ```C++
  #include <iostream>
  #include <cstdio>
  #include <cstdlib>
  #include <vector>
  using namespace std;
  
  int findRootGroup(vector<int> &groups, int x) {
      if(x == groups[x]) {
          return x;
      }
  
      return groups[x] = findRootGroup(groups, groups[x]);
  }
  
  bool unionGroups(vector<int> &groups, int x, int y) {
      int rootX = findRootGroup(groups, x);
      int rootY = findRootGroup(groups, y);
  
      if(rootX == rootY) {
          return false;
      }
  
      groups[rootX] = groups[rootY];
      return true;
  }
  
  int main() {
      int caseNumber = 1;
      int n, m;
      while(scanf("%d%d", &n, &m) != EOF &&
              n != 0 && m != 0) {
          vector<int> groups(n + 1, 0);
          for(int i = 1 ; i <= n ; ++i) {
              groups[i] = i;
          }
  
          int groupCount = n;
          for(int religionCase = 0 ; religionCase < m ; ++religionCase) {
              int i, j;
              scanf("%d%d", &i, &j);
  
              if(unionGroups(groups, i, j)) --groupCount;
          }
  
          printf("Case %d: %d\n", caseNumber++, groupCount);
      }
  
      return 0;
  }
  ```

### H [ Almost Union-Find](https://vjudge.net/contest/447620#problem/H) [UVA 11987](https://vjudge.net/problem/UVA-11987/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  long long n, m, k, pa[100000], sum[100000], cnt[100000], id[100000];
  int find(int x) {
      return x == pa[x] ? x : pa[x] = find(pa[x]);
  }
  void remove(int x) {
      int u = find(id[x]);
      sum[u] -= x;
      cnt[u]--;
      id[x] = ++m;
      pa[m] = m;
      sum[m] = x;
      cnt[m] = 1;
  }
  void unionn(int x, int y) {
      int u = find(id[x]), v = find(id[y]);
      pa[u] = v;
      sum[v] += sum[u];
      cnt[v] += cnt[u];
  }
  int main() {
      while(cin >> n >> k) {
          m = n;
          for(int i = 0; i <= n; ++i) {
              pa[i] = id[i] = sum[i] = i;
              cnt[i] = 1;
          }
          for(int a, b, c; k--;) {
              cin >> c;
              if(c == 1) {
                  cin >> a >> b;
                  if(find(id[a]) != find(id[b]))unionn(a, b);
              }
              if(c == 2) {
                  cin >> a >> b;
                  if(find(id[a]) != find(id[b])) {
                      remove(a);
                      unionn(a, b);
                  }
              }
              if(c == 3) {
                  cin >> a;
                  b = find(id[a]);
                  cout << cnt[b] << ' ' << sum[b] << endl;
              }
          }
      }
      return 0;
  }
  ```

### I [ Islands](https://vjudge.net/contest/447620#problem/I) [UVA 1665](https://vjudge.net/problem/UVA-1665/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  typedef struct {
      int height;
      int modified_height;
      int parent;
  } detail;
  int n, m;
  detail arr[1000000];
  void dfs(int index, int root) {
      int next[] = {-m, -1, 1, m};
      if(index < 0 || index >= n * m) return;
      if(arr[index].modified_height == 0) return;
      if(arr[index].parent == root) return;
      if(index == root) arr[index].parent = -1;
      else arr[index].parent = root;
      ++arr[index].modified_height;
      for(int i = 0; i < 4; ++i) dfs(index + next[i], root);
  }
  int main() {
      int Z;
      cin >> Z;
      while(Z--) {
          int T, year;
          cin >> n >> m;
          memset(arr, 0, n * m * sizeof(detail));
          for(int i = 0; i < n * m; ++i) cin >> arr[i].height;
          cin >> T;
          while(T--) {
              cin >> year;
              for(int i = 0; i < n * m; ++i) arr[i].modified_height = ((arr[i].height - year) > 0);
              for(int i = 0; i < n * m; ++i) {
                  if(arr[i].modified_height == 1) {
                      dfs(i, i);
                  }
                  else continue;
              }
              int cnt = 0;
              for(int i = 0; i < n * m; ++i) if(arr[i].parent == -1) cnt++;
              if(T) printf("%d ", cnt);
              else printf("%d\n", cnt);
              for(int i = 0; i < n * m; ++i) arr[i].parent = 0;
          }
      }
      return 0;
  }
  ```

  

### J [ Borrowers](https://vjudge.net/contest/447620#problem/J) [UVA 230](https://vjudge.net/problem/UVA-230/origin)

- Code

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  typedef struct {
      string author;
      int status;
  } books;
  map<string, books> bookMap;
  vector<string> bookSort;
  bool cmp(string a, string b) {
      if(bookMap[a].author != bookMap[b].author) return bookMap[a].author < bookMap[b].author;
      else return a < b;
  }
  int main() {
      string s, name, author, action;
      while(getline(cin, s) && s[0] != 'E') {
          int pst = s.find('"');
          int pend = s.find_last_of('"');
          name = s.substr(pst, pend + 1);
          pst = s.find("by") + 3;
          bookSort.push_back(name);
          bookMap[name].author = s.substr(pst);
          bookMap[name].status = 1;
      }
      sort(bookSort.begin(), bookSort.end(), cmp);
      while(cin >> action && action != "END") {
          cin.ignore();
          if(action == "BORROW") {
              getline(cin, s);
              int pst = s.find('"');
              int pend = s.find_last_of('"');
              name = s.substr(pst, pend + 1);
              bookMap[name].status = 0;
          }
          else if(action == "RETURN") {
              getline(cin, s);
              int pst = s.find('"');
              int pend = s.find_last_of('"');
              name = s.substr(pst, pend + 1);
              bookMap[name].status = -1;
          }
          else if(action == "SHELVE") {
              for(int i = 0; i < bookSort.size(); ++i) {
                  if(bookMap[bookSort[i]].status == -1) {
                      int j;
                      for(j = i - 1; j >= 0; --j)
                          if(bookMap[bookSort[j]].status == 1) break;
                      if(j == -1) cout << "Put " << bookSort[i] << " first" << endl;
                      else cout << "Put " << bookSort[i] << " after " << bookSort[j] << endl;
                      bookMap[bookSort[i]].status = 1;
                  }
              }
              cout << "END" << endl;
          }
      }
      return 0;
  }
  ```

### K [ Database](https://vjudge.net/contest/447620#problem/K) [UVA 1592](https://vjudge.net/problem/UVA-1592/origin)

- Code 

  ```C++
  #include<bits/stdc++.h>
  using namespace std;
  map<string, int> setID;
  int cnt;
  int getIndex(char *c) {
      if(setID.count(c) > 0) return setID[c];
      else {
          setID[c] = cnt;
          cnt++;
      }
      return cnt - 1;
  }
  int main() {
      int n, m;
      char s[1000];
      while(cin >> n >> m) {
          int db[10000][10];
          map<long long, int> dbmap;
          bool find = false;
          setID.clear();
          cnt = 0;
          fgets(s, 80, stdin);
          for(int i = 0; i < n; ++i) {
              fgets(s, 1000, stdin);
              size_t l = strlen(s);
              char *ptr = strtok(s, ",");
              for(int j = 0; ptr != NULL; ++j) {
                  db[i][j] = getIndex(ptr);
                  ptr = strtok(NULL, ",");
              }
          }
          for(int j = 0; j < m; ++j) {
              for(int k = j + 1; k < m; ++k) {
                  dbmap.clear();
                  for(int i = 0; i < n; ++i) {
                      long long col = (long long)db[i][j] * 1000000 + db[i][k];
                      if(dbmap.count(col) == 0) {
                          dbmap[col] = i;
                      }
                      else {
                          find = true;
                          cout << "NO" << endl;
                          cout << dbmap[col] + 1 << " " << i + 1 << endl;
                          cout << j + 1 << " " << k + 1 << endl;
                          k = m, j = m, i = n;
                      }
                  }
              }
          }
          if(!find) cout << "YES" << endl;
      }
      return 0;
  }
  ```

  
