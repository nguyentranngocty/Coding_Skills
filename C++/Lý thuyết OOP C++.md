# OOP

## STRUCT

- Khai báo struct : struct tên { thuộc tính; hàm; hàm khởi tạo, nạp chồng toán tử};

- Mỗi đối tượng có nhiều thuộc tính giống nhau → struct SinhVien chứ ko dùng mảng vì quá phiền
- Viết hàm trong struct (a.tên_hàm()) hoặc ngoài struct (tên_hàm(a))
- Khởi tạo : struct biến → dùng hàm nhập thông tin riêng hoặc **struct biến{truyền thông tin lần lượt theo thứ tự**}, nếu struct có 1 thông tin thì **struct biến(thông tin)**
- **con trỏ this** : trỏ vào đối tượng
    - VD : this → sinhVien x :  this → ten = ten (x.ten = ten)
- Trong struct nên xây dựng đầy đủ các constructor và đặc biệt hàm constructor mặc định VD Sinhvien(){ } → khai báo ko bị lỗi ⇒ bắt buộc phải luôn có constructor đó trước khi tạo các construtor khác có truyền tham số vào
- s = 01/05/2002 (đúng form như v) → tách s1 = 20020501 → viết cmp so sánh về tuổi ⇒ sẽ so sánh theo thứ tự từ điển là tuổi lớn → tuổi nhỏ
- Cài đặt :
    
    ```cpp
    //Một struct căn bản
    struct student{
    	string name, birth_day;
    	int student_id, gender;
    	
    	//CONSTRUCTOR MẶC ĐỊNH
    	student(){ //1
    	}
    	
    	//CONSTRUCTOR (có thể truyền tham số hoặc ko)-> tên của struct và ko có kiểu trả về (những thuộc tính nhiều đối tượng có thì tạo hàm khởi tạo mặc định)
    	student(int g){
    		name = "James"; //2
    		student_id = 1;
    		birth_day = "0192";
    		gender = g;
    	}
    	
    	student(string ten, string ns, int id, int gt){ //3
    		name = ten;
    		student_id = id;
    		birth_day = ns;
    		gender = gt;
    	}
    
    	void input(){ //Hàm trong struct thì chỉ dùng con trỏ this hoặc ko
    		getline(cin, name);
    		cin >> student_id; cin.ignore();
    		getline(cin, birth_day);
    		cin >> gender;
    	}
    
    	void output(){
    		cout << name << " " << student_id << " " << birth_day << " " << gender;
    	}
    	//DESTRUCTOR MẶC ĐỊNH
    	~student(){
    	}
    };
    
    void nhap(student &a){ //Hàm bên ngoài thì bắt buộc phải a.thuộc tính hoặc a -> thuộc tính
    	getline(cin, a.name);
    	cin >> a.student_id; cin.ignore();
    	getline(cin, a.birth_day);
    	cin >> a.gender;
    }
    
    void xuat(student a){
    	cout << a.name << " " << a.student_id << " " << a.birth_day << " " << a.gender;
    }
    
    //Nạp chồng toán tử -> qua vd về struct số phức
    struct soPhuc{ //x = a +bi
    	int a, b;
    	
    	//2 cách nạp chồng toán tử
    	soPhuc operator + (const soPhuc other){
    		soPhuc tong;
    		tong.a = a + other.a;
    		tong.b = b + other.b;
    		return tong;
    	}
    	friend soPhuc operator - (const soPhuc x, const soPhuc y){
    		soPhuc hieu;
    		hieu.a = x.a - y.a;
    		hieu.b = x.b - y.b;
    		return hieu;
    	}
    
    	//insertion -> luồng cin
    	friend istream& operator >> (istream& in, soPhuc &x){
    		in >> x.a >> x.b;
    		return in;
    	}
    
    	//extraction -> luồng cout
    	friend ostream& operator << (ostream& out, soPhuc x){
    		out << x.a << " " << "+" << " " << x.b << "i";
    		return out;
    	}
    	
    	//boolean
    	friend bool operator == (soPhuc x, soPhuc y){
    		return x.a == y.a && x.b == y.b;
    	}
    
    	friend bool operator > (soPhuc x, soPhuc y){
    		return sqrt(x.a * x.a + x.b * x.b) > sqrt(y.a * y.a + y.b * y.b); 
    	}
    };
    
    void input(soPhuc &p){
    	cin >> p.a >> p.b;
    }
    
    void output(soPhuc p){
    	cout << p.a << " " << "+" << " " << p.b << "i";
    }
    
    int main(){
    	//Class 1	
    	student a{"Anna S.",  "01-01-2001", 123456789, 2}; //3
    	a.output(); cout << endl;
    	student b; //1 
    	nhap(b); //b.input();
    	xuat(b); 
    	student c(1); //2
    	xuat(c);
    	
    	//Class 2
    	soPhuc x, y, z;
    	//Cách nhập và xuất 1
    	input(x); 
    	output(x); 
    	cout << endl;
    	//Cách nhập và xuất 2 -> nạp chồng toán tử cin và cout vào struct
    	cin >> y; 
    	cout << y; 
    	cout << endl;
    	//Tính toán thẳng qua toán tử mà ko cần viết hàm tính riêng
    	z = x + y;
    	cout << z;
    	//So sánh cũng qua toán tử
    	if(x > y) cout << "True";
    	else cout << "False";
    }
    ```
    

## Class - Object - Khái niệm

### Tạo class, constructor, constructor initialization list, tạo object từ class, destructor

- Khai báo class :

```cpp
#include <iostream>
#include <string>

class HumanBeings {
public:
    std::string name;
    void human() {
        std::cout << "My name is: " << name;
    }
};

int main() {
    **HumanBeings myself;    //** Tạo đối tượng từ lớp HumanBeings trên stack
    **HumanBeings *myself = new HumanBeings();   //** Tạo đối tượng từ lớp HumanBeings trên heap (cần giải phóng bằng delete khi không cần thiết nữa)
}
```
- Constructor:

    - Có thể gọi là **hàm thiết lập** hoặc **hàm khởi tạo**
    - Constructor được khai báo giống như một phương thức với **tên phương thức trùng với tên lớp** và **không có giá trị trả về** (kể cả void).
    - Constructor phải có **phạm vi là public**
    - Constructor **có thể được khai báo chồng** như các hàm C++ thông thường
    - Constructor có thể khai báo **default parameters**
    - `PhanSo() {}` được **coi là constructor mặc định** khi chưa có constructor khác
    - Khi có một **constructor khác viết đè** thì **constructor mặc định sẽ biến mất** (có thể tự tạo lại như dưới đây)

    ```cpp
    class PhanSo {
    private:
        int tu, mau;
    public:
        PhanSo() {};
        PhanSo(int tu, int mau) {
            ....
        }
    };
    ```

