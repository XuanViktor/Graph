# Nhiệm vụ

Bạn cần thực hiện việc giao thư đến cư dân trong một thành phố. Vì lý do này, bạn cần tìm một hành trình mà điểm bắt đầu và kết thúc đều ở bưu điện, đồng thời đi qua **mỗi con đường chính xác một lần**.

---

## Dữ liệu vào

1. Dòng đầu tiên chứa hai số nguyên `n` và `m`:  
   - `n`: số lượng ngã tư (đỉnh).  
   - `m`: số lượng con đường (cạnh).

2. Các ngã tư được đánh số từ `1, 2, ..., n`, và bưu điện nằm tại ngã tư số `1`.

3. Sau đó có `m` dòng, mỗi dòng chứa hai số nguyên `a` và `b`, biểu thị rằng có một con đường hai chiều giữa ngã tư `a` và `b`.

**Lưu ý**:
- Mỗi con đường nối giữa hai ngã tư khác nhau.
- Không có hai con đường trùng nhau nối cùng một cặp ngã tư.

---

## Dữ liệu ra

1. Nếu có giải pháp, in ra tất cả các ngã tư trên hành trình theo thứ tự bạn sẽ đi qua.  
2. Nếu không có giải pháp, in ra **`IMPOSSIBLE`**.

---

## Yêu cầu của bài toán

- Hành trình phải là **chu trình Euler**:
  - Đi qua **mỗi cạnh đúng một lần**.
  - Điểm bắt đầu và kết thúc phải là **đỉnh 1**.

---

## Ví dụ

### Dữ liệu vào 1

### Example
### Input:
6 8

1 2

1 3

2 3

2 4

2 6

3 5

3 6

4 5

### Output:
1 2 6 3 2 4 5 3 1

Link: https://cses.fi/problemset/task/1691/

```cpp
#include <bits/stdc++.h>
using namespace std;
 
#define ll long long
#define mod 1000000007
#define faster ios::sync_with_stdio(false); cin.tie(nullptr); cout.tie(nullptr);
 
const int MAXN = 1005;
 
void FileIO(){
    #ifndef ONLINE_JUDGE
    freopen("In.txt", "r", stdin);
    freopen("Out.txt", "w", stdout);
    #endif 
    faster;
}
 
int n,m;
set<int> adj[1000001];
int degree[1000001];
int start;
 
void input(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x, y; cin >> x >> y;
        adj[x].insert(y);
        adj[y].insert(x);
        degree[x]++;
        degree[y]++;
    }
}
 
void euler(){
    // kiểm tra các đỉnh đều bật chẵn
    int start_v;
    for (int i = 1; i <= n; i++){
        if (degree[i] % 2 == 1){
            cout << "IMPOSSIBLE";
            return;
        }
        else{
            start_v = 1;
        }
    }
    stack<int> st;
    vector<int> euler_cycle;
    st.push(start_v);
    while (!st.empty()){
        int x = st.top();
        if (!adj[x].empty()){
            int y = *adj[x].begin();
            st.push(y);
 
            // delete
            adj[x].erase(y);
            adj[y].erase(x);
        }
        else{
            st.pop();
            euler_cycle.push_back(x);
        }
    }
 
    // Nếu các đỉnh có bậc lớn hơn 0 trong đồ thị không nằm cùng một TPLT 
    // thì không tồn tại đáp án
    if ((int)euler_cycle.size() < m + 1){
        cout << "IMPOSSIBLE";
        return;
    }
    reverse(begin(euler_cycle), end(euler_cycle));
    for (int x : euler_cycle) cout << x << " ";
}
 
int main() {
    //FileIO();
    faster;
    input();
    euler();
}
