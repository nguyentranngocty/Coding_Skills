# STL
## Functions in <algorithm> of STL
- Các hàm :
    - `min`
    - `max`
    - `min_element`
    - `max_element`
    - `accumulate`
    - `swap`
    - `find`
    - `binary_search`
    - `sort`
    - `stable_sort`
    - `lower_bound` : >= x 
    - `upper_bound` : > x
    - `memset`
    - `fill`
    - `merge`
    - `reverse`
    - Đều phải sort trước khi sử dụng => các phép trong tập hợp
        - `set_union`
        - `set_intersection`
        - `set_difference`
        - `set_symmetric_difference`
- Cài đặt :
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    using ll = long long;

    int main(){
        freopen("input.txt", "r", stdin);
        freopen("output.txt", "w", stdout);
        ios::sync_with_stdio(false); 
        cin.tie(nullptr); cout.tie(nullptr);

        //input mảng và vector ban đầu
        int n; cin >> n;
        int a[n];
        vector<int> v;
        for(int &x : a){
            cin >> x;
            v.push_back(x);
        }

        //min(), max();
        cout << min(10, 20) << endl; // tương tự với max()
        cout << max({10, 20, 30, 50}) << endl; // tương tự vs min()

        //min_element(), max_element(); => trả về con trỏ và iterator đến phần tử => dùng * để giải tham chiếu
        cout << *max_element(a, a + n) << endl;
        cout << *min_element(v.begin() + 3, v.begin() + 5) << endl;

        //accumulate => tính tổng
        int sum = accumulate(a, a + n, 0); //giống như khởi tạo s = 0 -> đi cộng vào
        cout << sum << endl;
        cout << accumulate(v.begin(), v.end(), 0) << endl;

        //swap => hoán vị giá trị 2 phần tử 
        int x = 100, y = 200;
        cout << x << ' ' << y << endl;
        swap(x, y);
        cout << x << ' ' << y << endl;

        //find() tìm 1 phần tử có xuất hiện trong mảng, vector, set hay ko => trả về iterator hoặc con trỏ
        if(find(a, a + n, 5) != a + n) cout << "FOUND" << endl;
        else cout << "NOT FOUND" << endl;
        if(find(v.begin(), v.end(), 4) != v.end()) cout << "FOUND" << endl;
        else cout << "NOT FOUND" << endl;

        //binary search => trả vể TRUE or FALSE và chỉ áp dụng cho mảng, vector đã sắp xếp tăng dần
        if(binary_search(a, a + n, 5)) cout << "FOUND" << endl;
        else cout << "NOT FOUND" << endl;

        //sort -> upper_bound đã được tìm hiểu và trình bày (lower_bound và upper_bound trả vể con trỏ hoặc vector)

        //memset() => gán tất cả các phần tử trong mảng, mảng 2 chiều cho 0 hoặc -1
        int b[n];
        memset(b, 0, sizeof(a)); 
        for(int x : b) cout << x << ' ';
        cout << endl;

        //fill() => gán tất cả các phần tử trong mảng, vector cho 1 giá trị bất kì
        vector<int> vi(5);
        fill(begin(vi), end(vi), 200);
        for(int x : vi) cout << x << ' ';
        cout << endl;

        //merge => trộn 2 dãy tăng dần vào 1 dãy
        vector<int> res(10);
        vector<int> c = {1, 2, 3, 6, 8};
        vector<int> d = {2, 4, 7, 10, 11};
        merge(c.begin(), c.end(), d.begin(), d.end(), res.begin());
        for(int x : res) cout << x << ' ';
        cout << endl;

        //reverse() => lật ngược mảng hoặc vector hoặc string
        string s = "ngocty";
        reverse(s.begin(), s.end());
        cout << s << endl;

        //set_union tương tự vs các hàm set_ khác
        int z[] = {1, 2, 3, 4, 5};
        int t[] = {1, 3, 4, 9, 10};
        vector<int> u(11);
        auto it = set_union(z, z + 5, t, t + 5, u.begin()); // tương tự những cái còn lại
        // phải resize vector u đi vì sau khi giao hợp hiệu thì vector u kích thước sẽ thay đổi chứ ko như ban đầu
        u.resize(it - u.begin());
        for(auto x : u) cout << x << ' ';
        cout << endl;
    }
    ```
## Iterator
- Các hàm :
    - `v.begin()` : phần tử đầu
    - `v.rbegin()` : phần tử cuối
    - `v.end()` : sau phần tử cuối
    - `v.rend()` : trước phần tử đầu
- Dùng iterator để duyệt set, map, vector, pair
    - [x; y) = (v.begin() + x, v.begin() + y);
    - [x; y] = (v.begin() + x, v.begin() + y + 1);
    - v[x] = v.begin() + x 
``` cpp
for(int i = 0; i < vi.size(); i++) cin >> v[i] ;
for(int &x : vi) cin >> x;
for(int i = 0; i < vi.size(); i++) cout << v[i] ;
for(int x : vi) cout << x;
for(vector<int>::iterator it = vi.begin(); it ≠ vi.end(); it++) cout << *it;
vector<int>::iterator it = auto it  //auto thay cho mọi kiểu dữ liệu
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
    - `vi.erase(vị trí)` : xóa phần tử thông qua iterator `vi.erase(vi.begin() + x)`  
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
    - `se.insert(giá trị)` : thêm phần tử vào set  `se.insert(3)`
    - `se.size()` : số lượng phần tử trong set
    - `se.find(x)`: tìm phần tử trong set trả về iterator trỏ tới phần tử trong set
        - `auto it = se.find(3);`
        - `vector<int>::iterator it = se.find(3);`
    - `se.count(x)` : đếm số phần tử xuất hiện trong set cho ra giá trị là 0 hoặc 1
    - `se.erase(x)` : xóa phần tử trong set
### multiset
- Khai báo : multiset<kiểu_dữ_liệu> tên_biến `multiset<long long> se;`
- Các hàm giống set trừ hàm find :
    - `se.find(x)` : trả về iterator của phần tử đầu tiên nếu các phần tử trùng nhau
### unordered_set
- Khai báo : unordered_set<kiểu_dữ_liệu> tên_biến `unordered_set<string> se;` 
- Các hàm giống set
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
    - `mp[key] = value` : có thể thay đổi giá trị của key đã cho trước
    - `mp[key]++` : tăng giá trị của value có trước lên 1 còn nếu chưa có key với value trong map thì tự động thêm vào và cho `mp[key] = 1`
    - `mp.size()` : số lượng cặp pt
    - `mp.find(x)` : tìm key có nằm trong map hay không và trả về iterator như vector hoặc set
    - `mp.count(x)` : đếm xem key trong map xuất hiện bao nhiêu lần
    - `mp.erase(x)` : xóa cả key và value và xóa thông qua key
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
    - `+` : concate nối 2 xâu lại và cũng có thể nối xâu với kí tự
    - `isdigit(char c)` : kiểm tra chữ số
    - `islower(char c)` : kiểm tra chữ in thường
    - `isupper(char c)` : kiểm tra in hoa
    - `isalpha(char c)` : kiểm tra chữ cái
    - `int tolower(char c)` : chuyển thành chữ in thường mã ASCII ép kiểu char
    - `int toupper(char c)` : chuyển thành chữ in hoa mã ASCII ép kiểu char ta thường dùng `s[i] = toupper(s[i])` => gán lại cho s[i]
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