- Constructor initialization list:

    - **Cho phép gọi constructor của đối tượng thành phần** (đối tượng là thành phần của lớp và đối tượng thành phần thuộc kiểu cơ sở)

    ```cpp
    class Diem {
    private:
        int x;
        int y;
    public:
        Diem() {};
        Diem(int x, int y) {
            this->x = x;
            this->y = y;
        }
    };

    class TamGiac {
    private:
        Diem A, B, C;
        int count;
    public:
            // Cách bình thường
        TamGiac(int x1, int y1, int x2, int y2, int x3, int y3, count) {
            A = Diem(x1, y1);
            B = Diem(x2, y2);
            C = Diem(x3, y3);
        }
        
            // Constructor initialization list
        TamGiac(int x1, int y1, int x2, int y2, int x3, int y3, int count) : A(x1, y1), B(x2, y2), C(x3, y3), count(count) {};
    };
    ```

- Tạo object từ class:

```cpp
// Tạo một constructor khác đè lên constructor mặc định
PhanSo a(1, 2);
PhanSo a = PhanSo(1, 2);
PhanSo *a = new PhanSo(1, 2);
		
// Nếu đã tạo lại constructor mặc định sau khi đã có constructor khác
PhanSo b;
PhanSo b = PhanSo();
PhanSo *b = new PhanSo();
		
// Không được
PhanSo c();
```

- Destructor:

    - Destructor có **tên giống class**, nhưng bắt đầu bằng **~.**
    - **Không có tham số** cho destructor.
    - **Tự động gọi** khi object không còn được sử dụng nữa.
    - Destructor phải nằm trong **public.**
        - **Nếu thuộc tính trong của đối tượng là một con trỏ trong vùng nhớ động** ⇒ trong hàm destructor phải delete con trỏ đó.

    ```cpp
    class HumanBeings {
    public:
        std::string name;
        void human() {
            std::cout << "My name is: " << name;
        }

        ~HumanBeings() { // Hàm hủy để giải phóng bộ nhớ khi đối tượng bị hủy
            std::cout << "Destructor called for " << name << std::endl;
        }
    };

    ```

### Property - method

- Property:

    - Property là các giá trị mô tả trạng thái đối tượng, chứa thông tin về các tính chất hoặc đặc điểm của đối tượng đó (đơn là giản là những biến không phải function)

    ```cpp
    class HumanBeings {
    private:
            // Property
        string name;
            string address;
            string phoneNumber;
            int age;
    }
    ```
- Method:

    - Method là một **function được định nghĩa ở trong class** để thực hiện một hành động cụ thể hoặc thực hiện một loạt các hành động trên với các property của object của class đó.

    - **Có quyền truy cập vào các thành phần private** của các đối tượng (tham chiếu đối tượng hay con trỏ đối tượng) có cùng class.

    ![Untitled](OOP%200025e91fb3df40b2b2fea74d1202ec5e/Untitled.png)

    ( Trong ví dụ trên thì method **KiemTraTrung** nằm trong class **Point** )

    ```cpp
    class HumanBeings {
    public:
            // Khai báo method trong bên trong class (như function bình thường)
        void human() {
            ....
        }
        
        // Định nghĩa method (để khai báo bên ngoài)
        void action();
    };

    // Khai báo bên ngoài 
    // Syntax **<type> <class_name>::<method_name>(<variable>) { ... }**
    void HumanBeings::action() {
            ....
    }
    ```

### Con trỏ this

- **Con trỏ this** chỉ tồn tại trong phạm vi methods của một class.
- **Con trỏ this** trỏ đến object hiện tại mà method đó đang thao tác.
- Đồng thời cũng giúp phân biệt biến ở trong object hay tham số của method nếu trùng tên

```cpp
class PhanSo {
private:
    int tu, mau;
public:
    PhanSo() {};
    PhanSo(int tu, int mau) {
	       this->tu = tu;
	       this->mau = mau;
    }
};
```

### Từ khóa friend

- Dùng từ khóa **`friend`** để khai báo, định nghĩa friend function, friend class.
- Có thể dùng **`friend`** mà trước đó function, class đó vẫn chưa được khai báo.

- Friend function:

    - Friend function không thuộc lớp nhưng **có quyền truy cập private, protected** của lớp ⇒ Cách cho phép **chia sẻ dữ liệu giữa các đối tượng với một hàm** tùy ý trong chương trình.
    - **Không dùng this được** như method.
    - **Syntax:    friend <type_return> <name>(<variable>)**

    ```cpp
    class Point {
    private:
        int x, y;
    public:
        Point(int a, int b) {
            x = a;
            y = b;
        }

        friend void getX(Point);

    };

    void getX(Point a) {    // Friend function
        cout << a.x << endl;
    }

    ```

- Friend class:

    - Friend class **có thể truy cập đến các thành phần có thuộc tính private** của một class khác.
    - **Syntax:   friend class <name_class>**

    ```cpp
    #include <iostream>
    #include <string>
    using namespace std;

    class NhanVien {
    private:
        string name = "Pham Hoang Vinh";
        int age = 18;
    public:
            // Friend class
        friend class CongTy;
        
        // Không thể khai báo một method là friend (chỉ có cách cho toàn bộ class là friend)
        friend void CongTy::getNhanVien(NhanVien);   // Error
    };

    class CongTy {
    private:
        string name;
    public:
        void getNhanVien(NhanVien &nhanvien) {
                // Nếu không có friend class thì không truy cập được private của NhanVien 
            cout << nhanvien.name << " " << nhanvien.age << endl;
        }
    };

    int main() {
        CongTy congty;
        NhanVien nhanvien;
        congty.getNhanVien(nhanvien);
    }
    ```

### Truy vấn và cập nhật (get và set)

- Truy vấn:

    - Đối với truy vấn đơn giản, quy ước đặt tên với tiền tố **‘get’**
        
        **Vd**: int **get**Size(), int **get**Count(), …
        
    - Đối với truy vấn điều kiện, quy ước đặt tên với tiền tố **‘is’**
        
        **Vd**: int **is**Highest(), int **is**Prime(), …
        
    - Các loại truy vấn khác **nên có tên có tính mô tả.**

- Cập nhật:

    - Thường để thay đổi trạng thái của đối tượng bằng cách sửa đổi một hoặc nhiều thành viên dữ liệu của đối tượng đó.

    - Quy ước đặt tên với tiền tố **‘set’.**
        
        - **Vd**: void **set**Name(), void **set**Age(), …
    

- Ý nghĩa:

    - Bảo vệ nguyên tắc đóng gói, kiểm tra xem giá trị mới có hợp lệ để sửa đổi không.
    - Sử dụng truy vấn cho phép kiểm tra trước khi thực hiện thay đổi giá trị.
    - Chỉ cho phép các dữ liệu có thể truy vấn hay thay đổi mới được truy cập đến.

### Static member

- Static dùng để khai báo biến, method dùng chung cho class, **chỉ có một bản duy nhất tồn tại trong suốt quá trình chạy.**
- Các static member có thể là **public**, **private**, **protected**.
- Static cũng là một member của class, vậy nên **có quyền truy cập tất cả.**
- Giải thích tại sao **`int** NhanVien::countPublic = 0`; mà không phải `NhanVien::countPublic = 0` : Vì khi khai báo trong class một biến static, ta chỉ cung cấp type và name của biến đó, chứ không phát bộ nhớ cho nó. Giống như ta đang chỉ định rằng có một biến static tên “….” thuộc class “….”. ⇒ Vậy nên **phải khai báo và ở khởi tạo bên ngoài class**.
- Giải thích tại sao không khai báo được trong main : Biến static phải khai báo và khởi tạo bên ngoài hàm main để đảm bảo rằng bộ nhớ được cấp phát cho biến trước khi bất kì mã chương trình nào được thực thi. (Khi khai báo và khởi tạo trong hàm main sẽ không hoạt động vì main là một phần của chương trình) ⇒ **Phải khai báo và khởi tạo ngoài hàm main.**

