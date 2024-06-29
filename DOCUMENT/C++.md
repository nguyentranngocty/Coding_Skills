# C++
## Một số thư viện thường dùng
- Thư viện tổng import 1 lần là được thường dùng trong lập trình thi đấu : `#include <bits/stdc++.h>`
- Các thư viện khác :
```cpp 
#include <iostream>
#include <algorithm>
#include <iomanip>
#include <cmath>
#include <cstdio>
#include <utility>
#include <vector>
#include <set>
#include <map>
#include <string>
#include <sstream>
#include <ctype.h>
#include <stdlib.h>
#include <climits>

```
## Chương trình C++
``` cpp
#include <bits/stdc++.h> 
using namespace std; //các toán tử được định nghĩa trong namespace
using ll = long long;

int main(){
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
	ios::sync_with_stdio(false); 
	cin.tie(nullptr); cout.tie(nullptr);	
}
```
## File
```cpp
fstream f;
ifstream in;
ofstream out;
in.open("input.txt");
in.open("D:/CNTT/Code/C++/SOURCE/input.txt");
out.output("output.txt");
if(in.is_open()){
    code
}
in.close();
out.close();
```
## Con trỏ

- Con trỏ b quản lý biến a :
    - `int a = 6;`
    - `int *b = &a;` 
- Gán giá trị khác cho a qua con trỏ :
    - `*b = 100;  //(a = 100)`
- In ra giá trị biến a :
    - `cout << a;`
    - `cout << *b;` 
- In ra địa chỉ biến a :
    - `cout << &a;`
    - `cout << b;`
- Cấp phát động, con trỏ quản lý mảng và mảng các con trỏ :
```cpp
int a[10000000] // mảng tĩnh => vùng nhớ stack 1e6 phần tử liên tiếp bị tràn
int *a = new int[100000000] //mảng động => vùng nhớ heap 1e6 phần tử ko liên tiếp và ko bị tràn 
int *c = NULL;
int d[100];
c = d = &d[0];
d[1] == *(c + 1);
//mảng con trỏ (con trỏ cấp 2)
int **a = new int*[1000000]
//di chuyển ô nhớ
int *ptr = NULL;
++ptr;
ptr -= 2;
//giải phóng con trỏ và mảng quản lý con trỏ
delete a;
delete[] a;
```
## Hàm
- Nạp chồng hàm -> tên hàm có thế giống nhau nhưng kiểu trả về khác nhau 
```cpp
void Tinh_tong(){
}
long long Ting_tong(){
}
```
- Truyền giá trị mặc định tham số vào hàm -> truyền vào phần tử cuối bên phải nếu chỉ truyền 1 tham số || truyền hết cho n tham số
```cpp
int check(int a, int b /*Tham số hình thức*/){
    return a;
}

int main(){
    int x = 5, y = 10; //Tham số chính thức
    check(x, y); // lời gọi hàm 
}
```
## Typedef và define
- typedef <kiểu dữ liệu> <tên>;
- #define <tên> <kiểu dữ liệu/cấu trúc/câu lệnh> (nhiều ứng dụng hơn)
- **C++ 11 trở lên** có thể dùng **using**
```cpp
typedef long long ll;
#define ll long long
#define FOR(a, b, i) for(int i = a, i < b; i++)
using ll = long long;
```
## Mảng 1 chiều
- Các hàm có sẵn
    - Tìm phần tử lớn nhất : `*max_element(a, a + n)`
    - Tìm phần tử nhỏ nhất : `*min_element(a, a + n)`
    - Hàm max, min của C++ :
        - `max(a, b)`
        - `min({a, b, ...})`
    - Hàm memset(tên_mảng, giá trị (0, -1), sizeof(tên_mảng)) 
        - `memset(a, 0, sizeof(a));`
        - `memset(b, false, sizeof(b));`
