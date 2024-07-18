## Building Teams
Có n học sinh trong lớp của Uolevi và m tình bạn giữa họ. Nhiệm vụ của bạn là chia các học sinh thành hai đội sao cho không có hai học sinh nào trong cùng một đội là bạn bè. Bạn có thể tự do chọn kích thước của các đội.

### Đầu vào
- Dòng đầu tiên chứa hai số nguyên n và m: số lượng học sinh và số lượng tình bạn. Các học sinh được đánh số từ 1, 2, ..., n.
- Sau đó, có m dòng mô tả các tình bạn. Mỗi dòng chứa hai số nguyên a và b: học sinh a và b là bạn bè.
- Mỗi tình bạn là giữa hai học sinh khác nhau. Bạn có thể giả định rằng có nhiều nhất một tình bạn giữa bất kỳ hai học sinh nào.

### Đầu ra
- In ra một ví dụ về cách xây dựng các đội. Đối với mỗi học sinh, in ra "1" hoặc "2" tùy thuộc vào đội mà học sinh đó sẽ được phân vào. Bạn có thể in ra bất kỳ đội hợp lệ nào.
- Nếu không có giải pháp nào, in ra "IMPOSSIBLE".

### Ràng buộc
- 1 ≤ n ≤ 10^5
- 1 ≤ m ≤ 2 ⋅ 10^5
- 1 ≤ a, b ≤ n
### Ví dụ
### Đầu vào:
5 3
1 2
1 3
4 5

### Đầu ra
1 2 2 1 2

## Cách 1
```cpp
vector<int> adj[MAXN];
int color[MAXN];
int n,m, flag = 1;
 
void input(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x,y; cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    for (int i = 1; i <= n; i++){
        sort(begin(adj[i]), end(adj[i]));
    }
}
 
// 1 : RED, 2 : BLUE
bool bfs(int u){
    queue<int> q;
    q.push(u);
    color[u] = 1;
    while (!q.empty()){
        int v = q.front(); q.pop();
        for (int x : adj[v]){
            if (color[x] == 0){
                color[x] = 3 - color[v];
                q.push(x);
            }
            else if (color[x] == color[v]) return false;
        }
    }
    return true;
}
 
int main(){
    FileIO();
    input();
 
    bool ok = true;
    for (int i = 1; i <= n; i++){
        if (color[i] == 0){
            if (!bfs(i)){
                ok = false; break;
            }
        }
    }
    if (ok){
        for (int i = 1; i <= n; i++){
            cout << color[i] << " ";
        }
    } else cout << "IMPOSSIBLE";
```
## Cách 2
```cpp
vector<int> adj[MAXN];
int color[MAXN];
int n,m, flag = 1;
 
void input(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x,y; cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    for (int i = 1; i <= n; i++){
        sort(begin(adj[i]), end(adj[i]));
    }
}
 
void dfs(int u){ 
    for (int v : adj[u]){
        if (color[v] == 0){
            color[v] = 3 - color[u];
            dfs(v);
        }
        else if (color[v] == color[u]){
            flag = 0;
            return;
        }
    }
}
int main(){
    FileIO();
    input();
 
    for (int i = 1; i <= n; i++){
        if (!color[i]){
            color[i] = 1;
            dfs(i);
        }
    }
    if (flag) {
        for (int i = 1; i <= n; i++){
            cout << color[i] << " ";
        }
    }
    else cout << "IMPOSSIBLE";
}
```
