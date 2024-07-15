# Tính chất của OOP

## Abstraction

- Tính trừu tượng là khái niệm mà các đối tượng và lớp được thiết kế để đại diện cho các khái niệm hoặc thực thể trong thế giới thực một cách trừu tượng. Tính trừu tượng giúp giảm sự phức tạp bằng cách tập trung vào các đặc điểm quan trọng và bỏ qua các chi tiết không quan trọng.
- **Đặc điểm chính:**
    - **Tập trung vào giao diện chính và giảm sự phức tạp:** Tính trừu tượng cho phép tập trung vào các khái niệm hoặc chức năng chung mà không cần quan tâm đến chi tiết cụ thể.
    - **Tăng tính linh hoạt và tái sử dụng**: Tính trừu tượng cho phép tạo ra các lớp và đối tượng có thể tái sử dụng được, vì chúng không phụ thuộc quá nhiều vào chi tiết cụ thể của triển khai.
    - **Cung cấp giao diện chung:** Các lớp và đối tượng trừu tượng thường cung cấp một giao diện chung mà các lớp con có thể kế thừa và triển khai. ⇒ Giúp tạo hệ thống linh hoạt và dễ mở rộng.

## Encapsulation

- **Tính đóng gói** là khái niệm trong lập trình hướng đối tượng mà trong đó các thuộc tính và phương thức được đóng gói lại với nhau trong một thực thể gọi là đối tượng (object). ⇒ Các chi tiết triển khai bên trong của một đối tượng được giấu kín và chỉ những phần cần thiết công khai thì mới công khai. Tính đóng gói giúp bảo vệ dữ liệu bên trong đối tượng khỏi sự can thiệp và sử dụng sai cách từ bên ngoài, đồng thời tạo ra một cấu trúc rõ ràng, dễ bảo trì và mở rộng.

## Inheritance

- **ĐỀ BÀI**
![Screen Shot 2024-04-22 at 07.51.18.png](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Screen_Shot_2024-04-22_at_07.51.18.png)
    - **Trước khi kế thừa:**
    ![Untitled 5](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%205.png)
    - **Sau khi kế thừa:**
    ![Untitled 6](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%206.png)

- **Quan hệ đặc biệt hóa - tổng quát hóa**
    -**Hai lớp đối tượng có quan hệ đặc biệt này khi:** lớp của đối tượng này là trường hợp đặc biệt của lớp đối tượng kia và lớp của đối tượng kia là trường hợp tổng quát của lớp đối tượng này.
    ![Untitled 7](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%207.png)
    - Kế thừa là một đặc điểm của ngôn ngữ dùng để **biểu diễn mối quan hệ đặc biệt hóa - tổng quát hóa giữa các lớp.**
    - Tính kế thừa cho phép **xây dựng một lớp mới dựa trên các định nghĩa của lớp đã có**, nghĩa là lớp cha có thể chia sẻ dữ liệu và phương thức cho các lớp con ⇒ Các lớp con khỏi phải định nghĩa lại, ngoài ra có thể bổ sung thêm các thành phần mới *( tái sử dụng mã nguồn 1 cách tối ưu, tận dụng được mã nguồn ).*
        - Lớp mới gọi là **lớp con (subclass)** hay **lớp dẫn xuất (derived class).**
        - Lớp đã có gọi là **lớp cha (superclass)** hay **lớp cơ sở (base class).**
    - **Đặc tính:** Thừa kế cho phép
        - **Nhiều lớp** có thể dẫn xuất từ **một lớp cơ sở**.
        - **Một lớp** có thể là dẫn xuất của **nhiều lớp cơ sở**.
        - Thừa kế không giới hạn ở một mức: Một lớp dẫn xuất có thể là lớp cơ sở cho các lớp dẫn xuất khác.
    - **Lợi ích:**
        - Cho phép xây dựng lớp mới từ lớp đã có.
        - Cho phép chia sẻ mã chương trình chung ⇒ dễ dàng sửa chữa, nâng cấp hệ thống.
        - Trong c++, kế thừa còn định nghĩa sự tương thích, nhờ đó ta có cơ chế chuyển kiểu tự động.
    - **Lưu ý:**
        - Khi lớp con kế thừa từ lớp cha ⇒ sẽ tạo Constructor của lớp cha trước → Constructor của lớp con.
        - Ngược lại Destructor lớp con sẽ bị hủy trước rồi mới đến Destructor của lớp cha.
    - **Syntax:**

    ```cpp
    class SuperClass {
        // Thành phần lớp cơ sở
    };

    class DerivedClass : public/protected/private SuperClass {
        // Thành phần bổ sung của lớp xuất dẫn
    };
    ```