- Cài đặt :
```cpp
int a[1000006], n;

void input(){
    cin >> n;
    for(int i = 0; i < n; i++) cin >> a[i];
}
void output(){
    for(int i = 0; i < n; i++) cout << a[i] << ' '; 
}

int find(int val){
    for(int i = 0; i < n; i++){
        if(a[i] == val) return i;
    }
    return -1;
}

void insert(int pos, int val){
    if(pos >= 1e6) return;
    for(int i = n - 1; i >= pos; i--){
        a[i + 1] = a[i];
    }
    a[pos] = val;
    n++;
}

void erase(int val){
    int pos = find(val);
    if(pos == -1) return;
    for(int i = pos + 1; i < n; i++){
        a[i - 1] = a[i];
    }
    n--;
}

int sz(){
    return n;
}
```
## Mảng 2 chiều
- Duyệt ô liền kề -> dùng 2 mảng hoặc 1 pair để lưu lượng thay đổi khi di chuyển sang các ô ở cột và hàng khác nhau
    - move[4] -> duyệt 4 ô xung quanh (chung cạnh)
    ```cpp
    int dx[4] = {-1, 0, 0, 1};
    int dy[4] = {0, -1, 1, 0};
    pair<int, int> move4[4] = {{-1, 0}, {0, -1}, {1, 0}, {0, 1}};
    ```
    - move[8] -> duyệt 8 ô xung quanh (chung đỉnh)
    ```cpp
    int dx[8] = {-1, -1, -1, 0, 0, 1, 1, 1};
    int dy[8] = {-1, 0, 1, -1, 1, -1, 0, 1};
    pair<int, int> move8[8] = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
    ```
    - knightmove[8] -> duyệt 8 ô là nước đi của con mã
    ```cpp
    int dx[8] = {-2, -2, -1, -1, +1, +1, +2, +2};
    int dy[8] = {-1, +1, -2, +2, -2, +2, -1, +1};
    pair<int, int> knigntMove[8] = {{-2, -1}, {-2, 1}, {-1, -2}, {-1, 2}, {1, -2}, {1, 2}, {2, -1}, {2, 1}};
    ```
- Cài đặt và ứng dụng :
```cpp
ll res[1000][1000];
int n, m, p;

int main(){
    //Nhập mảng 2 chiều
    cin >> m >> n >> p;
    int a[n][p], b[p][m], sum[n][m], dif[n][m];
    ll product[n][m];
    for(int i = 0; i < n; i++){
        for(int j = 0; j < p; j++){
            cin >> a[i][j];
        }
    }

    for(int i = 0; i < p; i++){
        for(int j = 0; j < m; j++){
            cin >> b[i][j];
        }
    }

    //Cộng 2 ma trận
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            sum[i][j] = a[i][j] + b[i][j]; 
        }
    }

    //Hiệu 2 ma trận
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            dif[i][j] = a[i][j] - b[i][j]; 
        }
    }

    //Nhân 2 ma trận
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            product[i][j] = 0;
            for(int k = 0; k < p; k++){
                product[i][j] += 1ll * a[i][k] * b[k][j];
            }
        }
    }

    //Xuất ma trận
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            cout << sum[i][j] << ' ';
        }
        cout << endl;
    }
    cout << endl;

    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            cout << dif[i][j] << ' ';
        }
        cout << endl;
    }
    cout << endl;

    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            cout << product[i][j] << ' ';
        }
        cout << endl;
    }
    cout << endl;

    //Giá trị min và max với vị trí của chúng trong mảng 2 chiều
    int max_val = INT_MIN; 
    int min_val = INT_MAX;
    
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            max_val = max(a[i][j], max_val);
            min_val = min(a[i][j], min_val);
        }
    }
    cout << min_val << endl;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            if(min_val == a[i][j]) cout << i + 1 << " " << j + 1 << endl;
        }
    }
    cout << max_val << endl;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < m; j++){
            if(max_val == a[i][j]) cout << i + 1 << " " << j + 1 << endl;
        }
    }
}
```
# STL
## iterator
- Các hàm :
    - `v.begin()` : phần tử đầu
    - `v.rbegin()` : phần tử cuối
    - `v.end()` : sau phần tử cuối
    - `v.rend()` : trước phần tử đầu
