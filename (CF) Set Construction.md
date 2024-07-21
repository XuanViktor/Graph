Bạn có một ma trận nhị phân b có kích thước n x n. Ma trận này chứa các giá trị 0 và 1. Nhiệm vụ của bạn là xây dựng n tập hợp A1,A2,...,An sao cho các điều kiện sau đây được thỏa mãn

- 1. Mỗi tập hợp là không rỗng và bao gồm các số nguyên khác nhau từ 1 đến n
  - Ví dụ: Tập hợp có thể là {1, 2, 3} hoặc {1} nhưng không thể là {} (rỗng).

- 2. Tất cả các tập hợp phải khác nhau.
  - Ví dụ: Không thể có hai tập hợp giống hệt nhau.

- 3. Mối quan hệ giữa các tập hợp phải phản ánh ma trận nhị phân.
  - Đối với mọi cặp chỉ số (i,j)
    - Nếu b[i][j] = 1 thì tập hợp Ai, phải là tập con thực sự của tập hợp Ạ. Nghĩa là tất cả các phần tử của Ai đều nằm trong Ạ, Nhưng Ai không bằng Ạ
    - Nếu b[i][j] = 0 thì Ai không phải là tâp con thực sự của Aj

### Đầu Vào
- Dòng 1 gồm t test
- Dòng 2 gồm n là kích thước của ma trận
- Dòng 3 là kích thước của ma trận n x n

### Đầu ra 
- Giá trị đầu tiên in kích thước của tập Ai còn lại in theo giá trị thỏa mãn điều kiện của các tập 

Input
2

4

0001

1001

0001

0000

3

011

001

000


Output
3 1 2 3

2 1 3

2 2 4

4 1 2 3 4

1 1

2 1 2

3 1 2 3


### Giải thích
- Tập hợp 𝐴1 phải là tập con thực sự của Tập hợp A 4 và không phải là tập con của các tập hợp khác.
- Tập hợp A2 phải là con thực sự của Tập hợp A4 và cũng là tập con thực sự của Tập hợp A1
- Tập hợp A3 phải là con thực sự của tập A4
- các tập hợp có thể được chọn như sau
 - A1 = {1, 2} 
 - A2 = {2} 
 - A3 = {3} 
 - A4 = {1, 2, 3, 4} 

```cpp
int n;
vector<int> adj[maxn]; 
 
void clearAdj() {
    for (int i = 1; i <= n; i++) {
        adj[i].clear();
    }
}
 
void input() {
    cin >> n;
    clearAdj(); 
 
    for (int i = 1; i <= n; i++) {
        adj[i].push_back(i);
        string row; cin >> row; 
        for (int j = 1; j <= n; j++) {
            if (row[j - 1] == '1') { 
                adj[j].push_back(i);
            }
        }
    }
}
 
int main() {
    FileIO();
    int t;  cin >> t;
    while (t--) {
        input();
        for (int i = 1; i <= n; i++) {
            cout << adj[i].size() << " ";
            for (int x : adj[i]) {
                cout << x << " ";
            }
            cout << endl;
        }
    }
    return 0;
}
```
