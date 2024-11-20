### Đề bài
Chúng ta có một đồ thị vô hướng với **N** đỉnh và **0** cạnh. Xử lý lần lượt **Q** truy vấn sau:

- **t<sub>i</sub> = 0 u<sub>i</sub> v<sub>i</sub>:** Thêm một cạnh **(u, v)**.
- **t<sub>i</sub> = 1 u<sub>i</sub> v<sub>i</sub>:** Nếu các đỉnh **u** và **v** được kết nối, in ra **1**. Ngược lại, in ra **0**.

### Ràng buộc
- 1 <= N <= 200000  
- 1 <= Q <= 200000  
- 0 <= u<sub>i</sub>, v<sub>i</sub> < N

![image](https://github.com/user-attachments/assets/f97f0f5b-6215-4cfa-be6d-24376af63e57)

```c++
#include <bits/stdc++.h>
using namespace std;

int n, m, w;
int parent[10000005], sz[10000005];

void init(){
    for(int i = 1; i <= n; i++){
        parent[i] = i; // khoi tao cac dinh i co id la i
        sz[i] = 1; // kich thuoc tung dinh la 1
    }
}

int Find(int u){
    if(u == parent[u]) return u;
    else return parent[u] = Find(parent[u]);
}

bool Union(int u, int v){
    u = Find(u); 
    v = Find(v);
    if(u == v) return false; // neu u == v chung to do thi la chu trinh
    if(sz[u] < sz[v]){ // dung de luc nao cung cho u lon hon v cho de xu ly
        swap(u, v); //u la thang co size lon hon
    }
    sz[u] += sz[v]; // them tp v vao tp u ghi gop
    parent[v] = u; // va gan lai cho thang co parent be la u cho v
    return true;
}

int main(){
    cin >> n >> m;
    init(); // khoi tao DSU
    for (int i = 0; i < m; i++){
        int w, x, y; cin >> w >> x >> y;
        if (w == 0){
            Union(x,y);
        }
        else {
            if (Find(x) == Find(y)) {
                cout << 1 << endl;
            } else {
                cout << 0 << endl;
            }
        }
    }
}
```