- Dùng iterator để duyệt set, map, vector, pair
``` cpp
for(int i = 0; i < vi.size(); i++) cin >> v[i] ;
for(int &x : vi) cin >> x;
for(int i = 0; i < vi.size(); i++) cout << v[i] ;
for(int x : vi) cout << x;
for(vector<int>::iterator it = vi.begin(); it ≠ vi.end(); it++) cout << *it;
vector<int>::iterator it = auto it  //auto thay cho mọi kiểu dữ liệu
vi.begin() + x = a[x];
[x; y) = (begin() + x, begin() + y);
[x; y] = (begin() + x, begin() + y + 1);
```
## pair
- Khai báo : pair<kiểu_dữ_liệu, kiểu_dữ_liệu>; 
    - `pair<int, int> pi;`   
    - `pair<pair<bool, char>, string> pi2;` 
- Nhập và xuất pair :
``` cpp
cin >> a. first >> a.second  // pi = {100, 200} = make_pair(100, 200);
for(int i = 0; i < n; i++){
    cin >> a[i].first >> a[i].second; 
    cout << a[i].first << a[i].second;
}
```
## vector
- Khai báo và nhập : 
```cpp
vector<int> vi; 
vector <pi> vii; 

for(int i = 0; i < n; i++) {
    int temp; cin >> temp; 
    vi.push_back(temp);
}
// khai báo vector có n pt như mảng
const n = 1e6;
vector<int> a(n); 
for(int i = 0; i < n; i++){
    cin >> a[i]; // hoặc dùng push_back() vẫn đc 
}
// gán giá trị sẵn cho vector 
vector<kiểu dữ liệu> a(n, giá trị); // n pt có giá trị bằng giá trị gán
vector<int> a(n, 6);
```
- Các hàm :
    - `vi.push_back()` : thêm vào sau vector và truy cập phần tử như mảng
    - `vi.size()` : cho biết số lượng phần tử vector
    - `vi.pop_back()` : xóa phần tử ở cuối vector
    - `vi.erase(vị trí)` : O(n) xóa phần tử thông qua iterator `vi.erase(vi.begin() + x)`  
    - `vi.insert(vị trí, giá trị)` : thêm phần tử vào vị trí nào đó `vi.insert(vi.begin() + x, k)`
    - `vi.clear()` : xóa toàn bộ phần tử trong vector `vi.clear();` : `vi.size() = 0`
- Ứng dụng :
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int mark[1000001] = {0};

