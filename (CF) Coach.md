Huấn luyện viên lập trình có n sinh viên để giảng dạy. Chúng ta biết rằng n chia hết cho 3. Giả sử rằng tất cả các sinh viên đều được đánh số từ 1 đến n, bao gồm cả.
Trước khi diễn ra giải vô địch lập trình của trường đại học, huấn luyện viên muốn chia tất cả các sinh viên thành các nhóm ba người. Đối với một số cặp sinh viên, chúng ta biết rằng họ muốn ở cùng một đội. Hơn nữa, nếu sinh viên thứ i muốn ở cùng đội với sinh viên thứ j, thì sinh viên thứ j cũng muốn ở cùng đội với sinh viên thứ i. Huấn luyện viên muốn các đội đạt kết quả tốt, vì vậy ông ấy muốn điều kiện sau đây được thỏa mãn: nếu sinh viên thứ i muốn ở cùng đội với sinh viên thứ j, thì sinh viên thứ i và sinh viên thứ j phải ở cùng một đội. Ngoài ra, rõ ràng là mỗi sinh viên phải chỉ ở một đội duy nhất.
Hãy giúp huấn luyện viên và chia các đội theo cách ông ấy mong muốn.

![image](https://github.com/user-attachments/assets/d62f0d01-52c2-4048-b21e-9965203958c4)


### Đầu vào
- Dòng đầu tiên chứa các số nguyên n và m (3 <= n <= 48)
- Tiếp theo là m dòng, mỗi dòng chứa một cặp số nguyên ai,bi (1 <= ai < bi <= n) - cặp ai,bi có nghĩa là các sinh viên có số ai và bi muốn ở cùng một đội
- Đảo bảo rằng n chia hết cho 3. 

### Đầu ra
- Nếu việc phân chia thành các đội theo yêu cầu không tồn tại, in ra số -1. 
- Ngược lại in ra n/3 dòng. Trong mỗi dòng in ra ba số nguyên xi,yi,zi (1 <= xi,yi,zi <= n) - đội thứ i
- Nếu có nhiều câu trả lời bạn có thể in ra bất kỳ câu nào trong số đó

### Input
3 3

1 2

2 3

1 3

### Output
3 2 1

```cpp
int n, m, visited[maxn];
vector<int> adj[maxn];
 
void inp() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        int x, y; cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
}
 
void dfs(int u, vector<int>& comp) {
    visited[u] = true;
    comp.push_back(u);
    for (int v : adj[u]) {
        if (!visited[v]) {
            dfs(v, comp);
        }
    }
}
 
int main() {
 
    inp();
    vector<vector<int>> comps;
    for (int i = 1; i <= n; i++) {
        if (!visited[i]) {
            vector<int> comp;
            dfs(i, comp);
            comps.push_back(comp);
        }
    }
 
    vector<vector<int>> result;
    vector<int> singles, pairs;
 
    for (auto comp : comps) {
        if (comp.size() > 3) {
            cout << "-1\n";
            return 0;
        } else if (comp.size() == 3) {
            result.push_back(comp);
        } else if (comp.size() == 2) {
            pairs.push_back(comp[0]);
            pairs.push_back(comp[1]);
        } else {
            singles.push_back(comp[0]);
        }
    }
 
    while (!pairs.empty() && !singles.empty()) {
        vector<int> team;
        team.push_back(pairs.back()); pairs.pop_back();
        team.push_back(pairs.back()); pairs.pop_back();
        team.push_back(singles.back()); singles.pop_back();
        result.push_back(team);
    }
 
    while (singles.size() >= 3) {
        vector<int> team;
        team.push_back(singles.back()); singles.pop_back();
        team.push_back(singles.back()); singles.pop_back();
        team.push_back(singles.back()); singles.pop_back();
        result.push_back(team);
    }
 
    if (!pairs.empty() || !singles.empty()) {
        cout << "-1\n";
        return 0;
    }
 
    for (auto team : result) {
        for (int student : team) {
            cout << student << " ";
        }
        cout << "\n";
    }
 
    return 0;
}
```