- **Mức độ truy cập thành viên của class (Phạm vi truy xuất)**

    ![Untitled 8](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%208.png)

    ![Untitled 9](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%209.png)

    - **public**: Nếu kế thừa ở dạng này, sau khi kế thừa, tất cả các thành viên dạng `public` lớp cha sẽ `public` ở lớp con, dạng `protected` ở lớp cha vẫn sẽ là `protected` ở lớp con.
    - **protected**: Nếu dùng `protected` thì sau khi kế thừa, tất cả các thành viên dạng `public` lớp cha sẽ trở thành `protected` tại lớp con.
    - **private**: Trường hợp ta sử dụng `private`, thì sau khi kế thừa, tất cả các thành viên dạng `public` và `protected` ở lớp cha sẽ thành `private` tại lớp con.

```cpp
class ConNguoi {
protected:
    string name;
    int age;
    int yearOfBirth;

public:
    ConNguoi() {};
    ConNguoi(string name, int age, int yearOfBirth) : name(name), age(age), yearOfBirth(yearOfBirth) {};

    void xuatInfo() {
        printf("%20s %5d %8d", name.c_str(), age, yearOfBirth);
    }
};

class SinhVien : public ConNguoi {
protected:
    string maSV;
    
public:
    SinhVien() {};
    SinhVien(string name, int age, int yearOfBirth, string maSV) : ConNguoi(name, age, yearOfBirth), maSV(maSV) {};
};

```

- Chuyển kiểu tự động (con trỏ và kế thừa)

    - Con trỏ trong kế thừa hoạt động theo nguyên tắc:
    - Con trỏ **trỏ đến đối tượng thuộc lớp cơ sở** thì **có thể trỏ đến các đối tượng thuộc lớp con**.
    - Con trỏ **trỏ đến đối tượng thuộc lớp con** thì **không thể trỏ đến đối tượng thuộc lớp cơ sở**.

- **Lưu ý:** 

    - Những thuộc tính và method còn lại **đều bị ẩn** đi chứ không bị xóa, nếu sử dụng **virtual** và **override** thì có thể hiện đè được hàm trùng tên ở lớp cơ sở.

```cpp
NVVP *nvvp1 = new NVVP("23521793", "Pham Hoang Vinh", 10e6, 23);
NhanVien *nhanvien = nvvp1;
cout << nhanvien << " " << nvvp1;  // Trỏ đến đúng 1 vùng nhớ
```

- Đa kế thừa:
    - Đa kế thừa cho phép một lớp có thể là dẫn xuất của nhiều lớp cơ sở.
    - Các đặc điểm của kết thừa đơn vẫn đúng cho trường hợp đa kế thừa.

```cpp
class DerivedClass : **public SuperClass1**, **protected SuperClass2** {
    // Thành phần bổ sung của lớp xuất dẫn
};
```

## Polymorphism

- **Đa hình** : là hiện tượng **các đối tượng thuộc các lớp khác nhau** có thể **hiểu cùng một thông điệp** nhưng **theo các cách khác nhau**.

    - Tính đa hình xuất hiện **khi có sự kế thừa giữa các lớp**.
    - Có **phương thức tổng quát ở lớp cơ sở**, nhưng **nội dung của nó chỉ được xác định ở các lớp dẫn xuất cụ thể.**
    - Ví dụ : Phương thức tính diện tích của hình tam giác, hình vuông, …

