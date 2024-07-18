A game has n levels and m teleportes between them. You win the game if you move from level 1 to level n using every teleporter exactly once.
Can you win the game, and what is a possible way to do it?
### Input
- The first input line has two integers n and m: the number of levels and teleporters. The levels are numbered 1,2,\dots,n.
- Then, there are m lines describing the teleporters. Each line has two integers a and b: there is a teleporter from level a to level b.
- You can assume that each pair (a,b) in the input is distinct.
### Output
- Print m+1 integers: the sequence in which you visit the levels during the game. You can print any valid solution.
- If there are no solutions, print "IMPOSSIBLE".

### Constraints

- $(2 \leq n \leq 10^5)$
- $(1 \leq m \leq 2.10^5)$
- $(1 \leq a,b \leq n)$

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