- Với property:

```cpp
class NhanVien {
private:
    string name;
    int age;
    ....
    static int countPrivate;
public:
    static int countPublic;
};

// Khai báo bên ngoài
int NhanVien::countPublic = 0;
int NhanVien::countPrivate = 0;

int main() {
    cout << NhanVien::countPublic; // Có thể truy cập được public
	    cout << NhanVien::countPrivate; // Error vì private

    // Không được khai báo bên trong hàm main
    int NhanVien::countPublic = 0;   // Error
}
```

- Với method:

```cpp
#include <iostream>
#include <string>
using namespace std;

class NhanVien {
private:
    string name = "No Name";
    int age = 0;
public:
    static void print(NhanVien);   // Khai báo static method
};

void NhanVien::print(NhanVien nhanvien) {
    cout << nhanvien.name << nhanvien.age;
    
    // Không thể trực tiếp truy cập thẳng vô
    cout << name << age;   // Error
}
int main() {
    NhanVien nhanvien;
    NhanVien::print(nhanvien);
}
```

### Operator overload

- Cho phép sử dụng toán tử toán học đối với các kiểu dữ liệu của c++ thay vì gọi hàm
    
    (**VD**:  Thay `c = a.cong(b)` bằng `c = a + b`)
    
- Chỉ được cho phép **tạo phép toán mới trên cơ sở các kí hiệu phép toán đã có**, **không được quyền cài đặt phép toán mới**. [ cài đặt thêm phép toán là **sự nạp chồng toán tử** (hay **operator overload**) ].
- **Không thể thay đổi thứ tự ưu tiên** của toán tử

- Một số **toán tử đơn** có thể dùng làm cả toán tử trước và toán tử sau. VD: ++, —
- Một số toán tử có thể dùng làm cả toán tử đơn  và toán tử đôi như * (**toán tử đơn**: giải tham chiếu con trỏ ***ptr** ||| **toán tử đôi** : **a * b**).
- Toán tử chỉ mục **[…]** là toán tử đôi.
- Các từ khóa **new** và **delete** cũng được coi là toán tử và có thể định nghĩa lại.

![Untitled](OOP%200025e91fb3df40b2b2fea74d1202ec5e/Untitled%201.png)

![Untitled](OOP%200025e91fb3df40b2b2fea74d1202ec5e/Untitled%202.png)

- **Syntax**: **operator@** cho toán tử ‘**@**’

|  | Method of class | Global function |
| --- | --- | --- |
| aa@bb | aa.operator@(bb) | operator@(aa, bb) |
| @aa | aa.operator@() | operator@(aa) |
| aa@ | aa.operator@(int) | operator@(aa, int) |

- **Ví dụ operator overload**

```cpp
class PhanSo{
    long tu, mau;
public:
		....

    PhanSo operator* (PhanSo);
}

PhanSo PhanSo::operator*(PhanSo other) {
    ....
}

bool operator>(PhanSo a, PhanSo b) {
    return a.tu * b.mau > a.mau * a.tu;
}

int main() {
    PhanSo a(1, 2), b(3, 5);
//    PhanSo c = a.nhan(b);
    PhanSo c = a * b;
    c.printf();
}
```

- **Trường hợp viết thuần và cách chuyển kiểu bằng constructor**

    - Viết thuần mọi trường hợp xảy ra:

    ```cpp
    class PhanSo
    {
            ...
        PhanSo nhan(PhanSo);
        PhanSo operator*(PhanSo) const;
        PhanSo operator*(int) const;
        friend PhanSo operator*(int, PhanSo);
    }

    // TH: PhanSo * PhanSo
    PhanSo PhanSo::operator*(PhanSo otherPhanSo) const {
        PhanSo newPhanSo(this->numerator * otherPhanSo.numerator, this->denominator * otherPhanSo.denominator);
        return newPhanSo.rutGon();
    }

    // TH: PhanSo * int
    PhanSo PhanSo::operator*(int x) const {
        PhanSo newPhanSo(this->numerator * x, this->denominator);
        return newPhanSo.rutGon();
    }

    // TH: int * PhanSo
    PhanSo operator*(int x, PhanSo phanSo) {
        PhanSo newPhanSo(phanSo.numerator * x, phanSo.denominator);
        return newPhanSo.rutGon();
    }
    ```

    - Chuyển kiểu bằng constructor:

        - Theo quy tắc ép kiểu ngầm định của c++, **ưu tiên chuyển kiểu của constructor hơn các kiểu cơ bản.**

        **Điều kiện:**

        - Chuyển từ kiểu đã có (Vd: int) sang kiểu đang định nghĩa (Vd: PhanSo).
        - Phải có một quan hệ giữa kiểu đang định nghĩa và kiểu có sẵn (ví dụ kiểu có sẵn là **2** thành kiểu đang định nghĩa là **2/1**).

        **Ưu điểm:**

        - Có thể giảm số phép toán cần định nghĩa từ 3 xuống 1 bằng cách dùng hàm toàn cục (như dưới đây).

        **Nhược điểm:**

        - Muốn chuyển kiểu từ đang định nghĩa sang một kiểu đã có, ta phải chuyển đổi kiểu đã có.
        - Không thể chuyển từ kiểu đang định nghĩa sang kiểu cơ bản.

    ```cpp
    class PhanSo
    {
            ...
            PhanSo(int);   // chuyển kiểu bằng constructor
        friend PhanSo operator*(PhanSo, PhanSo);
    }

    PhanSo::PhanSo(int x) {
        this->numerator = x;
        this->denominator = 1;
    }

    PhanSo operator*(PhanSo a, PhanSo b) {
            PhanSo newPhanSo(a.numerator * b.numerator, a.denominator * b.denominator);
        return newPhanSo.rutGon();
    }
    ```

- Chuyển kiểu bằng phép toán chuyển kiểu:

    - Khắc phục được nhược điểm của chuyển kiểu bằng constructor
    - **Syntax:** **X::operator T()**   (X là tên class, T là kiểu dữ liệu để chuyển thành)

```cpp
#include <iostream>
using namespace std;

class PhanSo {
private:
    int numerator;
    int denominator;
public:
    PhanSo(int, int);
    operator double() const;
};

PhanSo::PhanSo(int numerator, int denominator = 1) {
    this->numerator = numerator;
    this->denominator = denominator;
}

PhanSo::operator double() const {
    return double(this->numerator) / this->denominator;
}

int main() {
    PhanSo a(1, 2);

    double z = a;
    cout << z;
}

// 0.5
```

