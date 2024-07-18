Bạn được cung cấp một bản đồ của một mê cung, và nhiệm vụ của bạn là tìm một con đường từ điểm bắt đầu đến điểm kết thúc. Bạn có thể đi sang trái, phải, lên và xuống.

### Đầu vào
- Dòng đầu tiên chứa hai số nguyên n và m: chiều cao và chiều rộng của bản đồ.
- Sau đó, có n dòng mỗi dòng chứa m ký tự mô tả mê cung. Mỗi ký tự có thể là . (sàn), # (tường), A (bắt đầu), hoặc B (kết thúc). Có đúng một A và một B trong đầu vào.

### Đầu ra
- Đầu tiên, in ra "YES" nếu có một con đường, và "NO" nếu không có.
- Nếu có một con đường, in ra độ dài của con đường ngắn nhất đó và mô tả của nó dưới dạng một chuỗi gồm các ký tự L (trái), R (phải), U (lên), và D (xuống). Bạn có thể in ra bất kỳ giải pháp hợp lệ nào.

### Ràng buộc
- 1 ≤ n, m ≤ 1000

### Ví dụ
### Đầu vào:
5 8

########

#.A#...#

#.##.#B#

#......#

########

### Đầu ra:
YES

9

LDDRRRRRU

```cpp
int n, m;
char a[1005][1005];
int parent[1005][1005], visited[1005][1005];
string dir = "ULRD";
int xa,ya,xb,yb;
 
void input() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            cin >> a[i][j];
            if (a[i][j] == 'A') xa = i, ya = j;
            if (a[i][j] == 'B') xb = i, yb = j;
               
        }
    }
}
 
void bfs() {
    queue<pair<int,int>> q;
    q.push({xa,ya});
    visited[xa][ya] = 1;
    while (q.size()){
        int x = q.front().fi;
        int y = q.front().se;
        q.pop();
 
        for (int i = 0; i < 4; i++){
            int newx = x + move0[i].fi;
            int newy = y + move0[i].se;
            if (newx >= 1 && newx <= n && newy >= 1 && newy <= m && a[newx][newy] != '#' && !visited[newx][newy]){
                visited[newx][newy] = 1;
                parent[newx][newy] = i;
                q.push({newx,newy});
            }
        }
    }
    if (visited[xb][yb]){
        cout << "YES" << endl;
        string ans;
        while (xb != xa || yb != ya){
            int i = parent[xb][yb];
            ans += dir[i];
            xb -= move0[i].fi;
            yb -= move0[i].se;
        }
        reverse(begin(ans), end(ans));
        cout << ans.size() << endl;
        cout << ans;
    } else {
        cout << "NO";
    }
}
 
int main() {
    FileIO();
    input();
    bfs();
}
```
