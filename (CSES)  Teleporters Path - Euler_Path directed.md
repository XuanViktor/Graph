# Mô tả bài toán

Một trò chơi có **n** cấp độ và **m** cổng dịch chuyển giữa chúng. Bạn sẽ thắng trò chơi nếu bạn di chuyển từ cấp độ **1** đến cấp độ **n** bằng cách sử dụng **mỗi cổng dịch chuyển chính xác một lần**.  

Bạn có thể thắng trò chơi không? Nếu có, hãy tìm một cách để thực hiện điều đó.

---

## Dữ liệu vào

- Dòng đầu tiên chứa hai số nguyên **n** và **m**:  
  - **n**: số lượng cấp độ.  
  - **m**: số lượng cổng dịch chuyển.

- Tiếp theo là **m** dòng, mỗi dòng chứa hai số nguyên **a** và **b**, nghĩa là có một cổng dịch chuyển từ cấp độ **a** đến cấp độ **b**.

**Lưu ý**:
- Mỗi cặp **(a, b)** trong dữ liệu vào là khác nhau.

---

## Dữ liệu ra

- Nếu có cách thắng trò chơi, in ra **m+1** số nguyên: thứ tự các cấp độ mà bạn đi qua trong trò chơi.  
- Nếu không có cách, in ra **`IMPOSSIBLE`**.

---

## Ràng buộc

- \( 2 \leq n \leq 10^5 \)  
- \( 1 \leq m \leq 2 \times 10^5 \)  
- \( 1 \leq a, b \leq n \)  

---

## Ví dụ

### Dữ liệu vào 1


### Example
### Input:
5 6

1 2

1 3

2 4

2 5

3 1

4 2

### Output:

1 3 1 2 4 2 5

```cpp
int n, m;
set<int> adj[1000001];
vector<pair<int, int>> degree; // first ra : second vao
int start;

void input(){
    cin >> n >> m;
    degree.resize(n + 1, {0, 0});

    for (int i = 0; i < m; i++){
        int x, y; 
        cin >> x >> y;
        adj[x].insert(y);
        degree[x].first++;
        degree[y].second++;
    }
}

void euler(){
    // kiểm tra các đỉnh có bán bận ra bằng bán bậc vào
    // vào có 2 đỉnh bán bậc ra - bán bậc vào = 1 và bán bậc vào - bán bậc ra = 1
    int cnt = 0, start_v = 1;
    for (int i = 1; i <= n; i++){
        if (degree[i].first == degree[i].second){
            continue;
        } 
        else{
            if (abs(degree[i].first - degree[i].second) == 1){
                cnt++;
            }
        }
    }
    if (cnt != 2){
        cout << "IMPOSSIBLE";
        return;
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

    // điều kiện phụ của bài toán Teleporters Path 
    // phải có đường đi từ 1 đến n
    if (*(euler_cycle.end() - 1) != n){
        cout << "IMPOSSIBLE";
        return;
    }
    for (int x : euler_cycle) cout << x << " ";
}

int main() {
    //FileIO();
    faster;
    input();
    euler();
    return 0;
}