- **Sự nhập nhằng**

    - **Xảy ra khi có 2 cơ chế chuyển kiểu** (ví dụ **từ số nguyên sang phân số** và **từ phân số sang số thực**) ⇒ Dẫn đến không xác định là sử dụng function nào ⇒ **Error.**

    ```cpp
    #include <iostream>
    using namespace std;

    int Sum(int a, int b)
    {
        return a+b;
    }
    double Sum(double a, double b)
    {
        return a+b;
    }

    int main() {
        int a = 3, b = 7;
        double r = 3.2, s = 6.3;
        cout << Sum(a,b) << "\n";
        cout << Sum(r,s) << "\n";
        cout << Sum(a,r) << "\n";   // Error: Call to 'Sum' is ambigious
    }
    ```

**Toán tử >> , <<**

```cpp
class ToaDo {
private:
    int x, y;

public:
    ToaDo() {};
    ToaDo(int x, int y) : x(x), y(y) {};

    friend ostream& operator << (ostream &, ToaDo);
    friend istream& operator >> (istream &, ToaDo &);
};

ostream& operator << (ostream &os, ToaDo t) {
    os << "(" << t.x << "; " << t.y << ")";
    return os;
}

istream& operator >> (istream &is, ToaDo &t) {
    is >> t.x >> t.y;
    return is;
}

int main() {
    ToaDo a;
    cin >> a;
    cout << a << endl;
}
```

**Toán tử []**

**Cách viết khác của []** 

```cpp
// CPP program to demonstrate []
// operator
#include <iostream>
using namespace std;
int main()
{
    char name[] = "Ramswarup Tushar Nilesh Subhash";
 
    // Both of the statement prints same thing
    cout << name[5] << endl;
    **cout << 5 [name] << endl;**
    return 0;
}
```

**Viết toán tử []**

```cpp
// Overloading operators for Array class
#include <cstdlib>
#include <iostream>

using namespace std;

// A class to represent an integer array
class Array {
private:
    int* ptr;
    int size;

public:
    Array(int*, int);

    // Overloading [] operator to access elements in array style
    int& operator[](int);

    // Utility function to print contents
    void print() const;
};

// Implementation of [] operator.  This function must return a
// reference as array element can be put on left side
**int& Array::operator[](int index)
{
    if (index >= size) {
        cout << "Array index out of bound, exiting";
        exit(0);
    }
    return ptr[index];
}**

// constructor for array class
Array::Array(int* p, int s = 0)
{
    size = s;
    ptr = NULL;
    if (s != 0) {
        ptr = new int[s];
        for (int i = 0; i < s; i++)
            ptr[i] = p[i];
    }
}

void Array::print() const
{
    for (int i = 0; i < size; i++)
        cout << ptr[i] << " ";
    cout << endl;
}

// Driver program to test above methods
int main()
{
    int a[] = { 1, 2, 4, 5 };
    Array arr1(a, 4);
    arr1[2] = 6;
    arr1.print();
    arr1[8] = 6;
    return 0;
}
```

### Copy constructor

- **Copy constructor** là một constructor tạo đối tượng bằng việc khởi tạo nó với một đối tượng cùng lớp đó mà đã tạo trước đó.
- **Tại sao cần thiết copy constructor**: Nếu một copy constructor không được định nghĩa trong lớp, compiler sẽ tự định nghĩa một copy constructor. Nếu các biến có giá trị con trỏ hay cấp phát bộ nhớ động thì chắc chắn cần phải tự tạo một copy constructor. ⇒ Nếu không tạo một copy constructor thì sẽ xảy ra trường hợp **shallow copy.**
- Để giải quyết vấn đề trên thì phải làm **deep copy.**

    - Trường hợp shallow copy:

    ```cpp
    class String{
        char *p;
    public:
        String(char s[] = "") { p = strdup(s); }
        ~String() { cout <<"delete"<<(void*)p<<"\n"; delete [] p; }
    };

    int main(){
            // Cùng trỏ đến một vùng nhớ (cơ bản thì sử dụng phép gán giống như *p = p)
            // => Lí do cần sử dụng copy constructor
        String a("Nguyen Van A");      // p = 0x7fb2f9d05900
        String b = a;                  // p = 0x7fb2f9d05900
        return 0;
    }

    ```

    - Giải quyết bằng deep copy:

        - Xử lí 2 trường hợp là khi khởi động và khi gán.

        **Lưu ý:**

        - Khi gán thì phải thực hiện 2 thao tác: **dọn dẹp tài nguyên cũ** và **sao chép mới**
        - Trường hợp gán các giá trị ban đầu

    ```cpp
    class String{
        char *p;
    public:
            **// Trường hợp gán các giá trị ban đầu**
        String(char s[] = "") { p = strdup(s); }

            **// Khởi động**
        String(const String &s) {
            p = strdup(s.p);
        }
            
            **// Gán**
        void operator = (const String &s) {
            if (this != &s) {
                delete []p;    // Xóa tài nguyên cũ
                p = strdup(s.p);   // Sao chép mới
            }
        }

        char* getP() {return p;}
        ~String() { cout <<"delete"<<(void*)p<<"\n"; delete [] p; }
    };

    int main(){
            **// Trường hợp gán các giá trị ban đầu**
        String a("Nguyen Van A");    // p = 0x7fe229d04850
        String aa = "Le van AA";     // p = 0x7fe229d04860
            
            **// Khởi động**	
        String b = a;                // p = 0x7fe229d04870
        String c(a);                 // p = 0x7fe229d04880
        String *d = new String(a);   // p = 0x7fe229d04890
            
            **// Gán**    
            aa = a;                      // p = 0x7fe229c051c0

        return 0;
    }
    ```

### Phạm vi truy xuất

- **Public:**
    - Thành phần thuộc thuộc tính public thì có thể truy xuất ở bất cứ nơi nào.
- **Protected:**
    - Cho phép quy định một vài thành phần bảo mật, không cho bên ngoài truy xuất vào, nhưng các lớp con, cháu,… đều được phép truy xuất.
- **Private:**
    - Là riêng tư của lớp đó.
    - Chỉ có hàm thành phần và ngoại lệ là các hàm bạn được phép truy xuất.
    - Các lớp con cũng không có quyền truy cập.

![Untitled](OOP%200025e91fb3df40b2b2fea74d1202ec5e/Untitled%203.png)

**Scope Resolution Operator**

```cpp
#include <iostream>
#include <string>

class Human {
public:
    std::string mess = "Goodbye!";
    void PassMess();
};

// std::string Human::mess = "Goodbye!"; // Error

void Human::PassMess() {
    std::cout << "Truyen tin: " << Human::mess;
}

int main() {
    Human myself;
    myself.mess = "Helo cac dong chi";
    myself.PassMess();
}

// >> Truyen tin: Helo cac dong chi
```

### Từ khóa Const

![Untitled](OOP%200025e91fb3df40b2b2fea74d1202ec5e/Untitled%204.png)

- Nếu khai báo function const thì không được thay đổi thuộc tính của class

### Lưu ý 

