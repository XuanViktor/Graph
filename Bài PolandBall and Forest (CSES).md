PolandBall sống trong một khu rừng cùng với gia đình của mình. Trong khu rừng này, có một số cây. Một cây là một đồ thị không có chu trình, có k đỉnh và k-1 cạnh, nơi k là một số nguyên.

Mỗi đỉnh của cây là nơi sinh sống của một thành viên trong gia đình, và mỗi thành viên có một ID duy nhất từ 1 đến n. Đối với mỗi Ball i, chúng ta biết ID của người thân xa nhất sống trên cùng một cây. Nếu có nhiều người thân xa nhất, chúng ta chỉ lấy ID nhỏ nhất trong số đó.

Nhiệm vụ của bạn là xác định số lượng cây trong khu rừng dựa trên thông tin đầu vào.

### Đầu vào:
- Dòng đầu tiên chứa số nguyên n (1 ≤ n ≤ 10^4) — số lượng Balls sống trong khu rừng.
- Dòng thứ hai chứa dãy p1, p2, ..., pn với độ dài n, trong đó (1 ≤ pi ≤ n). pi biểu thị ID của người thân xa nhất từ Ball i sống trên cùng một cây. Nếu có nhiều người thân xa nhất, pi là ID nhỏ nhất.
### Đầu ra:
- In ra một số nguyên: số lượng cây trong khu rừng.

### Ví dụ:
- Đầu vào:
5
2 1 5 3 3

- Đầu ra:
2

```cpp
int n;
vector<int> adj[100004];
bool visited[100004];

void input(){
    cin >> n;
    for (int i = 1; i <= n; i++){
        int x; cin >> x;
        adj[i].push_back(x);
        adj[x].push_back(i);
    }
    memset(visited,false,sizeof(visited));
}

void dfs(int u){
    visited[u] = true;
    for (int v : adj[u]){
        if (!visited[v]){
            dfs(v);
        }
    }
}

int main(){
    FileIO();
    input();
    int cnt = 0;
    for (int i = 1; i <= n; i++){
        if (!visited[i]){
            dfs(i);
            ++cnt;
        }
    }
    cout << cnt;
}
```