int main(){
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    ios::sync_with_stdio(false); 
    cin.tie(nullptr); cout.tie(nullptr);

    //In các phần tử khác nhau theo thứ tự xuất hiện
    //Code trâu
    int n; cin >> n;
    int a[n];
    for(int &x : a) cin >> x;
    for(int i = 0; i < n; i++){
        bool check = true;
        for(int j = 0; j < i; j++){
            if(a[i] == a[j]){
                check = false;
                break;
            }
        }
        if(check) cout << a[i] << ' ';
    }
    cout << endl;

    //Đếm phân phối -> nhanh
    for(int i = 0; i < n; i++){
        if(mark[a[i]] == 0){
            cout << a[i] << " ";
            mark[a[i]] = 1;
        }
    }
    cout << endl;

    //Trộn 2 mảng đã sx vào 1 mảng + tìm giao và hợp giữa 2 mảng
    int m, n; cin >> m >> n;
    int c[m], d[n];
    vector<int> v;
    for(int &x : c) cin >> x;
    for(int &x : d) cin >> x;
    int i = 0, j = 0;
    vector<int> giao, hop;
    while(i < m && j < n){
        if(c[i] == d[j]){
            v.push_back(c[i]);
            hop.push_back(c[i]);
            giao.push_back(c[i]);
            i++; j++;
        }
        else if(c[i] > d[j]){
            v.push_back(d[j]);
            hop.push_back(d[j]);
            j++;
        }
        else{
            v.push_back(c[i]);
            hop.push_back(c[i]);
            i++;
        }
    }
    while(i < m) v.push_back(c[i++]); hop.push_back(c[i++]);
    while(j < n) v.push_back(d[j++]); hop.push_back(d[j++]);

    for(int i = 0; i < v.size(); i++){
        cout << v[i] << ' ';
    }
    for(int i = 0; i < hop.size(); i++){
        cout << hop[i] << ' ';
    }
    for(int i = 0; i < giao.size(); i++){
        cout << giao[i] << ' ';
    }
}
```
## set
### set
- Khai báo : set<kiểu_dữ_liêu> tên_biến  `set<int> se`
- Các hàm :
    - `se.insert(giá trị)` : O(logN) thêm phần tử vào set  `se.insert(3)`
    - `se.size()` : O(1) số lượng phần tử trong set
    - `se.find(x)`: O(logN) tìm phần tử trong set trả về iterator trỏ tới phần tử trong set
        - `auto it = se.find(3);`
        - `vector<int>::iterator it = se.find(3);`
    - `se.count(x)` : O(logN) đếm số pt xuất hiện trong set cho ra giá trị là 0 hoặc 1
    - `se.erase(x)` : O(logN) xóa pt trong set
### multiset
- Khai báo : multiset<kiểu_dữ_liệu> tên_biến `multiset<long long> se;`
- Các hàm khác giống set trừ hàm find :
    `se.find(x)` : trả về iterator của phần tử đầu tiên nếu các phần tử trùng nhau
### unordered_set
- Khai báo : unordered_set<kiểu_dữ_liệu> tên_biến `unordered_set<string> se;` 
- Các hàm giống set **TUY NHIÊN các hàm find(), count(), erase() ⇒ độ phức tạp có thể  O(1) đến O(n)**
## map
### map
- Khai báo : map<kiểu dữ liệu, kiểu dữ liệu> tên_biến `map<int, int> mp;`
- Truy xuất phần tử : mp[key]  `mp[5];`
- Duyệt map :
    - **for each** : `for(pair<KDL, KDL> x : mp){ cout << x.first << x.second)` 
    - **iterator** : tương tự như set, vector NHƯNG chú ý (*it).first
    - Có thể thay `(*it).first = it → first`
- Các hàm :
    - `mp.insert({x, y})` : thêm 1 cặp phần tử `mp.insert({1, 5}) == map[1] = 5;`
    - `mp[key] = value` có thể thay đổi giá trị của key đã cho trước
    - `mp[key]++` : tăng giá trị của value có trước lên 1 còn nếu chưa có key với value trong map thì tự động thêm vào và cho mp[key] = 1
    - `mp.size()` : số lượng cặp pt
    - `mp.find(x)` : O(logN) tìm key có nằm trong map hay không và trả về iterator như vector hoặc set
    - `mp.count(x)` : O(logN) đếm xem key trong map xuất hiện bao nhiêu lần
    - `mp.erase(x)` : O(logN)  xóa cả key và value và xóa thông qua key
### multimap
- Giống map
- **KO HỖ TRỢ mp[key] = value**  không truy cập và gán
### unordered_map 
- Giống map
- Ứng dụng hash_table : Truy xuất O(1)
### Ứng dụng map 
``` cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

int main(){
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    ios::sync_with_stdio(false); 
    cin.tie(nullptr); cout.tie(nullptr);

    //Đếm tần suất xuất hiện của các ptu trong mảng
    //Đếm theo thứ tự tăng dần
    map<ll, int> mp;
    int n; cin >> n;
    ll a[n];
    for(int i = 0; i < n; i++){
        cin >> a[i];
        mp[a[i]]++;
    }
    //Duyệt bình thường bằng iterator
    for(auto it = mp.begin(); it != mp.end(); it++){
        cout << (*it).first << " " << (*it).second << endl;
    }
    //Duyệt bằng for each
    // bản thân it là 1 pair trong map rồi chứ ko phải iterator nữa nên ko cần (*it) -> trỏ đến 1 pair trong map nữa rồi mới (*it).first
    for(auto it : mp){
	    cout << it.first << ' ' << it.second << endl;
    }

    //Đếm theo thứ tự xuất hiện của mảng
    map<ll, int> mp;
    int n; cin >> n;
    ll a[n];
    for(int i = 0; i < n; i++){
        cin >> a[i];
        mp[a[i]]++;
    }
    for(int i = 0; i < n; i++){
        if(mp[a[i]] != 0){
            cout << a[i] << ' ' << mp[a[i]] << endl;
            mp[a[i]] = 0;
        }
    }
}
```
## string
- Khai báo : string tên_biến `string s = ”Noi dung”` : trong dấu ngoặc kép lưu 1 chuỗi kí tự
- Nhập :
    - `cin >> s` : xâu không có dấu cách `s = "Python";`
    - `getline(cin, s, <có thể thêm>)` : xâu có dấu cách
    - `cin.ignore()` : xóa dấu cách của cin trước khi dùng getline
- Các hàm : 
    - `s.size()` hoặc `s.length()` : trả số lượng kí tự trong xâu s
    - `s.front() == s[0]` : kí tự đầu tiên
    - `s.back() == s[s.size() - 1]` → kí tự cuối cùng
    - `s.compare(t)` nếu s == t thì 0; nếu s > t thì 1; nếu s < t thì -1;
    - **+** : concate nối 2 xâu lại và cũng có thể nối xâu với kí tự
    - `isdigit(char c)` : kiểm tra chữ số
    - `islower(char c)` : kiểm tra chữ in thường
    - `isupper(char c)` : kiểm tra in hoa
    - `isalpha(char c)` : kiểm tra chữ cái
    - `int tolower(char c)` : chuyển thành chữ in thường mã ASCII ép kiểu char
    - `int toupper(char c)` : chuyển thành chữ in hoa mã ASCII ép kiểu char ta thường dùng `s[i] = toupper(s[i])` : gán lại cho s[i]
    - `stoi (string to integer)` : đổi string sang số int `int t = stoi(s);`
    - `stoll (string to ll)` : chuyển string sang long long `ll a = stoll(s);`
    - `to_string()` : đổi số sang string `string s = to_string(t);`
    - `stringstream ss(s)` : dùng để tách các xâu có nhiều dấu cách hoặc xâu con có các kí tự phân biệt
        ```cpp
        string s = "hoc lap trinh   Python";
        string tmp;
        stringstream ss(s);
        while(ss >> tmp){
            //code
        }
