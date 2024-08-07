Your task is to deliver mail to the inhabitants of a city. For this reason, you want to find a route whose starting and ending point are the post office, and that goes through every street exactly once.

### Input
- The first input line has two integers n and m: the number of crossings and streets. The crossings are numbered 1,\,2,\ldots,\,n, and the post office is located at crossing 1.
- After that, there are m lines describing the streets. Each line has two integers a and b: there is a street between crossings a and b. All streets are two-way streets.
- Every street is between two different crossings, and there is at most one street between two crossings.

### Output
- Print all the crossings on the route in the order you will visit them. You can print any valid solution.
- If there are no solutions, print "IMPOSSIBLE".

### Constraints
- $(2\leq n\leq 10^5)$
- $(1\leq m\leq 2.10^5)$
- $(1\leq a,\,b\leq n)$

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
