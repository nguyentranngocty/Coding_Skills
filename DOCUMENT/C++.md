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
- Nạp chồng hàm : tên hàm có thế giống nhau nhưng kiểu trả về khác nhau 
```cpp
void Tinh_tong(){
}
long long Ting_tong(){
}
```
- Truyền giá trị mặc định tham số vào hàm : truyền vào phần tử cuối bên phải nếu chỉ truyền 1 tham số || truyền hết cho n tham số
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
## Iterator
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
## Pair
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
## Vector
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
## Set
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
    - `se.find(x)` : trả về iterator của phần tử đầu tiên nếu các phần tử trùng nhau
### unordered_set
- Khai báo : unordered_set<kiểu_dữ_liệu> tên_biến `unordered_set<string> se;` 
- Các hàm giống set **TUY NHIÊN các hàm find(), count(), erase() ⇒ độ phức tạp có thể  O(1) đến O(n)**
## Map
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
## String
- Khai báo : string tên_biến `string s = ”Noi dung”` (trong dấu ngoặc kép lưu 1 chuỗi kí tự)
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
# Hướng đối tượng (OOP)
## Cấp phát tĩnh
- Các cú pháp ban đầu :
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
//Encapsulation
//Class sinh viên
class SinhVien{
private:
    //Property - Attributes - Data field -> thuộc về đối tượng
    string name, date, grade;
    double gpa;
    //Static => khởi tạo giá trị bên ngoài class ko được gán giá trị trong class
    static string schoolName;
public:
    //Constructor (ko có kiểu trả về có tên trùng vs class) -> Khai báo ra đối tượng là sẽ khởi động => Function overloading
    //constructor mặc định => ko xây dựng vẫn tự động có => bắt buộc phải có trước khi tạo constructor đầy đủ tham số + việc khai báo ra có thể can thiệp chỉnh sửa constructor vào lúc nó tự động gọi lên => tránh được những giá trị bất định cho biến
    //Nếu ko có Constructor mặc định thì nếu khai báo ở hàm main biến ko truyền tham số sẽ bị sai => để tạo biến theo nhiều cách thì nên viết hết constructor ra
    SinhVien(){ 
        //Bình thường sẽ trống ko có code
        cout << "Khoi tao SV \n";
    }
    //Constructor đầy đủ tham số => thường được xây dựng để tiện khi khởi tạo biến có thể truyền thẳng giá trị tự bên ngoài => chương trình sẽ gọn hơn ko cần phải gán giá trị lần lượt
    SinhVien(string ten, string ns, string lop, double diem){
        ten = name;
        ns = date;
        lop = grade;
        diem = gpa;
    }
    //Tránh sự nhập nhằng giữa tên biến tham số và tên của thuộc tính => con trỏ this
    SinhVien(string name, string date, double gpa){
        this->name = name;
        this->date = date;
        this->gpa = gpa;
    }
    
    //Method -> Khai báo hàm thôi ko cài đặt
    void input();
    void output();
    
    //Khai báo friend function => giúp cho biến bên ngoài class có thể truy cập vào các Attributes
    friend void printInfo(SinhVien x);
    friend void greetings(SinhVien x);
    
    //Interface (giao thức) => mỗi thuộc tính để truy xuất và sửa đổi thông tin
    //Getter
    string getName(); //Lấy thông tin trong private
    double getGpa();
    //Setter
    void setName(string newName); // Sửa đổi thông tin 

    //overload operator
    //insertion
    friend istream& operator >> (istream &in, SinhVien &other){
        getline(in, other.name);
        in >> other.date >> other.grade >> other.gpa; 
        return in;
    }
    //extraction
    friend ostream& operator << (ostream &out, SinhVien other){
        out << other.name << endl << other.date << endl << other.grade << endl << other.gpa;
        return out;
    }

    //Destructor => kết thúc thì đối tượng sẽ được hủy => ko xây dựng thì vẫn tự xây dựng -> Áp dụng khi cấp phát động để giải phóng vùng nhớ
    //Nếu thuộc tính trong 1 object là 1 con trỏ trong vùng nhớ động => delete con trỏ đó trong hàm destructor VD con trỏ của class khác trong class đc sử dụng thì phải delete trong destructor
    ~SinhVien(){
        //Bth cũng trống ko
        cout << "Huy SV \n";
    }
};

