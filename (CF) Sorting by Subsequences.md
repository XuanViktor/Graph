Bạn có một dãy số nguyên khác nhau và cần chia dãy này thành nhiều dãy con nhất có thể sao cho khi sắp xếp từng dãy con theo thứ tự tăng dần, toàn bộ dãy ban đầu cũng được sắp xếp theo thứ tự tăng dần.

### Yêu cầu:
- Chia dãy số ban đầu thành số lượng lớn nhất các dãy con.
- Mỗi phần tử của dãy số phải xuất hiện trong đúng một dãy con.
- Sau khi sắp xếp từng dãy con theo thứ tự tăng dần, toàn bộ dãy số ban đầu cũng phải theo thứ tự tăng dần.

### Đầu vào:
- Số nguyên n - độ dài của dãy số (1 <= n <= 10^5)
- n số nguyên khác nhau a1,a2,...,an (-10^9 <= ai <= 10^9)

### Đầu ra
- In ra số lượng lớn nhất các dãy con k
- In ra k  dòng, mỗi dòng mô tả một dãy con:
	- Số lượng phần tử trong dãy con ci
	- Các chỉ số của các phần tử này trong dãy ban đầu
Các chỉ số có thể in ra theo bất kỳ thứ tự nào, nhưng mỗi chỉ số từ 1 đến n  phải xuất hiện đúng một lần. Nếu có nhiều cách chia, in ra bất kỳ cách nào trong số đó.

### Input
6

3 2 1 6 5 4

### Output
4

2 1 3

1 2

2 4 6

1 5

### Yêu cầu:
Chia dãy số thành số lượng lớn nhất các dãy con sao cho khi sắp xếp từng dãy con theo thứ tự tăng dần, toàn bộ dãy số cũng được sắp xếp theo thứ tự tăng dần.
4 là số lượng dãy con lớn nhất mà ta có thể chia.
Các dãy con sau khi sắp xếp sẽ giúp dãy ban đầu cũng được sắp xếp tăng dần.
#### Kiểm tra lại:
- Dãy số [3,2,1,6,5,4] có thể chia như sau
- [3,1] (chỉ số 1 và 3): Sau khi sắp xếp dãy con này [1,3]
- [2] (chỉ số 2) đã sắp xếp
- [6,4] (chỉ số 4 và 6): Sau khi sắp xếp dãy con này [4,6]
- [5] (chỉ số 5) đã sắp xếp

#### Sắp xếp lại
- [1,2,3,4,5,6]

```cpp
#define f0(i,n) for (int i = 0; i < n; i++)
#define f1(i,n) for (int i = 1; i <= n; i++)
 
ll n, a[maxn], b[maxn], nxt[maxn];
bool vis[maxn] = {0};
 
int main(){
    FileIO();
    cin >> n;
    for (int i = 1; i <= n; i++){
        cin >> a[i];
        b[i] = a[i];
    }
    sort(b+1,b+n+1);
    f1(i,n){
        int j = lower_bound(b+1,b+n+1,a[i]) - b;
        nxt[i] = j;
    }
 
    vector<vector<int>> ans;
    f1(i,n){
        if (vis[i] == 0){
            int u = i;
            vector<int> v;
            while (vis[u] == 0){
                v.push_back(u);
                vis[u] = 1;
                u = nxt[u];
            }
            ans.push_back(v);
        }
    }
    cout << ans.size() << endl;
    for (auto v : ans){
        cout << v.size() << " ";
        for (int x : v){
            cout << x << " ";
        }
        cout << endl;
    }
}
```
