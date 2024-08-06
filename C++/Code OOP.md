# Code OOP
## Struct
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
## Cấp phát tĩnh
- Cài đặt ban đầu :
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
class student : public person{ 
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
    //error
    void output(){ 
     cout << ten << ' ' << address << ' ' << fixed << setprecision(2) << gpa;
    }

    //fuction overiding => cùng tên, cùng kiểu trả về, cùng ds tham số
    void output(){
        //gọi hàm output() của lớp cha để in các thuộc tính của lớp cha + ghi đè thêm thông tin lớp con
        person::output();
        cout << fixed << setprecision(2) << gpa;
    }
};

//Polymorphism + inheritance
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
        // ko cần get set vì mode protected
        return length * width; 
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
        // call a function in base class and improve or define again
        vehicle::run(); 
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
//pure virtual function => must be defined again in sub class to initalize and use
//usually don't create Constructor using virtual
class person{
protected:
    string name;
public:
    //Abstract Class => at least 1 pure virtual 
    //Interface => all functions in class are pure virtual
    virtual string getName() = 0;
    virtual void setName(string name) = 0;
    virtual void greeting() = 0;
    
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
    // up casting to Car by assigning => vehicle* v = (vehicle*)Car;
    vehicle* v = Car; 
    //((car*)v)->run(); => down casting 
    v->run(); 
    //Manage a list of sub class inheriated base class
    vehicle* list[2];
    list[0] = new car();
    list[1] = new truck();
    for(int i = 0; i < 2; i++) list[i]->run();
    // cannot initalize (dont use general object in real life => must be specific object)
    person* p = new person(); 
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
    //pass by pointer => don't need to have first value
    person* owner; 
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
        onwer = other.getOwner();
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
    //pass by reference => need to have first value => use initialization list
    otherPerson &otherOwner;  
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
    ~taxi2(){delete Engine} => free up the memory for program
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
    truck(string s, registerInfo info) : truckName(s), license(info.license), ownerName(info.ownerName){}
    //pass by reference of pointer => inficient time because it will copy the name of memory allocation of value passed before => use for class or struct
    //string also a class
    truck(string& s, registerInfo& info) : truckName(s), license(info.license), ownerName(info.ownerName){} 
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
    