- **Phương thức ảo**

    - Là cách thể hiện tính đa hình trong c++
    - Các phương thức ở lớp cơ sở có tính đa hình phải được định nghĩa là một phương thức ảo.

    - **Con trỏ thuộc lớp cơ sở có thể trỏ đến lớp con :**

    ```cpp
    **NhanVien** *p = new **NVSX**("23234122", "Nefieowjdw fewfc", 10e6, 32);
    p->printfNv();  // Goi ham cha

    NVVP nvvp1("23521793", "Pham Hoang Vinh", 10e6, 23);
    nvvp1.printfNv();   // Goi ham con
    nvvp1.NhanVien::printfNv();   // Goi ham cha
    ```
    ⇒ Ta muốn thông qua con trỏ thuộc lớp cơ sở có thể truy xuất hàm thành phần được định nghĩa lại ở lớp con.
    *(như VD trên ta mong muốn gọi printfNv của NVSX nhưng lại gọi printfNv của NhanVien)* 
        ⇒ **Phương thức ảo để giải quyết vấn đề này**

        - Ta quy định một hàm thành phần là **phương thức ảo** bằng các **thêm từ khóa virtual vào trước khi khai báo hàm**.
        - Thêm một loại đối tượng mới mà không cần sửa đổi thao tác xử lí, quy trình thêm chỉ là xây dựng lớp con kế thừa cơ sở và định nghĩa lại phương thức (ảo) ở lớp mới.

        ```cpp
        #include <iostream>
        using namespace std;

        class Nguoi {
        protected:
            string name;
            int age;

        public:
            Nguoi() {};
            Nguoi(string name, int age): name(name), age(age) {};

            **virtual** void xuat() {
                printf("Name: %s, age: %d", name.c_str(), age);
            }
        };

        class SinhVien: public Nguoi {
        private:
            string MS;

        public:
            SinhVien() {};
            SinhVien(string name, int age, string MS): Nguoi(name, age), MS(MS) {};

            void xuat() **override** {
                printf("Name: %s, age: %d, MSSV: %s", name.c_str(), age, MS.c_str());
            }
        };
        ```

    - **Lưu ý:**

        - **Phương thức ảo chỉ hoạt động thông qua con trỏ.**
        - Muốn một hàm trở thành phương thức ảo có 2 cách:
            - Khai báo với **từ khóa là virtual**
            - Hoặc phương thức tương ứng ở lớp cơ sở đã là phương thức ảo
        - Phương thức ảo chỉ hoạt động nếu các **phương thức ở lớp cơ sở và lớp con có cùng tên**.
        - Nếu ở lớp con định nghĩa lại phương thức ảo thì sẽ gọi phương thức ở lớp cơ sở (gần nhất có định nghĩa). **??**

    - **Cơ chế:**

        - Để thực hiện cơ chế đa hình, **mỗi đối tượng được gán một bảng phương thức ảo** (virtual method table hoặc vtable). Bảng này **chứa địa chỉ của các phương thức ảo** mà đối tượng có thể gọi. Khi đối tượng được tạo, trình biên dịch sẽ tự động khởi tạo bảng phương thức ảo này.
        - Khi gọi phương thức **`xuat()`** trên một đối tượng thuộc lớp **`Nguoi`**, hàm **`Nguoi::xuat()`** sẽ được gọi. Trong khi đó, khi gọi phương thức **`xuat()`** trên một đối tượng thuộc lớp **`SinhVien`**, hàm **`SinhVien::xuat()`** sẽ được gọi thay vì hàm **`Nguoi::xuat()`**, điều này cho phép lớp dẫn xuất **`SinhVien`** "ghi đè" (override) hành vi của phương thức ảo từ lớp cơ sở **`Nguoi`** hiện thông qua con trỏ, hàm có địa chỉ trong bảng phương thức ảo sẽ được gọi.
            
            *(Giải thích theo ý hiểu: Khi tạo class Nguoi, sẽ có một bảng virtual chứa phương thức ảo, và **khi SinhVien kế thừa, cũng sẽ có bảng phương thức ảo** đó, việc ta cần làm là tạo một class trùng tên (trùng tên thì sẽ thành virtual như cơ thế trở thành phương thức ảo đã nói trên) thì nó sẽ được cho lại vào bảng virtual của SinhVien và ghi đè lại của Nguoi, nên mới gọi được của SinhVien.)*
    

- **Phương thức thuần ảo**

    ⇒ Mục đích thay thế cho nội dung không có ý nghĩa. **Phương thức ảo thuần túy** là **phương thức ảo không có nội dung**.

    - **Khi lớp có phương thức ảo thuần túy**, **lớp trở thành lớp cơ sở trừu tượng (abstract - tính trừu tượng)**. Ta **không thể tạo đối tượng thuộc lớp này**.
    - Ta có thể định nghĩa phương thức ảo thuần túy, nhưng chỉ có các đối tượng con có thể gọi nó. Khi một lớp con kế thừa từ lớp cơ sở chứa một phương thức ảo thuần túy, **lớp con phải cung cấp cài đặt cho phương thức đó**. Nếu không, **lớp con sẽ trở thành một lớp trừu tượng và không thể khởi tạo đối tượng từ lớp đó.**

    ![Untitled 9](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%209.png)

    ![Untitled 10](https://github.com/nguyentranngocty/Coding_skills/blob/main/C%2B%2B/Image/Untitled%2010.png)

    - Ví dụ như Shape là lớp cơ sở, Rectangle, Triangle, … là lớp dẫn xuất, khai báo Shape là phương thức ảo thuần túy đảm bảo không thể tạo đối tượng thuộc lớp Shape.

    Giải thích dễ hiểu : Phương thức ảo thuần túy có ý nghĩa cho việc tổ chức sơ đồ phân cấp các lớp, nó đóng vai trò chừa sẵn chỗ trống cho các lớp con điền vào với phiên bản phù hợp.
