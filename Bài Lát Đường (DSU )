Bài Lát Đường
ở vùng đất có n thành phố và ban đầu không có đường giữa chúng. Tuy nhiên
mỗi ngày một con đường mới sẽ được xây dựng và sẽ có tổng cộng m con đường.
Một cụm thành phố là một nhóm các thành phố trong đó có một tuyến đường giữa hai thành
phố bất kỳ bằng cách sử dụng các con đường. Sau mỗi ngày, nhiệm vụ của bạn là tìm ra
số lượng cụm thành phố và kích thước của cụm thành phố lớn nhất.

Dòng đầu tiên có hai số nguyên n và m. số thành phố và con đường
Sau đó m dòng miêu tả các con đường mới. Mỗi dòng là a và b
một con đường được xây dựng từ tp a đến tp b.
Bạn có thể cho rằng mọi con đường sẽ được xây dựng giữa hai thành phố khác nhau

In m dòng. Thông tin cần thiết sau mỗi ngày

Input    OutPut
 5 3      4 2
 1 2      3 3
 1 3      2 3
 4 5

#include <bits/stdc++.h>
using namespace std;

int n, m, max_city = 1;
int parent[100005], sz[100005];

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
	max_city = max({max_city,sz[u],sz[v]});
	return true;
}

int main(){
	cin >> n >> m;
	init(); // khoi tao DSU
	int cnt = n;
	for (int i = 0; i < m; i++){
		int x, y; cin >> x >> y;
		if (Union(x,y)){
			--cnt;
		}
		cout << cnt << " " << max_city << endl;
	}
}