//friend function (Hàm bạn) => giúp cho hàm chứa tham số là đối tượng trong class có thể truy xuất các thuộc tính trong private
void printInfo(SinhVien x){
    cout << x.name << ' ' << x.date << ' ' << x.grade << ' ' << x.gpa << endl;
}
void greetings(SinhVien x){
    cout << x.name << endl;
    cout << x.date << endl;
    cout << x.grade << ' ' << x.gpa << endl;
}

//Static initialize -> toàn bộ các đối tượng trong class sẽ sử dụng school name
string SinhVien::schoolName = "UIT"; 

//Implementation -> cài đặt bên ngoài
void SinhVien::input(){ //Khai báo phạm vi nó thuộc vào lớp SinhVien
    getline(cin, name);
    cin.ignore();
    cin >> date >> grade >> gpa;
}

void SinhVien::output(){
    cout << name << endl;
    cout << date << endl;
    cout << grade << endl;
    cout << gpa << endl;
}

//Getter Setter 
string SinhVien::getName(){
    return name;
}
double SinhVien::getGpa(){
    return gpa;
}
void SinhVien::setName(string newName){
    name = newName;
}

//Class số phức
class soPhuc{ //x = a +bi
private:
    int a, b;
public:
    //Constructor mặc định
    soPhuc(){
    }

    //overload operator
    //Cách 1 ko dùng hàm friend
    soPhuc operator + (soPhuc other){
        soPhuc tong;
        tong.a = this->a + other.a;
        tong.b = this->b + other.b;
        return tong;
    }
    
    bool operator < (soPhuc other){
        return sqrt(this->a * this->a + this->b * this->b) > sqrt(other.a * other.a + other.b * other.b);
    }

    //Cách 2 dùng hàm friend
    friend soPhuc operator - (soPhuc x, soPhuc y){
        soPhuc hieu;
        hieu.a = x.a - y.a;
        hieu.b = x.b - y.b;
        return hieu;
    }

    //insertion
    friend istream& operator >> (istream& in, soPhuc &x){
        in >> x.a >> x.b;
        return in;
    }

    //extraction
    friend ostream& operator << (ostream& out, soPhuc x){
        out << x.a << " " << "+" << " " << x.b << "i";
        return out;
    }

    //Khi nạp chồng toán tử so sánh rồi => sort() ko cần viết cmp mà nó sẽ tự sort theo toán tử nạp chồng
    friend bool operator == (soPhuc x, soPhuc y){
        return x.a == y.a && x.b == y.b;
    }

    friend bool operator > (soPhuc x, soPhuc y){
        return sqrt(x.a * x.a + x.b * x.b) > sqrt(y.a * y.a + y.b * y.b); 
    }
    
    //Friend function
    friend void input(soPhuc &p);
    friend void output(soPhuc p);
};

void input(soPhuc &p){
    cin >> p.a >> p.b;
}
void output(soPhuc p){
    cout << p.a << " " << "+" << " " << p.b << "i";
}

