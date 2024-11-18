Bob quyết định đi dạo trong một công viên được biểu diễn như một đồ thị liên thông với n đỉnh và m cạnh hai chiều. Ban đầu, Bob ở đỉnh 1 và ghi lại đỉnh này. Anh có thể đi từ đỉnh này đến đỉnh khác qua các cạnh hai chiều. Mỗi khi anh ghé thăm một đỉnh chưa được ghi lại, anh sẽ ghi lại nó. Sau khi thăm hết tất cả các đỉnh, anh sẽ dừng lại.
Bob muốn biết dãy số nhỏ nhất theo thứ tự từ điển mà anh có thể ghi lại khi đi dạo. Bạn cần tìm và xuất dãy số này.
### Đầu Vào
Dòng đầu chứa hai số nguyên n  và m (số đỉnh và cạnh).
m dòng tiếp theo, mỗi dòng chứa hai số nguyên ui và vi ( các đỉnh mà cạnh thứ i kết nối)

### Đầu Ra
Xuất một dòng chứa dãy số nhỏ nhất theo thứ tự từ điển mà Bob có thể ghi lại

### Ví dụ
### Input
5 5

1 4

3 4

5 4

3 2

1 5

### Output
1 4 3 2 5
- Trong ví dụ, Bob có thể đi từ 1 đến 4, rồi 3,2 quay lại 3 sau đó 4 rồi quay lại 1 và cuối cùng đến 5 vậy dãy số có từ điển nhỏ nhất là {1,4,3,2,5}

```cpp
#define f0(i,n) for (int i = 0; i < n; i++)
#define f1(i,n) for (int i = 1; i <= n; i++)
 
int n,m, vis[maxn];
vector<int> a[maxn];
 
void inp(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x, y; cin >> x >> y;
        a[x].pb(y);
        a[y].pb(x);
    }
}
 
void bfs(int u){
    priority_queue<int,vector<int>,greater<int>> q;
    vis[u] = 1;
    q.push(1);
    while (!q.empty()){
        int u = q.top(); q.pop();
        cout << u << " ";
        for (int v : a[u]){
            if (!vis[v]){
                vis[v] = 1;
                q.push(v);
            }
        }
    }
 
}
 
int main(){
    FileIO();
    inp();
    bfs(1);
}
```
