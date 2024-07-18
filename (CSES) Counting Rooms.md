Bạn được cung cấp một bản đồ của một tòa nhà, và nhiệm vụ của bạn là đếm số lượng phòng của nó. Kích thước của bản đồ là n x m ô vuông, và mỗi ô vuông có thể là sàn hoặc tường. Bạn có thể đi sang trái, phải, lên và xuống qua các ô sàn.

### Đầu vào
- Dòng đầu tiên chứa hai số nguyên n và m: chiều cao và chiều rộng của bản đồ.
- Sau đó, có n dòng mỗi dòng chứa m ký tự mô tả bản đồ. Mỗi ký tự có thể là . (sàn) hoặc # (tường).

### Đầu ra
- In ra một số nguyên: số lượng phòng.

### Ràng buộc
- 1 ≤ n, m ≤ 1000
  
### Ví dụ
### Đầu vào:
5 8

########

#..#...#

####.#.#

#..#...#

########

### Đầu ra:
3

## Cách 1
```cpp
int n,m; 
char a[1001][1001];
 
void inp(){
    cin >> n >> m;
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= m; j++){
            cin >> a[i][j];
        }
    }
}
 
void dfs(int x, int y) {
    if (x < 1 || y < 1 || x > n || y > m || a[x][y] == '#') return;
 
    a[x][y] = '#'; // visited
    for (int i = 0; i < 4; i++) {
        int newX = x + move0[i].first;
        int newY = y + move0[i].second;
        dfs(newX, newY);
    }
}
 
int main(){
    FileIO();
    inp();
    int cnt = 0;
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= m; j++){
            if (a[i][j] == '.'){
                ++cnt;
                dfs(i,j);
            }
        }
    }
    cout << cnt;
}
```
## Cách 2
```cpp
int n,m; 
char a[1001][1001];
 
void inp(){
    cin >> n >> m;
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= m; j++){
            cin >> a[i][j];
        }
    }
}
 
void dfs(int x, int y){
    a[x][y] = '#';
    for (int i = 0; i < 4; i++){
        int i1 = x + move0[i].fi;
        int j1 = y + move0[i].se;
        if (i1 >= 1 && i1 <= n && j1 >= 1 && j1 <= m && a[i1][j1] == '.'){
            dfs(i1,j1);
        }
    }
}
 
int main(){
    FileIO();
    inp();
    int cnt = 0;
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= m; j++){
            if (a[i][j] == '.'){
                ++cnt;
                dfs(i,j);
            }
        }
    }
    cout << cnt;
}
```
