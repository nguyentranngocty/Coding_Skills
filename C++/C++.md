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
//các toán tử được định nghĩa trong namespace
using namespace std; 
using ll = long long;

int main(){
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
	ios::sync_with_stdio(false); 
	cin.tie(nullptr); cout.tie(nullptr);	
}
```
## File
- Cài đặt :
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
- Viết hàm và gọi hàm :
    ```cpp
    int check(int a, int b /*Tham số hình thức*/){
        return a;
    }

    int main(){
        int x = 5, y = 10; //Tham số chính thức
        check(x, y); // lời gọi hàm 
    }
    ```
- Nạp chồng hàm : tên hàm có thế giống nhau nhưng kiểu trả về khác nhau 
    ```cpp
    void Tinh_tong(){
    }
    long long Ting_tong(){
    }
    ```
- Truyền giá trị mặc định tham số vào hàm : truyền vào phần tử cuối bên phải nếu chỉ truyền 1 tham số || truyền hết cho n tham số
    - `void f(int a = 5, long long b = 7, float c = 7.6);`
    - `void f(int a, int b, char c = 'c');`
- Viết hàm có tham số là con trỏ hoặc mảng :
```cpp
// con trỏ
void f(int *a){
    code
}
int main(){
    f(&a);
}

// mảng 1 chiều
void f(int a[], int n){
    code
}
int main(){
    f(a, 10);
}

// mảng 2 chiều
void f(int a[][1000], int n){
    code
}
int main(){
    int n, m; cin >> n >> m;
    int a[n][m];
    f(a, n);
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
- Ứng dụng :
    ```cpp
    //Đếm phân phối => khai báo mảng đánh dấu ngoài main -> tránh bị tràn bộ nhớ
    int cnt[10000001] = {0}; 
    int mark[10000001] = {0};
    int used[10000001] = {0};

    //Liệt kê theo thứ tự tăng dân
    void counting1(int a[], int n){
        int min_val = INT_MAX; max_val = INT_MIN;
        for(int i = 0; i < n; i++){
            cnt[a[i]]++;
            max_val = max(max_val, a[i]);
            min_val = min(max_val, a[i]);
        }
        for(int i = min_val; i <= max_val; i++){
            if(cnt[i]) cout << i << ' ' << cnt[i];
        }
    }

    //Liệt kê theo thứ tự xuất hiện của các phần tử trong mảng
    void counting2(int a[], int n){
        for(int i = 0; i < n; i++){
            mark[a[i]]++;
        }
        for(int i = 0; i < n; i++){
            if(used[a[i]] == 0){
                cout << a[i] << ' ' << mark[a[i]] << endl;
                used[a[i]] = 1;
            }
        }
    }

    // Đảo ngược máng
    void reverse(int a[], int n){
        int l = 0; r = n - 1;
        while(l <= r){
            swap(a[l], a[r]); //int temp = a[l]; a[l] = a[r]; a[r] = temp;
            l++; r--;
        }
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
  
