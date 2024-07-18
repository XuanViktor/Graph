Có n thành phố và m chuyến bay. Nhiệm vụ của bạn là kiểm tra xem bạn có thể đi từ bất kỳ thành phố nào đến bất kỳ thành phố nào khác bằng các chuyến bay có sẵn.

### Đầu vào
- Dòng đầu tiên chứa hai số nguyên n và m: số lượng thành phố và số lượng chuyến bay. Các thành phố được đánh số từ 1 đến n.
 Tiếp theo, có m dòng mô tả các chuyến bay. Mỗi dòng có hai số nguyên a và b: có một chuyến bay từ thành phố a đến thành phố b. Tất cả các chuyến bay đều là chuyến bay một chiều.

### Đầu ra
- In ra "YES" nếu tất cả các tuyến đường là có thể đi được, và "NO" nếu không. Trong trường hợp "NO", cũng in ra hai thành phố a và b sao cho bạn không thể đi từ thành phố a đến thành phố b. Nếu có nhiều giải pháp có thể, bạn có thể in ra bất kỳ giải pháp nào.

### Ràng buộc
- 1 ≤ n ≤ 100,000
- 1 ≤ m ≤ 200,000
- 1 ≤ a, b ≤ n

### Ví dụ
### Đầu vào:
4 5

1 2

2 3

3 1

1 4

3 4

### Đầu ra:
NO

4 2

```cpp
int n, m;
vector<int> adj[100005], T_adj[100005];
bool visited[100005];
stack<int> st;
 
void inp(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x,y; cin >> x >> y;
        adj[x].push_back(y);
        T_adj[y].push_back(x);
    }
}
 
void dfs1(int u){
    visited[u] = true;
    for (int v : adj[u]){
        if (!visited[v]){
            dfs1(v);
        }
    }
    st.push(u);
}
 
void dfs2(int u){
    visited[u] = true;
    for (int v : T_adj[u]){
        if (!visited[v]){
            dfs2(v);
        }
    }
}
 
void Kosaraju(){
    // B1 goi dfs1 va luu vao stack
    for (int i = 1; i <= n; i++){
        if (!visited[i]){
            dfs1(i);
        }
    }
 
    // B3 pop tung dinh trong stack va dfs2
    int cnt = 0;
    vector<int> a;
    memset(visited, false, sizeof(visited));
    while (!st.empty()){
        int u = st.top(); st.pop();
        if (!visited[u]){
            ++cnt;
            a.push_back(u);
            dfs2(u);
        }
    }
    if (cnt == 1) cout << "YES";
    else {
        cout << "NO" << endl;
        cout << a[1] << " " << a[0];
    }
}
 
int main(){
    faster;
    inp();
    Kosaraju();
}
```