- Ứng dụng :
```cpp
//Chuyển đổi chuỗi sang full in hoa
void toUpper(string &s){
    for(int i = 0; i < n; i++){
        s[i] = toupper(s[i]);
    }
}

//Chuyển đổi chuỗi sang full in thường
void toLower(string &s){
    for(int i = 0; i < n; i++){
        s[i] = tolower(s[i]);
    }
}

//Đối vs các số lớn có nhiều chữ số (>= 10^6 chữ số) lưu vào string
void solve(string s){
		cin >> s;
		int sum = 0;
		for(char x : s){
				sum += (int) x; // sai vì nó sẽ cộng mã ASCII của x vào sum chứ ko phải số cần tính
				sum += x - '0'; //Lấy mã ASCII của char x trừ đi mã ASCII 0 sẽ ra số tách ra từ xâu
		}
		cout << sum;
}

//Chuẩn hóa ngày tháng năm sinh theo form dd/mm/yyyy => ứng dụng để viết comparator so sánh tuổi theo thứ tự từ điển
void chuanHoa(string &s){
	if(s[2] != '/') s = "0" + s;
	if(s[5] != '/') s.insert(3, "0");
}

    //Đếm kí tự xuất hiện trong xâu bằng map<char, int>
    string s; getline(cin, s);
    map<char, int> mp;
    for(char x : s){
        mp[x]++;
    }
    for(auto it : mp){
        if(it.first == ' ') cout << '_' << ' '<< it.second << endl;
        else cout << it.first << " " << it.second << endl;
    }

    //Đếm kí tự xuất hiện trong xâu bằng mảng -> nhanh hơn
    string s; getline(cin, s);
    int dem[256] = {0};
    for(char x : s){
        dem[x]++;
    }
    //chỉ duyệt 0 - 255 hoặc bé hơn 256 nếu dùng <= 256 sẽ sai ngay
    for(int i = 0; i < 255; i++){
        if(dem[i] != 0) cout << (char)i << ' ' << dem[i] << endl;
    }
    
    //Tách chuỗi nhỏ trong xâu -> áp dụng tách số vẫn được nhưng phải convert qua
    string s; getline(cin, s);
    stringstream ss(s); //khởi tạo stringstream tách chuỗi trong xâu
    string word;
    vector<string> vi;
    //while(getline(ss, word, ts3)) ts3 : là kí hiệu sẽ ngắt luồng cin
    while(ss >> word){ // luồn nhập liên tục cứ tới dấu cách là ngưng
        vi.push_back(word);
    }
    //có thể làm bất cứ thứ gì với vector<string>
    sort(vi.begin(), vi.end());
    
```        
