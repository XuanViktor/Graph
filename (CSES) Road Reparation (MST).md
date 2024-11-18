## Bài Sửa đường
ở vùng đất có n thành phố và m đường giữa chúng. Thật không may tình trạng của những con đường quá kém nên chúng không thể
sử dụng. Nhiệm vụ của bà là sữa chữa một số con đường để có một con đường tốt giữa hai thành phố bất kì. 
Đối với mỗi con đường biết chi phí sữa chữa của nó và bạn nên tìm giải pháp sao cho tổng chi phí nhỏ nhất.

### Đầu Vào
- Dòng đầu tiêu có hai số nguyên n và m. Số thành phố và đường
- Sau đó m dòng môt tả các con đường. Mỗi dòng gồm 3 só a,b,c và có một con đường giữa tp a và tp b với chi phí là c
- Tất cả các côn đường đều là đường hai chiều. Mọi con đường đều năm giữa 2 tp khác nhau và có nhiều nhất 1 con đường 
giữa 2 tp.

### Đầu Ra
- In một số nguyên: Tổng chi phí sửa chữa tối thiểu. Nếu ko có giải pháp in "IMPOSSIBLE"

### Constraints 
- 1 <=n<= 10^5, 
- 1 <=m<=2.10^^5, 
- 1 <=a,b<= n, 
- 1 <=c<= 10^^9

| INPUT       | OUTPUT |
|-------------|--------|
| 5 6         | 14     |
| 1 2 3       |        |
| 2 3 5       |        |
| 2 4 2       |        |
| 3 4 8       |        |
| 5 1 7       |        |
| 5 4 4       |        |


## Cách 1 dùng Kruskal
```cpp
#include <bits/stdc++.h>
using namespace std;

struct edge{
	int x, y, w;
};

int n, m;
int parent[100005], sz[100005];
vector<edge> dscanh;

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

void nhap(){
	cin >> n >> m;
	for (int i = 0; i < m; i++){
		int x, y, w; cin >> x >> y >> w;
		dscanh.push_back((edge){x,y,w});
	}
}

void Kruskal(){
	// Buoc 1: sap xep dscanh theo trong so tang dan
	sort(begin(dscanh), end(dscanh), [](edge a, edge b)->bool{
		return a.w < b.w;	
	});
	// Buoc 2: Lap
	long long sum_weight = 0;
	vector<edge> MST; // luu cay khung cuc tieu
	for (int i = 0; i < m; i++){
		if (MST.size() == n-1) break; // dk cua cay khung co n - 1 canha
		edge e = dscanh[i]; // lay tung canh theo thu tu tang dan
		if (Union(e.x, e.y)){ // Neu 2 canh ghep duoc va khong tao thanh chu trinh
			MST.push_back(e);
			sum_weight += e.w;
		}
	}
	if (MST.size() < n - 1) cout << "IMPOSSIBLE\n";
	else {
		for (auto i : MST){
            		cout << i.x << " " << i.y << " " << i.w << endl; 
        	}
		cout << sum_weight << endl;
	}
}

int main(){
	nhap();
	init(); // khoi tao DSU
	Kruskal();
}
```

## Cách 2 Dùng Prim
```cpp
#include <bits/stdc++.h>
using namespace std;
 
struct canh{
    int x, y, w;
};
 
 
int n,m;
bool v[100001];
vector<pair<int,int>> adj[100001];
int parent[1000001], d[1000001];
 
void nhap(){
    cin >> n >> m;
    for (int i = 0; i < m; i++){
        int x,y,w; cin >> x >> y >> w;
        adj[x].push_back({y,w});
        adj[y].push_back({x,w});
    }
    memset(v,false,sizeof(v));
    for (int i = 1; i <= n; i++) d[i] = INT_MAX;
}
 
void Prim(int u){
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> Q;
    vector<canh> MST;
    ll res = 0;
    Q.push({0,u});
    int cnt  = 0;
    while (!Q.empty()){
        pair<int,int> top = Q.top(); Q.pop();
        int dinh = top.second, trongso = top.first;
        if (v[dinh]) continue;
        res += trongso;
        v[dinh] = true;
        if (u != dinh){
            MST.push_back({dinh, parent[dinh], trongso});
            ++cnt;
        }
        // duyet tat cac cac dinh ke
        for (auto it : adj[dinh]){
            int y = it.first, w = it.second;
            if (!v[y] && w < d[y]){
                Q.push({w,y});
                d[y] = w;
                parent[y] = dinh;
            }
        }
    }
    if (cnt == n - 1){
        cout << res << endl;
        // for (auto it : MST){
        //     cout << it.x << " " << it.y << " " << it.w << endl;
        // }
    }
    else cout << "IMPOSSIBLE";
}
 
int main(){
    faster;
    nhap();
    Prim(1);
}
```