- **Lỗi sử dụng vector**
    
    ```cpp
    #include <iostream>
    #include <vector>
    using namespace std;
    
    vector<int> emptyVector{};
    
    class MyHashSet {
    private:
        int SIZE = 1000;
        vector<vector<int>> myBuckets;
        int hashFunction(int x) {
            return x % SIZE;
        }
    
    public:
        MyHashSet() {
            myBuckets.resize(SIZE);
            for (int i = 0; i < myBuckets.size(); i++) {
                myBuckets[i] = emptyVector;
            }
        }
    
        void add(int key) {
            int hasValueIndex = hashFunction(key);
            // Có thể cho nhanh hơn bằng <set>
            vector<int> *bucket = &myBuckets[hasValueIndex];
            vector<int>::iterator index = find(bucket->begin(), bucket->end(), key);
            if (index == bucket->end()) {
                bucket->push_back(key);
            }
    
            cout << myBuckets[1][0]; 
        }
    
        void remove(int key) {
    
        }
    
        bool contains(int key) {
    
        }
    
        vector<vector<int>> getList() {
            return myBuckets;
        }
    
        void main() {
            MyHashSet* container = new MyHashSet();
            container->add(1);
            cout << myBuckets[1][0]; 
            container->add(2);
            container->add(1);
            container->add(3);
            vector<vector<int>> newVector = container->getList();
    
            for (int i = 0; i < newVector.size(); i++) {
                cout << newVector[i].size();
                for (int j = 0 ; j < newVector[i].size(); j++) {
                    cout << "Value: " << i << ' ' << newVector[i][j] << ' ';
                }
                cout << endl;
            }
        }
    
        ~MyHashSet() {
            cout << "Delete done!" << endl;
        }
    };
    
    int main() {
        auto test = new MyHashSet();
        test->main();
        
        delete test;
    }
    ```
    
- **Gán object cho object khác**
    
    ```cpp
    
    int main() {
        Point p, z;
        p.nhap(5, 2);
        z = p;
        cout << &z << endl;
        cout << &p << endl;
    }
    
    // >> 0x7ffee5ffd8b0
    //    0x7ffee5ffd8b8
    ```
    
    ```cpp
    int main() {
        Point p, *z;
        p.nhap(5, 2);
        *z = p;
        cout << &z << endl;
        cout << &p << endl;
    }
    
    // >> 0x7ffee5ffd8b8
    //    0x7ffee5ffd8b8
    ```
    
- **Khai báo 100 bộ nhớ cho 100 object từ class**
    
    ```cpp
    HCN* var = new HCN[100]
    
    p3[10].property
    p3[10].method()
    
    ....
    
    Point arr[200];
    ```
- Cấp phát tĩnh → cung cấp vùng nhớ trong Stack (nhanh nhưng bị hạn chế bộ nhớ) ⇒ ứng dụng cấp phát các biến nguyên thủy (primitive) (int, float, double, …) và kiểu dữ liệu mở rộng (trong namespace std) (string, vector, set, map, …) → tự động giải phóng vùng nhớ khi thoát khỏi scope của hàm chứa nó ⇒ destructor hoạt động
- Cấp phát động → cung cấp vùng nhớ trong Heap (lâu hơn nhưng ko bị hạn chế bộ nhớ) ⇒ ứng dụng để cấp phát cho các biến struct hoặc class (các Attributes and Methods rất lớn) → ko tự động thu hồi bộ nhớ → phải chủ động cung cấp (new) và giải phóng bộ nhớ (delete) ⇒ destructor hoạt động
- struct mặc định là public, class mặc định là private ⇒ nếu ko dùng các access modifier
- Khi lớp con kế thừa từ lớp cha ⇒ sẽ tạo Constructor của lớp cha trước → Constructor của lớp con
    - Ngược lại Destructor lớp con sẽ bị hủy trước rồi mới đến Destructor của lớp cha
- khai báo kiểu cấp phát tĩnh và truyền tham chiếu, hoặc kiểu dữ liệu nguyên thủy hoặc đơn giản đưa vào struct thì truy xuất dùng dấu chấm (.) → student x.ten
- khai báo kiểu cấp phát động truy xuất dùng dấu mũi tên (→) student *x → ten
- Tham số mặc định khi trong hàm thì bắt buộc phải ở cuối cùng và khi truyền ít nhất phải có 1 phần tử có tham số mặc định hoặc là toàn bộ phần tử. Nếu ko đáp ứng được thì bỏ trống ko cần truyền tham số mặc định
- Cấp phát động thì hàm phải có kiểu trả về là còn trỏ và phần tử lưu hàm cũng phải là con trỏ và dùng →
- Overloading ⇒ cùng tên hàm, cùng kiểu trả về nhưng bắt buộc khác tham số (chỉ cần có 1 tham số giống thôi thì bị lỗi ambiguous ngay)
- static <hàm> có thể đc gọi mà ko cần phải tạo object cụ thể ⇒ luôn trả về duy nhất 1 giá trị dù cho object có là gì ⇒ biến static thuộc về class ko thuộc về đối tượng
- Biến static thì mới dùng đc hàm static để gọi chứ ko phải loại biến khác.
- Biến static thì gắn liền với class và đc class quản lý chỉ có vậy thôi chứ nó ko khác gì biến toàn cục (global → có thể dụng ở mọi nơi trong chương trình kể cả class, function) ⇒ có thể thay thế biến static bằng biến global để xử lí tác vụ bình thường
- khi code có phát sinh **các kiểu dữ liệu mở rộng** ít thuộc tính ⇒ dùng **struct thay vì class** (tránh phức tạp và có thể dễ xử lý hơn)
- Constructor ở lớp cha như thế nào thì lớp con xây dựng y chang vậy hoặc phải dùng kiểu để hướng về Constructor khác cụ thể ở lớp cha
- **virtual function** gọi đối tượng có kiểu ở lớp cha nhưng thực hiện được các phương thức cụ thể ở lớp con
- **Abstract Class** ⇒ là lớp cơ sở có ít nhất 1 hàm pure virtual function ( = 0 và ko có cài đặt) và bắt buộc phải được định nghĩa lại ở lớp con kế thừa nó ⇒ quản lý các đối tượng
- **Interface** ⇒ là Abstract Class nhưng toàn bộ tất cả các hàm của nó đều là pure virtual và ko được định nghĩa constructor (vì constructor ko thêm từ khóa virtual vào được)
- **Forward Declaration** ⇒ Liệt kê hết tất cả các class ra để tránh trường hợp cài đặt class trước và sau dẫn đến class này sử dụng đến class kia thì ko hiểu (class Checker; class Person; class Engine;)
- Đối với việc gán giá trị trong Constructor thì đó chỉ đơn giản là thao tác gán giá trị chứ ko phải khởi tạo giá trị hẳn hoi ⇒ đối với các kiểu dữ liệu nguyên thủy thì được nhưng đối với 1 số kiểu dữ liệu đặc biệt thì nó buộc mình sẽ phải khởi tạo ⇒ **phải dùng initialization list**
    - **Constant (Const)** là kiểu dữ liệu ko thể thay đổi giá trị và phải gán cho nó ngay lúc khởi tạo nếu ko gán thì nó sẽ tự nhận 1 giá trị bất kì do hệ điều hành cung cấp và giá trị đó sẽ theo nó trong suốt chương trình
    - **Reference (tham chiếu)** là kiểu dữ liệu nó ko thể thay đổi được kiểu dữ liệu tham chiếu đến các kiểu dữ liệu khác và vì sao phải truyền Reference vào thuộc tính của 1 class vì để đảm bảo tính sở hữu nếu ko truyền Reference thì nó sẽ là thuộc tính của chính class đó thì đó là quan hệ Composition
    - **Array** là một kiểu dữ liệu cũng bắt buộc phải khởi tạo trong Constructor chứ ko phải đi gán lại
