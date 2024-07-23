Ngày xửa ngày xưa, có một người đàn ông đến biển. Biển lúc đó bão tố và đen tối. Người đàn ông bắt đầu gọi nàng tiên cá nhỏ xuất hiện nhưng than ôi, ông ta chỉ đánh thức Cthulhu...
Trong khi đó, ở đầu kia của thế giới, Lầu Năm Góc đang tích cực thu thập thông tin cố gắng dự đoán hành vi của con quái vật và chuẩn bị vũ khí siêu bí mật. Do hoạt động địa chấn cao và điều kiện thời tiết xấu, các vệ tinh vẫn chưa thể chụp được ảnh rõ nét của con quái vật. Phân tích bức ảnh đầu tiên dẫn đến một đồ thị vô hướng với n đỉnh và m cạnh. Giờ đây, những bộ óc thông minh nhất thế giới đang chuẩn bị xác định liệu đồ thị này có thể được coi là Cthulhu hay không.
Để đơn giản hóa, giả sử rằng Cthulhu trông giống như một vật thể hình cầu với các xúc tu gắn vào. Về mặt hình thức, chúng ta sẽ coi là Cthulhu một đồ thị vô hướng có thể được biểu diễn như một tập hợp gồm ba hoặc nhiều cây gốc, các gốc của chúng được kết nối bằng một chu trình đơn giản.
Đảm bảo rằng đồ thị không chứa các cạnh kép và vòng lặp tự thân.
![image](https://github.com/user-attachments/assets/fd72f934-531f-4799-887e-c1f53391c9d1)


### Đầu vào
- Dòng đầu tiên chứa hai số nguyên - số đỉnh n và số cạnh m của đồ thị (1 ≤ n ≤ 100, 0 ≤ m ≤ n*(n-1)/2 )
- Mỗi dòng trong m dòng tiếp theo chứa một cặp số nguyên x và y, cho thấy rằng có một cạnh tồn tại giữa các đỉnh x và y (1 ≤ x, y ≤ n, x ≠ y). Đối với mỗi cặp đỉnh sẽ chỉ có nhiều nhất một cạnh giữa chúng, không có cạnh nào kết nối một đỉnh với chính nó.

### Đầu ra
- In "NO" nếu đồ thị không phải là Cthulhu và "FHTAGN!" nếu đúng.

### Input
6 6

6 3

6 4

5 1

2 5

1 4

5 4

### Output
- FHTAGN!

```cpp
int n,m, visited[maxn], parent[maxn];
vector<int> adj[maxn];
int cnt1 = 0, cnt2 = 0;
 
void inp(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x, y; cin >> x >> y;
        adj[x].pb(y);
        adj[y].pb(x);
    }
}
 
void dfs(int u){
    ++cnt2;
    visited[u] = true;
    for (int v : adj[u]){
        if (!visited[v]){
            dfs(v);
        }
    }
    ++cnt1;
}
 
int main(){
    FileIO();
    inp();
 
    dfs(1);
    if (n == m && cnt1 >= 3 && cnt2 == n){
        cout << "FHTAGN!";
    } else {
        cout << "NO";
    }
}
```
