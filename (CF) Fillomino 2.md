Fillomino là một trò chơi logic cổ điển. Trong một lớp học tại thị trấn Yunqi, một số tình nguyện viên đang chơi một biến thể của trò chơi này trên bàn cờ:

Xem xét một bàn cờ kích thước n×n. Các hàng của bàn cờ được đánh số từ 1 đến 𝑛 từ trên xuống dưới. Các cột được đánh số từ 1 đến n từ trái sang phải. Ô nằm ở giao điểm của hàng thứ x và cột thứ 
y được ký hiệu là (x, y). Đường chéo chính của bàn cờ là các ô (x, x) với 1 ≤ 𝑥 ≤ 𝑛. 
Một hoán vị của {1, 2, 3, ..., n} được viết trên đường chéo chính của bàn cờ. Chính sách là có đúng một số được viết trên mỗi ô của các ô dưới và trên đường chéo chính (có chính xác 1+2+…+n ô như vậy) thành n khu vực kết nối thỏa mãn các ràng buộc sau:

Mỗi khu vực phải kết nối. Điều này có nghĩa là chúng ta có thể di chuyển từ bất kỳ ô nào của khu vực này đến bất kỳ ô nào khác của cùng khu vực chỉ đi qua các ô của cùng khu vực và di chuyển từ ô này đến ô kế cận.
Khu vực thứ x phải chứa ô trên đường chéo chính có số x với 1 ≤ x ≤ n.
Số lượng ô thuộc về khu vực thứ x phải bằng x với 1 ≤ x ≤ n.
Mỗi ô dưới và trên đường chéo chính chỉ thuộc về một khu vực duy nhất.

### Đầu vào:
- Dòng đầu tiên chứa một số nguyên n (1 ≤ n ≤ 500) đại diện cho kích thước của bàn cờ.
- Dòng thứ hai chứa n số nguyên p1, p2, ..., pn. Số pi là số được viết trên ô (i, i). Đảm bảo rằng mỗi số nguyên từ tập hợp {1, ..., n} xuất hiện đúng một lần trong p1, ..., pn.

### Đầu ra:
- Nếu không tồn tại cách phân chia thỏa mãn, in ra -1.
- Ngược lại, in ra n dòng. Dòng thứ i nên chứa i số. Số thứ j trên dòng thứ i là x nếu ô (i, j) thuộc về khu vực có x ô.

### Input
5

3 1 4 5 2

### Output
3

3 1

3 3 2

4 4 4 5

```cpp
#define f0(i,n) for (int i = 0; i < n; i++)
#define f1(i,n) for (int i = 1; i <= n; i++)
 
int n, d;
vector<vector<int>> a;
 
void dfs(int u, int v, int x){
    if (d > x) return;
    a[u][v] = x;
    if (v - 1 > 0 && a[u][v-1] == 0) d++, dfs(u,v-1,x);
    if (u + 1 <= n && a[u+1][v] == 0) d++, dfs(u+1,v,x);
}
 
int main() {
    cin >> n;
    a.resize(n + 1, vector<int>(n + 1, 0)); // Khởi tạo ma trận với giá trị 0
    f1(i,n){
        int x; cin >> x;
        d = 1;
        dfs(i,i,x);
    }
 
    f1(i,n){
        f1(j,i){
            cout << a[i][j] << " ";
        }
        cout << endl;
    }
}
```