- Copy constructor ⇒ copy nội dung của object này sang object kia
    - dùng từ khóa const ⇒ copy dữ liệu với hiệu năng tốt hơn mà ko làm thay đổi dữ liệu gốc khi hoạt động chương trình


# Các câu hỏi ôn thi lí thuyết

## **Câu 1:** Nêu khái niệm về (đóng gói, kế thừa, đa hình, trừu tượng hóa) và ưu điểm của các tính chất trong lập trình. Cho ví dụ minh họa.

### Tính đóng gói

- **Khái niệm:**
    - Các thuộc tính và phương thức được đóng gói trong một thực thể gọi là đối tượng.
    - Ẩn đi các chi tiết triển khai bên trong đối tượng, chỉ cho phép truy cập thông qua các thuộc tính, phương thức công khai.
- **Ưu điểm:**
    - Bảo vệ dữ liệu khỏi truy cập không hợp lệ từ bên ngoài.
    - Dễ bảo trì, có thể tái sử dụng.
- **Ví dụ minh họa:**

```cpp
class Circle {
private:
		float r;
public:
		Circle(float r): r(r) {};
		
		void changeR(float newValue) {
				if (newValue > 0) r = newValue;
		}
		
		float getR() {
				return r;
		}
};

int main() {
    Shape* shape = new Circle(2);
    cout << shape->r;   // Error because its private.
    changeR(3);
    cout << shape->getR();
}
```

### Tính kế thừa

- **Khái niệm:**
    - Cho phép tạo ra một lớp mới từ lớp đã định nghĩa trước đó.
    - Cho phép lớp con kế thừa các thuộc tính và các phương thức từ lớp cha và có thể bổ sung thêm các thành phần mới.
- **Ưu điểm:**
    - Tái sử dụng mã nguồn một cách tối ưu.
    - Cho phép chia sẻ mã chương trình chung ⇒ dễ dàng sửa chữa, nâng cấp hệ thống.
- **Ví dụ minh họa:**

```cpp
class Vehicle {
public:
    void start() {
        std::cout << "Vehicle starting" << std::endl;
    }
};

class Car : public Vehicle {
public:
    void drive() {
        std::cout << "Car driving" << std::endl;
    }
};

int main() {
    Car myCar;
    myCar.start();  // Outputs: Vehicle starting
    myCar.drive();  // Outputs: Car driving
    return 0;
}
```

### Tính đa hình

- **Khái niệm:**
    - Các đối tượng thuộc các lớp khác nhau có thể hiểu cùng một thông điệp nhưng theo các cách khác nhau.
- **Ưu điểm:**
    - Cho phép các đối tượng có hành vi khác nhau cùng sử dụng một giao diện (interface).
    - Dễ mở rộng hệ thống bằng cách thêm lớp mới mà không thay đổi mã hiện có.
    - Dễ dàng thay thế cách triển khai ở các lớp cụ thể mà không ảnh hưởng đến mã khác.
- **Ví dụ minh họa:**

```cpp
class Animal {
public:
    virtual void makeSound() {
        std::cout << "Animal makes sound" << std::endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "Woof" << std::endl;
    }
};

class Cat : public Animal {
public:
    void makeSound() override {
        std::cout << "Meows" << std::endl;
    }
};

int main() {
    Animal* myAnimal = new Dog();
    myAnimal->makeSound();  // Outputs: Woof

    myAnimal = new Cat();
    myAnimal->makeSound();  // Outputs: Meows
}
```

### Tính trừu tượng

- **Khái niệm:**
    - Xác định các thuộc tính và hành vi chung của các đối tượng trong một hệ thống, và thể hiện chúng dưới dạng các khái niệm hoặc mô hình đơn giản hơn *(Tập trung vào các khía cạnh quan trọng nhất của đối tượng, bỏ qua chi tiết không cần thiết).*
- **Ưu điểm:**
    - Giảm độ phức tạp vì chỉ tập trung vào cách thuộc tính và phương thức cần thiết.
- **Ví dụ minh họa:**

```cpp
// Abstract base class
class Shape {
public:
    virtual void tinhCv() = 0;
};

class Circle : public Shape {
		float r;
public:
		Circle(float r): r(r) {};
		
    float tinhCv() override {
        return 2 * 3.14 * r;
    }
};

int main() {
    Shape* shape = new Circle(2);
    float chuVi = shape->tinhCv();
}
```

## **Câu 2:** Phân biệt phạm vi truy xuất private, protected, public. Cho ví dụ minh họa.

- **Public:**
    - Thành phần thuộc thuộc tính public thì có thể truy xuất ở bất cứ nơi nào.
- **Protected:**
    - Cho phép quy định một vài thành phần bảo mật, không cho bên ngoài truy xuất vào, nhưng các lớp con, cháu,… đều được phép truy xuất.
- **Private:**
    - Là riêng tư của lớp đó.
    - Chỉ có hàm thành phần và ngoại lệ là các hàm bạn được phép truy xuất.
    - Các lớp con cũng không có quyền truy cập.

- **Ví dụ minh họa:**

```cpp
class Value {
private:
		int privateValue = 1;
protected:
		int protectedValue = 2;
public:
		int publicValue = 3;
};

class Derived : public Value {
public:
		void xuat() {
				cout << this->privateValue; // Error
				cout << this->protectedValue;  // 2
				cout << this->publicValue;  // 3
		}
};

int main() {
		Value value;
		cout << value.privateValue;   // Error
		cout << value.protectedValue;   // Error
		cout << value.publicValue;   // 3
}
```

## **Câu 3:** Trình bày về kế thừa theo private, protected, public. Cho ví dụ minh họa.

- **Public**:
    - Nếu kế thừa ở dạng này, sau khi kế thừa, tất cả các thành viên dạng `public` lớp cha sẽ `public` ở lớp con, dạng `protected` ở lớp cha vẫn sẽ là `protected` ở lớp con.
- **Protected**:
    - Nếu dùng `protected` thì sau khi kế thừa, tất cả các thành viên dạng `public`, `protected` lớp cha sẽ trở thành `protected` tại lớp con.
- **Private**:
    - Trường hợp ta sử dụng `private`, thì sau khi kế thừa, tất cả các thành viên dạng `public` và `protected` ở lớp cha sẽ thành `private` tại lớp con.

- **Ví dụ minh họa:**

```cpp
class Value {
private:
		int privateValue = 1;
protected:
		int protectedValue = 2;
public:
		int publicValue = 3;
};

class Value1: public Value {};
class Value2: protected Value {};
class Value3: private Value {};
```

## **Câu 4:** Cho biết ý nghĩa, mục đích của các hàm get/set trong một lớp.

- **Mục đích:**
    - Truy vấn dữ liệu được cho phép.
- **Ý nghĩa:**
    - Bảo vệ nguyên tắc đóng gói, chỉ cho phép các dữ liệu có thể truy vấn mới được truy cập đến.
    - Sử dụng truy vấn cho phép kiểm tra trước khi thực hiện thay đổi giá trị.

## **Câu 5:** Phân biệt khái niệm lớp và đối tượng trong lập trình hướng đối tượng. Cho ví dụ minh họa.

