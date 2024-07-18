Byteland has n cities, and m roads between them. The goal is to construct new roads so that there is a route between any two cities.
Your task is to find out the minimum number of roads required, and also determine which roads should be built.
### Input
- The first input line has two integers n and m: the number of cities and roads. The cities are numbered 1,2,\dots,n.
- After that, there are m lines describing the roads. Each line has two integers a and b: there is a road between those cities.
- A road always connects two different cities, and there is at most one road between any two cities.
### Output
- First print an integer k: the number of required roads.
- Then, print k lines that describe the new roads. You can print any valid solution.

### Constraints
- $(1 \leq n \leq 10^5)$
- $(1  \leq m  \leq 2.10^5)$
- $(1 \leq a,b \leq n)$

### Example
- Input:
4 2
1 2
3 4

- Output:
1
2 3

Link: https://cses.fi/problemset/result/7404616/

```cpp
#include <bits/stdc++.h>
using namespace std;
 
 
// Kiểm tra đồ thị không có chu trình
// Kiểm tra đồ thị có n - 1 cạnh
// Thỏa 2 ý trên là cây
 
int n,m,cnt = 0;
vector<int> adj[100005];
bool visited[100005];
int parent[100005];
 
void input(){
    cin >> n >> m;
    for (int i = 1; i <= m; i++){
        int x,y; cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
}
 
void dfs(int u){
    visited[u] = true;
    for (int v : adj[u]){
        if (!visited[v]){
            dfs(v);
        }
    }
}
 
int main (){
    input();
 
    vector<int> path;
    for (int i = 1; i <= n; i++){
        if (!visited[i]) {
            path.push_back(i);
            ++cnt;
            dfs(i);
        }
    }
    cout << cnt - 1 << endl;
    for (int i = 1; i < (int)path.size(); i++){
        cout << path[i-1] << ' ' << path[i] << endl;
    }
```