int main(){
    student x{"Nguyen Van A", "Linh Xuan", 9.6};
    cout << x.getName() << ' ' << x.getGpa() << ' ' << x.getAdress() << endl;
}
```
- Đóng gói, Kế thừa và Đa hình :
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
//Inheritance
//Superclass
class person{
protected:
    //Attributes
    string name, address;
public:
    //constructor
    person(){
        //cout << "Constructor lop cha" << endl;
    }
    person(string name, string address){
        this->name = name;
        this->address = address;
    }
    //Getter Setter
    string getName();
    void setName(string newName);
    string getAdress();
    void setAdress(string newAdress);
    void output();
};

//Implementation
string person::getName(){
    return name;
}
void person::setName(string newName){
    this->name = newName;
}
string person::getAdress(){
    return address;
}
void person::setAdress(string newAdress){
    this->address = newAdress;
}
void person::output(){
    cout << name << ' ' << address;
}

//Subclass => ko thể truy cập trực tiếp vào các thuộc tính private của lớp cha
class student : public person{ //kế thừa các pt từ lớp person
//thêm các đặc điểm riêng của lớp con
private:
    double gpa;
public:
    //Constructor
    student(){
        cout << "Constructor lop con" << endl;
    }
    //Constructor => gọi constructor của lớp cha
    student(string name, string address, double gpa) : person(name, address){
        this->name = name;
        this->address = address;
        this->gpa = gpa;
    }
    //implement trong hàm vẫn đc
    double getGpa(){
        return gpa;
    }
    void setGpa(double gpa){
        this->gpa = gpa;
    }
    //các phương thức public lớp con vẫn gọi đc từ lớp cha 
    //có thể in thông tin của sv như tên hay địa chỉ kế thừa của lớp cha qua hàm get nhưng ko thể in qua trực tiếp hàm sau đây
    // void output(){ //error
    //  cout << ten << ' ' << address << ' ' << fixed << setprecision(2) << gpa;
    // }

    //fuction overiding => cùng tên, cùng kiểu trả về, cùng ds tham số
    void output(){
        //gọi hàm output() của lớp cha để in các thuộc tính của lớp cha + ghi đè thêm thông tin lớp con
        person::output();
        cout << fixed << setprecision(2) << gpa;
    }
};

//Polymorphism + multilevel inheritance
class shape{
protected:
    int length, width;
public:
    void setVal(int l, int w){
        length = l;
        width = w;
    }
    //Hàm ảo => đa hình dùng con trỏ lớp cha để gọi hàm của lớp con
    virtual int getArea(){
        return 0;
    }
    virtual int getPerimeter(){
        return 0;
    }
};

class rectangle : public shape{
public:
    int getArea(){
        return length * width; // ko cần get set vì mode protected
    }
};

class square : public rectangle{
public:
    int getArea(){
        rectangle::getArea();
        return length * length;
    }
    int getPerimeter(){
        return length * 4;
    }
};

int main(){
    //Polymorphism => dùng con trỏ lớp cha để gọi các method lớp con
    rectangle a;
    square b;
    shape *ptr1 = &a;
    shape *ptr2 = &b;
    ptr1->setVal(10, 20);
    ptr2->setVal(3, 3);
    cout << a.getArea() << endl;
    cout << ptr2->getPerimeter()<< endl;
}
```
## Cấp phát động 
- Sample 1 :
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

//Base class
class vehicle{
protected:
    //properties
    string modelName;
public:
    //Constructor => cannot Override
    vehicle(){
        cout << "Created a new vehicle" << endl;
    }
    //Constructor with parameters
    vehicle(string name){
        modelName = name;
        cout << "Created a new vehicle named " << name << endl;
    }
    //Getter Setter
    void setModelName(string name){
        modelName = name;
    }
    string getModelName(){
        return modelName;
    }
    //Member function (methods)
    void ready(){
        cout << "A vehicle is ready !" << endl;
    }
    //virrual function => call functions in each sub class from base class + if sub class don't override virtual function of base class => call from base class
    virtual void run(){
        cout << "A vehicle is running ...!" << endl;
    }

    //Destructor => free up memory from dynamic memory allocation -> usually use for pointer as a property in a class
    ~vehicle(){
        cout << "Deleted a vehicle" << endl;
    }
};

//Inheritance => should convert private to protected
//Sub class
class taxi : public vehicle{
protected:
    //specific properties for sub class
    float kmCounter;
public:
    //Constructor => auto find the default Constructor in base class
    taxi(){
        cout << "Created a new taxi" << endl;
    }
    //another way to access to Constructor with parameters without default Constructor in base class  
    car() : vehicle("Ford"){
        cout << "Created a car" << endl;
    }
    //Constructor with parameters in sub class => auto find default constructor in base class
    //Constructor with parameters => orient to Constructor with parameters in base class
    taxi(string name) : vehicle(name){
        cout << "Created a new taxi named " << name << endl;
    }

    //Overriding
    void run(){
        vehicle::run(); // call a function in base class and improve or define again
        cout << "It's a taxi !" << endl;
    }
    //Getter Setter
    void setKmCounter(float km);
    //Abstraction => Showing fuction names without implementation them 
    float calculateFee(); 
    void print();

    //Destructor
    ~taxi(){
        cout << "Deleted a taxi" << endl;
    }
};
//Implementation
void taxi::setKmCounter(float km){
    kmCounter = km;
}
float taxi::calculateFee(){
    return kmCounter * 100000;
}
void taxi::print(){
    cout << kmCounter << "km" << endl << fixed << setprecision(0) << this->calculateFee() << endl;
}