|  | Lớp (class) | Đối tượng (object) |
| --- | --- | --- |
| Định nghĩa | - Lớp là một bản thiết kế hoặc khuôn mẫu định nghĩa các thuộc tính và phương thức chung cho một nhóm đối tượng. | - Đối tượng là một thể hiện cụ thể của lớp. Nó chứa dữ liệu cụ thể và có thể thực hiện các hành vi được định nghĩa trong lớp. |
| Mục đích | - Tạo ra các nguyên mẫu cho đối tượng, định nghĩa các thuộc tính và phương thức mà đối tượng của lớp đó có thể có. | - Lưu trữ dữ liệu và tương tác với các phương thức được đĩnh nghĩa trong lớp. |
- **Ví dụ minh họa:**
    - *Này tự viết được @@*

## **Câu 6:** Trình bày khái niệm lớp trừu tượng (abstract class). Hàm ảo là gì, hàm thuần ảo là gì. Cho ví dụ minh họa.

- **Lớp trừu tượng:**
    - Là lớp chứa ít nhất một hàm thuần ảo.
    - Là lớp cơ sở không có đối tượng nào thuộc chính nó *(nghĩa là một lớp không thể tạo đối tượng trực tiếp mà chỉ dùng để làm lớp cơ sở cho các lớp khác kế thừa).*

|  | Hàm ảo (virtual function) | Hàm thuần ảo (pure virtual function) |
| --- | --- | --- |
| Khái niệm | - Là cách thể hiện tính đa hình trong c++.
- Hàm ảo là hàm thành viên của lớp cơ sở, có thể bị ghi đè (override) trong lớp dẫn xuất. | Hàm thuần ảo là hàm ảo không có nội dung. Lớp chứa ít nhất một hàm thuần ảo sẽ thành lớp trừu tượng. |
| Đặc điểm | - Có từ khóa ‘virtual’ trước khai báo phương thức.
- Không bắt buộc định nghĩa lại trong lớp dẫn xuất
- Phương thức ảo chỉ hoạt động thông qua con trỏ. | - Có từ khóa ‘virtual’ trước khai báo cho hàm bằng 0.
- Không có phần nội dung
- Không thể tạo đối tượng từ lớp có chứa hàm thuần ảo.
- Phải được định nghĩa trong lớp dẫn xuất (nếu không lớp dẫn xuất sẽ thành lớp trừu tượng).
 |

- **Ví dụ minh họa:**

```cpp
// Lớp trừu tượng
class Abstract {
public:
		virtual float tinhCv() = 0;   // Hàm thuần ảo
};

class Circle : public Abstract {
private:
		float r = 2;
public:
		float tinhCv() override {
				return 2 * 3.14 * r;
		}
}

class Human {
private:
		string name = "Vinh";
		int age = 18;
public:
		virtual void xuatThongTin() {  // Hàm ảo
				cout << name << age;
		}
}

class SinhVien : public Human {
private:
		string MSSV = "23521793";
public:
		void xuatThongTin() override {
				cout << name << MSSV << age;
		}
}
```

## **Câu 7:** Phân biệt khái niệm overload và override trong lập trình hướng đối tượng.

|  | Override | Overload |
| --- | --- | --- |
| Khái niệm | Là một phương thức cho phép lớp con cung cấp một cách triển khai cụ thể thay cho một phương thức đã được cung cấp bởi lớp cha. | Nạp chồng phương thức đơn giản là có thể sử dụng phương thức trùng tên khác nhau về đối số. Cho phép tạo nhiều phiên bản của một phương thức nhằm thuận lợi cho việc gọi phương thức. |
| Hành vi | Thay đổi hành vi hiện tại của phương thức. | Thêm hoặc mở rộng hành vi của phương thức. |
| Danh sách tham số | Danh sách tham số phải giống nhau | Danh sách tham số khác nhau (số lượng, thứ tự, kiểu dữ liệu). |
| Giá trị trả về | Kiểu trả về bắt buộc giống nhau. | Kiểu trả về có thể khác nhau. |
| Phạm vi  | Xảy ra giữa 2 class có quan hệ kế thừa. | Xảy ra trong phạm vi cùng class. |

**Câu 8:** Trình bày khái niệm hàm bạn, lớp bạn, ưu nhược điểm là gì. Cho ví dụ minh họa.

|  | Hàm bạn (friend function) | Lớp bạn (friend class) |
| --- | --- | --- |
| Khái niệm | Friend function không thuộc lớp nhưng có quyền truy cập private, protected của lớp ⇒ Cách cho phép chia sẻ dữ liệu giữa các đối tượng với một hàm tùy ý trong chương trình. | Friend class có thể truy cập đến các thành phần có thuộc tính private, protected của một class khác. |
| Ưu điểm | Cho phép một hàm truy cập trực tiếp vào dữ liệu riêng tư của đối tượng mà không cần phương thức truy vấn. | Cho phép một lớp truy cập trực tiếp vào dữ liệu riêng tư của đối tượng mà không cần phương thức truy vấn. |
| Nhược điểm | - Vi phạm nguyên tắc đóng gói.
- Tăng sự phụ thuộc giữa hàm và lớp. | - Vi phạm nguyên tắc đóng gói.
 |
- **Ví dụ minh họa:**

```cpp
class Box {
private:
		int width = 10;
public:
		friend void printWidth(Box &box);
		friend class MoreInfo;
}

// Hàm bạn
void printWidth(Box &box) {
		cout << box.width << endl;
}

// Lớp bạn
class MoreInfo {
private:
		int height = 5;
public:
		void printInfo(Box &box) {
				cout << height << ' ' << box.width << endl;
		}
}

int main() {
		Box box;
		MoreInfo info;
		
		printWidth(box);   // 10
		info.printInfo(box);   // 5 10
	
}
```

## **Câu 9:** Nêu khái niệm, vai trò của hàm tạo và hàm hủy trong định nghĩa class. Cho ví dụ minh họa.

|  | Constructor | Destructor |
| --- | --- | --- |
| Định nghĩa | - Là một loại phương thức đặc biệt dùng để khởi tạo một đối tượng cụ thể từ một class. | - Là một loại phương thức đặc biệt được gọi khi một đối tượng bị hủy hoặc kết thúc. |
| Mục đích | Khởi tạo đối tượng. | Giải phóng vùng nhớ. |
| Đặc điểm | - Phương thức trùng với tên lớp, không có kiểu trả về.

- Có thể có tham số, có thể khai báo default parameters.
- Buộc phải có phạm vi public.
- Mỗi lớp có thể có nhiều constructor | - Phương thức trùng tên với tên lớp nhưng bắt đầu bằng ~ , không có kiểu trả về.
- Không có tham số.

- Buộc phải có phạm vi public.
- Mỗi lớp chỉ có một destructor. |

**Trường hợp hỏi có bao nhiêu loại constructor**

- **Có 3 loại constructor sau đây:**
    - Constructor mặc định
    - Constructor có đối số
    - Constructor sao chép

```cpp
class PhanSo {
private:
		int tu;
		int mau;
public:
		// Constructor mặc định
		PhanSo() {};
		
		// Constructor có đối số
		PhanSo(int a. int b): tu(a), mau(b) {};
		
		// Constructor sao chép
		PhanSo(const PhanSo& phanSo) {
				tu = phanSo.tu;
				mau = phanSo.mau;
		}
}
```

