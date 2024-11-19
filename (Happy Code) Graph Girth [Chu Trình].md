Link: https://cses.fi/problemset/task/1707

# Bài toán: Chu vi ngắn nhất của đồ thị (Girth)

## Đề bài
Cho một đồ thị vô hướng, nhiệm vụ của bạn là xác định **chu vi ngắn nhất** của đồ thị (girth), tức là độ dài chu trình ngắn nhất trong đồ thị.

### **Dữ liệu vào**
- Dòng đầu tiên chứa hai số nguyên `n` và `m`: số lượng đỉnh và cạnh trong đồ thị. Các đỉnh được đánh số từ `1, 2, ..., n`.
- `m` dòng tiếp theo, mỗi dòng chứa hai số nguyên `a` và `b`: biểu diễn một cạnh giữa hai đỉnh `a` và `b`.
- Giả sử rằng giữa hai đỉnh bất kỳ có không quá một cạnh.

### **Dữ liệu ra**
- In ra một số nguyên:
  - **Chu vi của đồ thị** (độ dài chu trình ngắn nhất).
  - Nếu đồ thị không có chu trình nào, in ra `-1`.

### **Ràng buộc**
- \(1 \leq n \leq 2500\)
- \(1 \leq m \leq 5000\)

## Ví dụ
### **Dữ liệu vào**


Example
Input:
5 6
1 2
1 3
2 4
2 5
3 4
4 5

Output:
3

int tmp = 1e9, n, m;
vector<int> adj[MAXN];
vector<bool> visited(MAXN, false);
vector<int> dis(MAXN, 1e9);
vector<int> parent(MAXN, -1);
 
void inp(){
    cin >> n >> m;
    for (int i = 0 ; i < m; i++){
        int x, y; cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
}
 
int BFS(int u){
    visited.assign(n, false);
    dis.assign(n, 1e9);
    parent.assign(n, -1);
    int ans = 1e9;
    visited[u] = true;
    dis[u] = 0;
    queue<int> q;
    q.push(u);
    while (!q.empty()){
        int father_node = q.front(); q.pop();
        for (int x : adj[father_node]){
            int son_node = x;
            if (!visited[son_node]){
                visited[son_node] = true;
                dis[son_node] = dis[father_node] + 1;
                q.push(son_node);
                parent[son_node] = father_node;
            }
            else if (son_node != parent[father_node]){
                int value = dis[son_node] + dis[father_node] + 1;
                if (value == 2) continue; 
                ans = min(ans, value);
            }
        }
    }
    return ans;
}
 
int main(){
    inp();
    for (int i = 1; i <= n; i++){
        tmp = min(tmp, BFS(i));
    }
    if (tmp == 1e9) cout << -1;
    else cout << tmp;
}
