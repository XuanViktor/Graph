Ông Kitayuta mới vừa mua một đồ thị vô hướng bao gồm n đỉnh và m cạnh. Các đỉnh của đồ thị được đánh số từ 1 đến n. Mỗi cạnh, gọi là cạnh i, có một màu ci, nối đỉnh ai và bi.

Ông Kitayuta muốn bạn xử lý các truy vấn sau đây.

Trong truy vấn thứ i, ông đưa cho bạn hai số nguyên — ui và vi.

Hãy tìm số lượng màu sắc mà các cạnh của màu đó kết nối đỉnh ui và đỉnh vi, trực tiếp hoặc gián tiếp.

### Đầu vào
- Dòng đầu tiên của đầu vào chứa hai số nguyên cách nhau bằng khoảng trắng — n và m (2 ≤ n ≤ 100, 1 ≤ m ≤ 100), đại diện cho số lượng đỉnh và số lượng cạnh của đồ thị.

- M dòng tiếp theo chứa ba số nguyên cách nhau bằng khoảng trắng — ai, bi (1 ≤ ai < bi ≤ n) và ci (1 ≤ ci ≤ m). Lưu ý rằng có thể có nhiều cạnh giữa hai đỉnh. Tuy nhiên, không có nhiều cạnh cùng màu giữa hai đỉnh, tức là, nếu i ≠ j, thì (ai, bi, ci) ≠ (aj, bj, cj).

- Dòng tiếp theo chứa một số nguyên — q (1 ≤ q ≤ 100), đại diện cho số lượng truy vấn.

- Sau đó là q dòng, mỗi dòng chứa hai số nguyên cách nhau bằng khoảng trắng — ui và vi (1 ≤ ui, vi ≤ n). Đảm bảo rằng ui ≠ vi.

### Đầu ra
- Đối với mỗi truy vấn, in kết quả trên một dòng riêng biệt.
![image](https://github.com/user-attachments/assets/b166bb66-b3ec-4aca-ad5e-129e132576ae)
![image](https://github.com/user-attachments/assets/8b9d5def-ff0b-4842-8a13-504c0fbbd18e)


### Giải thích
- Đỉnh 1 và đỉnh 2 được nối với nhau bằng màu 1 và 2.

- Đỉnh 3 và đỉnh 4 được nối với nhau bằng màu 3.

- Đỉnh 1 và đỉnh 4 không được nối với nhau bằng bất kỳ màu sắc nào.

```cpp
int n, m;
vector<pair<int, int>> adj[MAXN]; // store (neighbor, color)
bool visited[MAXN];
int color_count[MAXN];
 
void input() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        int x, y, c;
        cin >> x >> y >> c;
        adj[x].emplace_back(y, c);
        adj[y].emplace_back(x, c);
    }
}
 
void dfs(int u, int target, int color) {
    visited[u] = true;
    for (auto &[v, c] : adj[u]) {
        if (!visited[v] && c == color) {
            if (v == target) {
                color_count[color]++;
                return;
            }
            dfs(v, target, color);
        }
    }
}
 
int main() {
    FileIO();
 
    input();
    int q;
    cin >> q;
    while (q--) {
        int u, v;
        cin >> u >> v;
        memset(color_count, 0, sizeof(color_count)); // reset color count for each query
        for (int color = 1; color <= m; color++) {
            memset(visited, false, sizeof(visited)); // reset visited for each color
            dfs(u, v, color);
        }
        int result = 0;
        for (int i = 1; i <= m; i++) {
            if (color_count[i] > 0) {
                result++;
            }
        }
        cout << result << '\n';
    }
    return 0;
}
```