- **Trường hợp hỏi có bao nhiêu loại destructor**
    - **Có 3 loại destructor**
        - **Destructor mặc định ***(Khi lớp không quản lý tài nguyên động hoặc các tài nguyên đặc biệt khác.)*
        - **Destructor tự định nghĩa** *(Khi lớp quản lý tài nguyên động hoặc cần thao tác đặc biệt khi đối tượng bị hủy.)*
        - **Destructor ảo** *(Khi lớp có khả năng bị kế thừa và quản lý tài nguyên, bảo đảm gọi đúng destructor trong lớp dẫn xuất.)*
            
            *Nếu cần hiểu thêm về tác dụng và cách sử dụng destructor ảo*
            
            ```cpp
            #include <iostream>
            using namespace std;
            
            class PhanSo {
                int *a = new int(10);
            public:
                virtual ~PhanSo() {
                    delete a;
                    cout << "Destructor called" << endl;
                }
            };
            
            class PhanSoNew : public PhanSo {
            public:
                ~PhanSoNew() {
                    cout << "CALL FOR NEW" << endl;
                }
            };
            
            int main() {
                PhanSo *phanSo = new PhanSoNew();
                delete phanSo;  // Se goi destructor cua ca 2 class, binh thuong goi moi cua PhanSo
            }
            ```
            
    
    ```cpp
    // Destructor mặc định
    class PhanSo() {
    		int a = 10;
    public: 
    		~PhanSo() {};
    }
    
    // Destructor tự định nghĩa
    class PhanSo {
    		int *a = new int(10);
    public:
    		~PhanSo() {
    				delete a;
    				cout << "Destructor called" << endl;
    		}
    }
    
    // Destructor ảo
    class PhanSo {
    public:
    		virtual ~PhanSo() {
    				cout << "Destructor called" << endl;
    		}
    }
    ```
    
- **Ví dụ minh họa:**

```cpp
class Human {
private:
		int *age;
public:
		// Phương thức thiết lập
		Human(int age): age(new int(age)) {};
		
		// Phương thức hủy
		~Human() {
				delete age;
				cout << "Destructor!!" << endl;
		}
}
```

## **Câu 10:** Khái niệm hàm copy constructor và hàm gán. Tại sao cần sử dụng 2 hàm đó. Cho ví dụ minh họa.

|  | Copy constructor | Hàm gán |
| --- | --- | --- |
| Khái niệm | Là một constructor đặc biệt được dùng để tạo một đối tượng mới từ một đối tượng đã tồn tại cùng kiểu. | Là một toán tử đặc biệt được dùng để gán giá trị của một đối tượng đã tồn tại cho một đối tượng khác đã tồn tại cùng kiểu. |
| Vai trò | - Tạo bản sao của tài nguyên

- Quản lí tài nguyên động và các tài nguyên đặc biệt, tránh trường hợp bị shallow copy. | - Giải phóng tài nguyên cũ, sao chép tài nguyên mới.
- Quản lí tài nguyên động và các tài nguyên đặc biệt, tránh trường hợp bị shallow copy. |
- **Ví dụ minh họa:**

```cpp
class Value {
		int *a;
public:
		Value(int x): a(new int(x)) {};
		
		// Copy constructor
		Value(const Value &value) {
				a = new int(*(value.a));
		}
		
		// Hàm gán
		void operator = (const Value &value) {
				if (this != &value) {
						delete a;
						a = new int(*(value.a));
				}
		}
}
```

## **Câu 11:** Property, method là gì. Cho ví dụ minh họa.

- **Property:**
    - Là các giá trị mô tả trạng thái đối tượng, chứa thông tin về các tính chất hoặc đặc điểm của đối tượng đó.
- **Method:**
    - Là một **function được định nghĩa ở trong class** để thực hiện một hành động cụ thể hoặc thực hiện một loạt các hành động với các property của object của class đó. Nó có quyền truy cập các thành phần private, protected của đối tượng cùng class đó.

- **Ví dụ minh họa:**

```cpp
class Human {
private:
		// Property
		string name = "Vinh";
		int age = 18;
public:
		// Method
		int nextAge() {
				return age + 1;
		}
}
```

## **Câu 12:** Khái niệm con trỏ this. Cho ví dụ minh họa.

- **Con trỏ this:**
    - Là một con trỏ đặc biệt chỉ tồn tại trong phạm vi methods của một class.
    - Trỏ đến object hiện tại mà method đó đang thao tác.
    - Giúp phân biệt biến ở trong object hay tham số của method nếu trùng tên.

```cpp
class PhanSo {
private:
    int tu, mau;
public:
    PhanSo() {};
    PhanSo(int tu, int mau) {
	       this->tu = tu;
	       this->mau = mau;
    }
};
```

## **Câu 13:** Trình bày về static member (thành viên tĩnh). Cho ví dụ minh họa.

- **Static member:**
    - Static dùng để khai báo biến, method dùng chung cho class, **chỉ có một bản duy nhất tồn tại trong suốt quá trình chạy.**
    - Các static member có thể là **public**, **private**, **protected**.
    - Static cũng là một member của class, vậy nên **có quyền truy cập tất cả.**

- **Ví dụ minh họa:**

```cpp
class Count {
private:
		static int count;
public:
		Count() {
				count++;
		}
		
		int getCount() {
				return count;
		}
};

int Count::count = 0;

int main() {
		Count c1, c2, c3;
		cout << c1.getCount();   // 3
}
```

## **Câu 14:** Trình bày về con trỏ chuyển kiểu tự động trong kế thừa. Cho ví dụ minh họa.

- **Con trỏ chuyển kiểu tự động trong kế thừa hoạt động theo nguyên tắc:**
    - Con trỏ trỏ đến các đối tượng thuộc lớp cơ sở thì có thể trỏ đến các đối tượng thuộc lớp con. Nhưng con trỏ trỏ đến các đối tượng thuộc lớp con thì không thể trỏ đến các đối tượng thuộc lớp cơ sở.

- **Ví dụ minh họa:**

```cpp
class Human {
		string name = "Vinh";
		int age = 18;
public:
		virtual xuat() {};
};

class SinhVien : public Human {
		string MSSV = "23521793";
public:
		xuat() {
				cout << name << ' ' << MSSV << ' ' << age;
		}
};

int main() {
		Human *sv = new SinhVien();
		sv.xuat();   // Vinh 23521793 18
}
```

## **Câu 15:** So sánh chuyển kiểu bằng constructor và chuyển kiểu bằng toán tử chuyển kiểu. Cho ví dụ minh họa.

|  | Chuyển kiểu bằng constructor | Chuyển kiểu bằng operator |
| --- | --- | --- |
| Cách chuyển | Chuyển từ một kiểu đã có (int, float, …) sang kiểu đang định nghĩa (phân số, đa thức, …) | Chuyển từ kiểu đang định nghĩa sang kiểu đã có |
| VD | PhanSo (int x) {
        tu = x;
        mau = 1;
} | PhanSo::operator double() const {
        return (double(this→tu) / this→mau);
} |