//multilevel inheritance
class car : public vehicle{
protected:
    string ownerName;
public:
    car(){
        cout << "Created a new car" << endl;
        ownerName = "None";
    }
    string getOwnerName(){
        return ownerName;
    }
    void setOwnerName(string name){
        ownerName = name;
    }
    void run(){
        cout << "A car is running .. !" << endl;
        //easily got runtime error when down casting
        cout << "A car of " << ownerName << " is running .. !" << endl;

    }
};

class truck : public car{
protected:
public:
    truck(){
        cout << "created a new truck" << endl;
    }
    //override => showing clearly this function is inherited and defined again in sub class
    void run() override {
        cout << "A truck is running ... !" << endl;
    }
};

//multi inheritance => check carefully before buidling as it easily got ambiguous errors and diamond inheritance ambiguous errors -> using virtual for access modifier => solve ambiguous properties or function
//as base classes may have the same properties or methods => ambiguous
//usually use multi inheritance for unrelated base class such as house or car
class house{
protected:
    float area;
    //ambiguous properties
    string modelName;
public:
    float getArea(){ 
        return area;
    }
    void setArea(float s){
        area = s;
    }
    void printArea(){
        cout << fixed << setprecision(2) << this->getArea() << "m^2" << endl;
    }
    //ambiguous methods
    void setModelName(string name){
        modelName = name;
    }
    string getModelName(){
        return modelName;
    }
};

class mobihome : public vehicle, public house{
protected:
public:
    void run(){
        cout << "A mobihome is running .. !" << endl;
    }
};

//Abstract class => cannot initalize (cannot create object) but can use as pointer to manage subclass + up casting down casting + must have subclass 
//pure virtual function => must be defined again in sub class to initalize and use (at least 1 pure virtual => Abstract class)
//usually don't create Constructor using virtual
class person{
protected:
    string name;
public:
    //Abstract Class => at least 1 pure virtual 
    virtual string getName() = 0;
    virtual void setName(string name) = 0;
    virtual void greeting() = 0;
    //Interface => all functions in class are pure virtual
};

struct gpa{
    float Lit, Maths, English;
};

class student : public person{
protected:
    gpa g;
public:
    //functions defined in sub class => can call and use
    string getName(){
        return name;
    }
    void setName(string name){
        this->name = name;
    }
    void greeting(){
        cout << "Student " << this->name << " hello !" << endl;
    }
};

int main(){
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    ios::sync_with_stdio(false); 
    cin.tie(nullptr); cout.tie(nullptr);

    taxi* Taxi = new taxi;
    Taxi->run();
    Taxi->setKmCounter(18.6);
    Taxi->print();
    delete Taxi;

    truck* Truck = new truck;
    Truck->run();

    mobihome* m = new mobihome;
    m->run();
    m->setArea(16);
    m->printArea();

    //Polymorphism => must be mastered for interviewing
    //Casting => Related to type casting
    car* Car = new car;
    Car->run();
    //Upcasting => sub class to base class
    ((vehicle*)Car)->run(); //syntax
    //Downcasting => base class to sub class => easily got error as it may not include some properties from subclass => runtime error
    vehicle* Vehicle = new vehicle;
    Vehicle->run();
    ((car*)Vehicle)->run();
    //Down casting fixed runtime errors
    vehicle* v = Car; // up casting to Car by assigning => vehicle* v = (vehicle*)Car;
    v->run(); //((car*)v)->run(); => down casting 
    //Manage a list of sub class inheriated base class
    vehicle* list[2];
    list[0] = new car();
    list[1] = new truck();
    for(int i = 0; i < 2; i++) list[i]->run();

    person* p = new person(); // cannot initalize (dont use general object in real life => must be specific object)
    student* s = new student();
    s->greeting();
}
```   
- Sample 2 : Tối ưu hóa
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

/*Forward Declaration => don't care about the order of class implementations
class person;
class vehicle;
class taxi;
...
*/

class person{
protected:
    string name;
public:
    //Initalization list
    person(string s) : name(s){}
    string getFullName(){
        return name;
    }
    void setFullName(string s){
        name = s;
    }
    void greeting(){
        cout << name << " Hello !" << endl;
    }
};

class vehicle{
protected:
    string modelName;
    //pass by pointer
    person* owner; // => don't need to have first value
public:
    //constructor
    vehicle(string name) : modelName(name){
        cout << "Created a vehicle " << name << endl;
    }
    //explicit default constructor => shallow copy => copy the value of datatypes to variables
    vehicle(vehicle& other){
        //not a pointer so dont use (->)
        cout << "Clone a vehicle " << other.getModelName() << endl;
        //have to assign the property to have the value
        modelName = other.getModelName();
        //some data types cannot be copied such as pointer => can create a new pointer with the same memory allocation
        //onwer = other.getOwner();
        //deep copy => change the default copy constructor with datatype pointer using operator new
        owner = new person(other.getOwner()->getFullName());
    }

    string getModelName(){
        return modelName;
    }
    void setOwner(person* p){
        owner = p;
    }
    person* getOwner(){
        return owner;
    }
    virtual void run(){
        cout << modelName << " is running .. !" << endl;
    }
};

class taxi : public vehicle{
protected:
    float kmCounter;
public:
    float kmFee(){
        return kmCounter * 100;
    }
    void getFee(){
        cout << "Km : "<< kmCounter << "km" << endl << "Total : "<< fixed << setprecision(0) << this->kmFee() << endl;
    }
    void run(){
        cout << modelName << " is running .. !" << endl;
    }
};

class otherPerson{
protected:
    string otherName;
public:
    //Initalization list
    otherPerson(string s) : otherName(s){}
    string getName(){
        return otherName;
    }
    void setName(string s){
        otherName = s;
    }
    void greeting(){
        cout << otherName << " Hello !" << endl;
    }
};

class otherVehicle{
protected:
    string otherModelName;
    int otherManufactureYear;
    float otherFrameSize[3];
    //reference => person have vehicle (without reference => vehicle have person -> wrong relation)
    //pass by reference
    otherPerson &otherOwner; // => need to have first value => use initialization list
public:
    //initialization list => Constructor
    otherVehicle(string name, int year, otherPerson& p) 
    : otherModelName(name), 
    otherManufactureYear(year),
    otherOwner(p),
    otherFrameSize{1.7, 2, 1.5}
    {
        // Error : otherOwner = p
        //not initialize -> assign variables
        // otherModelName = name;
        // otherManufactureYear = year;
        // cannot use frameSize = {1.7, 2, 1,5}
        // Have to use frameSize[0] = 1.7, frameSize[1] = 12,...=> instead use initalization list
        cout << "Created a new vehicle" << endl;
    }
    //Getter Setter
    string getOtherModelName(){
        return otherModelName;
    }
    int getOtherManufacturerYear(){
        return otherManufactureYear;
    }
    //Method
    virtual void operate(){
        cout << otherModelName << " is running .. !" << endl;
    }
};

//Inheritance 
class otherTaxi : public otherVehicle{
protected:
    float kmCount;
public:
    //Initalization list
    otherTaxi(string name, int year, otherPerson& owner, float km) : otherVehicle(name, year, owner), kmCount(km){
        cout << "Created a new taxi" << endl;
    }
    //Methods
    void operate(){
        //Override
        otherVehicle::operate();
        cout << "It is a taxi" << endl;
        cout << "A taxi is running .. !" << endl;
    }
    float otherKmFee(){
        return kmCount * 100;
    }
    void getOtherFee(){
        cout << "Km : "<< kmCount << "km" << endl << "Total : "<< fixed << setprecision(0) << this->otherKmFee() << endl;
    }
};

//base class
class vehicle2{
protected:
    string vName;
public:
    //constructor
    vehicle2(string s) : vName(s){}
    //pure virtual
    virtual string getName2() = 0;
};
class engine{};
class checker{};
//inheritance
class taxi2 : public vehicle2{
protected:
    //aggregation relation => initialize in constructor not in main function 
    engine e;
    // engine *Engine; => dynamic allocation memory
public:
    //const reference of pointer parameter
    taxi2(const string& s) : vehicle2(s){/* e.init()...; e.set()...; / Engine = new engine */}
    //~taxi2(){delete Engine} => free up the memory for program
    //Getter Setter
    string getName2(){
        return vName;
    }
};

class driver{
protected:
    string driverName;
    //composition relation
    vehicle2* newVehicle; 
public:
    driver(const string& s) : driverName(s){}
    string getDriverName(){
        return driverName;
    }
    void setDriverName(string s){
        driverName = s;
    }
    void setVehicle(vehicle2* v){
        newVehicle = v;
    }
    void getVehicle(){
        cout << driverName << " has a " << newVehicle->getName2()<< endl;
    }
};

//Const reference of pointer parameters
struct registerInfo{
    registerInfo(){}
    registerInfo(registerInfo &info){
        cout << "Clone a register info" << endl;
    }
    string license, ownerName;
};

class truck{
protected:
    string truckName, license, ownerName;
    driver *Driver;
public:
    //pass by value => assign parameters to variables or copy attributes between struct or class
    //system will automatically copy value passed in main function and assign to parameters in constructor => takes a lot of time
    //truck(string s, registerInfo info) : truckName(s), license(info.license), ownerName(info.ownerName){}
    //pass by reference of pointer => inficient time because it will copy the name of memory allocation of value passed before => use for class or struct
    //truck(string& s, registerInfo& info) : truckName(s), license(info.license), ownerName(info.ownerName){} //string also a class
    //in copy constructor we want to copy the data without changing it => use const keyword
    truck(const string& s, const registerInfo& info) : truckName(s), license(info.license), ownerName(info.ownerName){}
    void setTruckOwner(driver* d){
        Driver = d;
    }
    driver* getTruckOwner(){
        return Driver;
    }
    virtual void truckRun(){
        cout << "A truck is running .. !" << endl;
    }
};


int main(){
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    ios::sync_with_stdio(false); 
    cin.tie(nullptr); cout.tie(nullptr);

    //Copy constructor => create a different copy to operate independently
    person* p2 = new person("Vu");
    vehicle* v1 = new vehicle("Ford");
    v1->setOwner(p2);
    //Default copy constructor when constructor with parameters is not created => can be automatically created when not writing a constructor in class
    vehicle* v2 = new vehicle(*v1);
    v2->getOwner()->setFullName("Nam");
    cout << v1->getOwner()->getFullName() << endl;
    cout << v2->getOwner()->getFullName() << endl;
    v1->run();
    v2->run();

    //Initialization list
    otherPerson p1("Ngoc");
    otherTaxi* t = new otherTaxi("Ford", 2030, p1, 18);
    t->operate();
    t->otherKmFee();
    t->getOtherFee();

    //Composition relation
    vehicle2* Vehicle = new taxi2("Misubishi"); 
    driver* Driver = new driver("Khai");
    Driver->setVehicle(Vehicle);
    Driver->getVehicle();

    registerInfo info;
    info.license = "79C1-18705";
    info.ownerName = "Ty";
    //copy constructor will automatically called if using pass by value
    truck* Truck = new truck("Huyndai", info);
    Truck->truckRun();
}
``` 
- Sample 3 :
``` cpp
#include <bits/stdc++.h>
using namespace std;

class Ve{
protected:
    int Gia;
    int SoDoAn, SoThucUong;
public:
    void Nhap() {
        cout << "Nhap vao so do an: ";
        cin >> SoDoAn;
        cout << "Nhap vao so thuc uong: ";
        cin >> SoThucUong;
    }
    int getGia() {
        return Gia;
    }
    int getSoDoAn() {
        return SoDoAn;
    }
    int getSoThucUong() {
        return SoThucUong;
    }
    virtual bool LaVeSV() {
        return false;
    }
    virtual bool LaVeThuong() {
        return false;
    }
    virtual void TinhGiaVe() = 0;
};

class VeCombo : public Ve {
public:
    void TinhGiaVe() {
        Gia = 200000;
    }
};

class VeThuong : public Ve {
public:
    bool LaVeThuong() {
        return true;
    }
    void TinhGiaVe() {
        Gia = 60000 + 30000 * (SoDoAn + SoThucUong);
    }
};

class VeSV : public Ve {
public:
    bool LaVeSV() {
        return true;
    }
    void TinhGiaVe() {
        Gia = 30000 + 30000 * (SoDoAn + SoThucUong);
    }
};


int main() {
    int n, sum = 0, cnt = 0, tmp = 0;
    double avg = 0;

    cout <<"Nhap vao so ve: ";
    cin >> n;
    Ve** ds = new Ve*[n];
    for(int i = 0; i < n; i++) {
        int tmp;
        cout <<"1:Ve combo\n2:Ve thuong\n3:Ve sinh vien\nChon loai ve: ";
        cin >> tmp;

        if(tmp == 1) {
            ds[i] = new VeCombo();
        }
        else if(tmp == 2) {
            ds[i] = new VeThuong();
        }
        else ds[i] = new VeSV();

        ds[i]->Nhap();
        ds[i]->TinhGiaVe();
    }
    for(int i = 0; i < n; i++) {
        if(ds[i]->LaVeSV()) {
            sum+=ds[i]->getGia();
        }
    }
    cout << "Tong so tien ve sinh vien da ban la: " << sum << endl;;
    for(int i = 0; i < n; i++) {
        if(ds[i]->LaVeThuong()) {
            cnt++;
            tmp += ds[i]->getSoDoAn() + ds[i]->getSoThucUong();
        }
    }
    if(cnt != 0) avg = tmp * 1.0 / cnt;
    cout << "Trung binh moi ve thuong khach hang se mua " << avg <<" phan do an va thuc uong.";
}
```
- Chia file trong OOP + Design Pattern :
    - header.h
    ```cpp
    //pragma once
    //file.h chứa hết toàn bộ thuộc tính và phương thức của class
    #include <bits/stdc++.h>
    using namespace std;

    //Singleton => class yêu cầu chỉ có 1 đối tượng => quản lý các class khác
    class vehicle{
    protected:
        string modelName;
    public:
        vehicle(string name);
        string getModelName();
        virtual void run();
    };

    class vehicleManager{
    protected:
        vector<vehicle*> vehicles;
        //Tạo thuộc tính để quản lý class mà ko phụ thuộc vào class ấy => ko cần khởi tạo đối tượng mà có thể sử dụng luôn => static
        static vehicleManager* manager; //thuộc tính lưu object manager
        //constructor in private => giới hạn lại số lần cấp phát động ra các đối tượng từ bên ngoài
        vehicleManager();
    public:
        //tạo hàm chứa được biến quản lý staic đó
        static vehicleManager* getManager(); //phương thức lấy ra thuộc tính đó
        void addVehicle(vehicle* v);
        void start();
    };

    //Facade => First add pattern => như một cái app tổng hướng dẫn người dùng sử dụng chức năng như thế nào => Abstraction
    class vehicleApp{
    protected:
    public:
        //luôn luôn có 1 hàm khởi tạo => khởi tạo dữ liệu ban đầu mà chương trình cần làm
        void init();
        void start();
    };
    ```
    - implementation.cpp
    ```cpp
    #include "vehicle.h"
    #include <bits/stdc++.h>
    using namespace std;

    //Implementation => cài đặt các phương thức
    vehicle::vehicle(string name) : modelName(name){}
    string vehicle::getModelName(){
        return modelName;
    }
    void vehicle::run(){
        cout << modelName << " is running .. !" << endl;
    }

    //Khởi tạo giá trị cho biến manager
    vehicleManager* vehicleManager::manager = NULL;
    vehicleManager::vehicleManager(){
        cout << "Created a manager" << endl;
    }
    vehicleManager* vehicleManager::getManager(){ //phương thức lấy ra thuộc tính đó
        if(manager == NULL) manager = new vehicleManager();
        return manager;
    }
    void vehicleManager::addVehicle(vehicle* v){
        vehicles.push_back(v);
    }
    void vehicleManager::start(){
        for(vehicle* v : vehicles) v->run();
    }

    void vehicleApp::init(){
        //dữ liệu thực tế sẽ load từ database đây chỉ là demo nên cho fix cứng
        vehicle* t = new vehicle("Kia Morning");
        vehicle* v = new vehicle("Ford Ranger");
        //truy cập manager qua phương thức static
        vehicleManager::getManager()->addVehicle(t);
        vehicleManager::getManager()->addVehicle(v);
    }
    void vehicleApp::start(){
        vehicleManager::getManager()->start();
    }
    ```
    - main.cpp
    ```cpp
    #include "vehicle.h"
    using namespace std;
    int main(){
        //người dùng chỉ cần sử dụng qua các chức năng có trong app mà ko cần quan tâm cài đặt nó như thế nào
        vehicleApp* app = new vehicleApp;
        app->init();
        app->start();
    }
    ```
    
