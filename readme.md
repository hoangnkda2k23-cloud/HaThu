# BUỔI 1: CÚ PHÁP CƠ BẢN, BIẾN, KIỂU DỮ LIỆU & ÉP KIỂU

---

## 1. MỤC TIÊU BUỔI HỌC & TRỌNG TÂM LẤY ĐIỂM
* **Kiến thức cốt lõi:** Nắm vững các kiểu dữ liệu nền tảng (`int`, `long long`, `float`/`double`, `string`), cú pháp vào/ra chuẩn từ bàn phím, cơ chế ép kiểu (Type Casting).
* **Trọng tâm đề thi:** Câu 1 trong đề thi HSG Tin học THCS (thường chiếm 5 – 6 điểm)[cite: 2, 4]. Đây là câu gỡ điểm cơ bản, yêu cầu tính toán chính xác, tuyệt đối không được sai cú pháp hay tràn số[cite: 4, 6].
* **2 bẫy dữ liệu học sinh hay mất điểm:**
  1. **Bẫy chia số nguyên:** Trong C++, phép tính `5 / 2` cho ra kết quả `2` (bị cắt cụt phần thập phân); bắt buộc phải ép kiểu `(double)5 / 2` mới ra `2.5`[cite: 6, 8, 171, 173]. Trong Python, phép chia `/` tự động trả về số thực, nhưng học sinh cần lưu ý phép chia lấy phần nguyên `//`[cite: 6, 9, 171, 174].
  2. **Bẫy tràn số nguyên (Integer Overflow):** Kiểu `int` 32-bit chỉ lưu trữ tối đa khoảng $2 \times 10^9$[cite: 6, 171]. Tích của hai số $10^5 \times 10^5 = 10^{10}$ sẽ tràn kiểu `int` và sinh ra số rác; bắt buộc dùng `long long` trong C++[cite: 6, 17, 171, 182].

---

## 2. HIỆP 1: LÝ THUYẾT & THỊ PHẠM (55 PHÚT)

### 2.1. Khởi động (10 phút)
* **Câu hỏi 1:** Máy tính lưu trữ số nguyên và số thực khác nhau như thế nào? Tại sao lưu $10$ vào biến số thực lại thành $10.0$?
* **Câu hỏi 2:** Giả sử cạnh hình vuông $A = 100\,000$, diện tích $S = A \times A$. Nếu khai báo `int S = A * A;` trong C++ thì máy tính in ra kết quả đúng hay sai? Vì sao?

### 2.2. Bản chất kiến thức mới (15 phút)
* **Bản chất của biến & kiểu dữ liệu:** Biến là một ô nhớ có tên định danh trong bộ nhớ RAM; kiểu dữ liệu quy định dung lượng ô nhớ và cách máy diễn giải dãy bit nhị phân bên trong[cite: 6, 171].
* **Ẩn dụ thực tế:** Kiểu dữ liệu giống như các loại thùng chứa (thùng 2 lít, thùng 8 lít). Rót nước từ thùng lớn sang thùng nhỏ sẽ bị tràn (tràn số); rót từ thùng chứa chất rắn sang thùng lỏng cần dùng phễu chuyển đổi (ép kiểu).
* **Bảng quy chuẩn kiểu dữ liệu:**
  * **Số nguyên nhỏ:** `int` (4 bytes, phạm vi $[-2 \cdot 10^9, 2 \cdot 10^9]$)[cite: 6, 171].
  * **Số nguyên lớn:** `long long` trong C++ (8 bytes, lên tới $\approx 9 \cdot 10^{18}$)[cite: 6, 171]. Trong Python, kiểu số nguyên tự động co giãn kích thước theo giá trị[cite: 6, 74, 171, 239].
  * **Số thực:** `double` (C++) hoặc `float` (Python), đảm bảo độ chính xác phần thập phân[cite: 6, 171].

### 2.3. Thị phạm thuật toán mẫu (30 phút)
* **Bài toán:** Nhập 2 số $A, B$ từ bàn phím. In ra Tổng, Hiệu, Tích và Thương ($A/B$ lấy độ chính xác số thực)[cite: 8, 173].
* **Luồng chạy:** Nhập $A, B$ $\rightarrow$ Tính tổng, hiệu, tích $\rightarrow$ Ép kiểu số hạng sang thực trước khi chia $\rightarrow$ Xuất kết quả kèm định dạng[cite: 8, 9, 173, 174].

#### Code C++:
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    long long a, b;
    cin >> a >> b;
    cout << "Tong: " << a + b << "\n";
    cout << "Hieu: " << a - b << "\n";
    cout << "Tich: " << a * b << "\n";
    // Ép kiểu biến a sang double để phép chia trả về số thực
    cout << "Thuong: " << fixed << setprecision(2) << (double)a / b << "\n";
    return 0;
}
# BUỔI 2: CẤU TRÚC RẼ NHÁNH & BIỂU THỨC LOGIC

---

## 1. MỤC TIÊU BUỔI HỌC & TRỌNG TÂM LẤY ĐIỂM
* **Kiến thức cốt lõi:** Nắm vững các toán tử quan hệ (`==`, `!=`, `<`, `<=`, `>`, `>=`), toán tử logic (`&&`/`and`, `||`/`or`, `!`/`not`), và cấu trúc rẽ nhánh `if / elif / else` (Python) hoặc `if / else if / else` (C++)[cite: 12, 13, 14, 177, 178, 179].
* **Trọng tâm đề thi:** Chiếm trọn điểm ở các bài toán phân loại điều kiện, xét trường hợp biên (tam giác, năm nhuận, tính tiền lũy tiến) thường xuất hiện trong Bài 1 và Bài 2 của đề thi HSG[cite: 4, 12, 16, 177, 181].
* **2 bẫy dữ liệu học sinh hay mất điểm:**
  1. **Nhầm toán tử gán `=` với toán tử so sánh `==`:** Viết `if (a = b)` trong C++ không báo lỗi biên dịch mà sẽ gán giá trị của `b` cho `a`, khiến luồng rẽ nhánh bị sai hoàn toàn.
  2. **Sai thứ tự ưu tiên giữa `&&` và `||`:** Toán tử `&&` luôn được ưu tiên tính trước `||`[cite: 13, 178]. Nếu không đóng mở ngoặc rõ ràng khi kết hợp nhiều điều kiện, biểu thức sẽ cho kết quả sai[cite: 13, 15, 178, 180].

---

## 2. HIỆP 1: LÝ THUYẾT & THỊ PHẠM (55 PHÚT)

### 2.1. Khởi động (10 phút)
* **Câu hỏi 1:** Làm thế nào để kiểm tra một số nguyên $x$ nằm ngoài đoạn $[10, 20]$ bằng Python và C++[cite: 13, 178]?
* **Câu hỏi 2:** Cấu trúc `if ... else if ... else` khác gì so với việc viết nhiều lệnh `if ... if ... if` độc lập[cite: 19, 184]?

### 2.2. Bản chất kiến thức mới (15 phút)
* **Bản chất rẽ nhánh:** Máy tính đánh giá biểu thức điều kiện từ trên xuống dưới[cite: 19, 184]. Khi gặp điều kiện đầu tiên trả về `True`, khối lệnh tương ứng sẽ được thực thi và toàn bộ các nhánh `elif`/`else if`/`else` phía sau lập tức bị bỏ qua[cite: 19, 184].
* **Ẩn dụ thực tế:** Cấu trúc rẽ nhánh giống như một ngã rẽ đường ray xe lửa[cite: 14, 179]. Khi cần gạt đã bẻ sang một nhánh, đoàn tàu chỉ chạy vào nhánh đó và không thể đi vào các đường ray còn lại[cite: 19, 184].
* **Bảng toán tử logic chuẩn:**
  * **Và (AND):** `&&` (C++) / `and` (Python) – Chỉ đúng khi tất cả điều kiện đều đúng[cite: 13, 178].
  * **Hoặc (OR):** `||` (C++) / `or` (Python) – Đúng khi có ít nhất một điều kiện đúng[cite: 13, 178].
  * **Phủ định (NOT):** `!` (C++) / `not` (Python) – Đảo ngược giá trị logic[cite: 13, 178].

### 2.3. Thị phạm thuật toán mẫu (30 phút)
* **Bài toán:** Nhập vào năm nguyên dương $N$. Kiểm tra xem $N$ có phải là năm nhuận hay không[cite: 15, 180].
* **Quy tắc toán học:** Năm nhuận là năm chia hết cho 400 HOẶC (chia hết cho 4 và KHÔNG chia hết cho 100)[cite: 15, 180].
* **Luồng chạy:** Nhập số nguyên $N$ $\rightarrow$ Kiểm tra biểu thức `(N % 4 == 0 && N % 100 != 0) || (N % 400 == 0)` $\rightarrow$ Xuất kết luận[cite: 16, 181].

#### Code C++:
```cpp
#include <iostream>
using namespace std;

int main() {
    int nam;
    cin >> nam;
    
    // Kiểm tra theo đúng thứ tự ưu tiên logic
    if ((nam % 4 == 0 && nam % 100 != 0) || (nam % 400 == 0)) {
        cout << "Nam " << nam << " la nam nhuan.\n";
    } else {
        cout << "Nam " << nam << " KHONG phai nam nhuan.\n";
    }
    return 0;
}
# BUỔI 3: CẤU TRÚC LẶP & THUẬT TOÁN SỐ HỌC CƠ BẢN

---

## 1. MỤC TIÊU BUỔI HỌC & TRỌNG TÂM LẤY ĐIỂM
* **Kiến thức cốt lõi:** Nắm vững cấu trúc vòng lặp xác định (`for`), vòng lặp không xác định (`while`), vòng lặp lồng nhau, cùng cơ chế điều khiển `break` và `continue`[cite: 19, 20, 184, 185].
* **Trọng tâm đề thi:** Chiếm trọn điểm ở các bài toán xử lý chuỗi chữ số, tính tổng/tích dãy số có quy luật, và duyệt các bài toán số học cơ bản (ước số, số nguyên tố) thường gặp ở Câu 1 và Câu 2 đề thi HSG[cite: 4, 19, 22, 184, 187].
* **2 bẫy dữ liệu học sinh hay mất điểm:**
  1. **Lỗi lặp vô tận (Infinite Loop):** Trong vòng lặp `while`, quên cập nhật biến điều khiển (quên tăng/giảm biến đếm hoặc quên chia nguyên `N /= 10`), dẫn đến chương trình chạy mãi không dừng và bị chấm 0 điểm do quá thời gian (TLE)[cite: 3, 20, 185].
  2. **Bẫy chia nguyên khi tính tổng số thực:** Khi tính tổng dãy phân số kiểu $1/i$, nếu viết `1 / i` trong C++ thì máy tính hiểu là chia hai số nguyên (kết quả ra 0 với mọi $i > 1$); bắt buộc phải ép kiểu `1.0 / i` hoặc `(double)1 / i`[cite: 22, 187].

---

## 2. HIỆP 1: LÝ THUYẾT & THỊ PHẠM (55 PHÚT)

### 2.1. Khởi động (10 phút)
* **Câu hỏi 1:** Khi nào ta nên ưu tiên dùng vòng lặp `for`, và khi nào bắt buộc phải dùng vòng lặp `while`[cite: 25, 190]?
* **Câu hỏi 2:** Lệnh `break` và `continue` khác nhau như thế nào khi đứng bên trong thân một vòng lặp[cite: 20, 185]?

### 2.2. Bản chất kiến thức mới (15 phút)
* **Bản chất của vòng lặp:** Lặp đi lặp lại một khối công việc khi điều kiện lặp còn đúng; `for` dùng khi biết trước số lần lặp hoặc duyệt qua tập hợp, còn `while` dùng khi điều kiện dừng phụ thuộc vào dữ liệu biến đổi bên trong[cite: 19, 20, 25, 184, 185, 190].
* **Kỹ thuật tách chữ số của một số nguyên:**
  * Lấy chữ số hàng đơn vị: `chu_so = N % 10`
  * Bỏ chữ số hàng đơn vị: `N = N / 10` (chia lấy phần nguyên)
  * Điều kiện lặp: Tiếp tục thực hiện khi `N > 0`.
* **Ẩn dụ thực tế:** Vòng lặp `while` bóc tách từng chữ số giống như việc bạn bóc từng lớp của một củ hành tây: lột lớp ngoài cùng (`% 10`), vứt bỏ lớp đó đi (`/ 10`), và tiếp tục cho đến khi củ hành không còn gì (`N == 0`).

### 2.3. Thị phạm thuật toán mẫu (30 phút)
* **Bài toán:** Nhập số nguyên dương $N$. Tính tổng $S = 1 + \frac{1}{2} + \frac{1}{3} + \dots + \frac{1}{N}$ và in kết quả làm tròn đến 4 chữ số thập phân[cite: 22, 187].
* **Luồng chạy:** Nhập $N$ $\rightarrow$ Khởi tạo $S = 0.0$ $\rightarrow$ Dùng vòng lặp `for` chạy $i$ từ $1$ đến $N$ $\rightarrow$ Cộng dồn $1.0 / i$ vào $S$ $\rightarrow$ Xuất $S$ định dạng 4 số thập phân[cite: 22, 187].

#### Code C++:
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    int n;
    cin >> n;
    double s = 0.0; // Bắt buộc khai báo kiểu double/float để lưu số thực
    for (int i = 1; i <= n; i++) {
        s += 1.0 / i; // Chia số thực để tránh bị làm tròn về 0
    }
    cout << fixed << setprecision(4) << "Tong S = " << s << "\n";
    return 0;
}
# BUỔI 4: KỸ THUẬT ĐỌC/GHI FILE CHUẨN (*.INP, *.OUT)

---

## 1. MỤC TIÊU BUỔI HỌC & TRỌNG TÂM LẤY ĐIỂM
* **Kiến thức cốt lõi:** Nắm vững cơ chế hoạt động của File I/O trong lập trình thi đấu (đọc từ tệp `*.INP` và xuất ra tệp `*.OUT`)[cite: 25, 190].
* **Trọng tâm đề thi:** Áp dụng cho 100% các câu hỏi trong đề thi HSG các cấp (từ cấp Trường, Huyện đến Tỉnh)[cite: 2, 4]. Hệ thống chấm tự động (Themis) chấm bài trực tiếp qua tệp; bài làm không đọc/ghi đúng tệp sẽ bị 0 điểm toàn bài thi[cite: 25, 190].
* **2 bẫy dữ liệu học sinh hay mất điểm:**
  1. **Đặt sai tên tệp hoặc sai đường dẫn:** Đề bài yêu cầu `BAI1.INP` nhưng đặt nhầm thành `input.txt`, `bai1.inp` (hệ thống phân biệt chữ hoa/thường) hoặc không để tệp input cùng thư mục với mã nguồn[cite: 25, 190].
  2. **Quên đóng tệp (`close()`) hoặc đọc sót phần tử:** Quên gọi lệnh đóng tệp khiến bộ đệm (buffer) chưa kịp xả dữ liệu vào tệp output[cite: 26, 32, 191, 197]; hoặc đọc dữ liệu dạng xâu nhưng quên ép kiểu sang số nguyên dẫn đến lỗi tính toán[cite: 11, 25, 176, 190].

---

## 2. HIỆP 1: LÝ THUYẾT & THỊ PHẠM (55 PHÚT)

### 2.1. Khởi động (10 phút)
* **Câu hỏi 1:** Khi đi thi HSG, tại sao máy chấm không dùng bàn phím để nhập dữ liệu và màn hình để xem kết quả mà bắt buộc dùng tệp `*.INP` và `*.OUT`[cite: 3, 25, 190]?
* **Câu hỏi 2:** Tệp chứa dữ liệu vào (`*.INP`) và tệp mã nguồn (`.cpp` hoặc `.py`) phải được lưu ở vị trí nào để chương trình mở tệp thành công[cite: 25, 190]?

### 2.2. Bản chất kiến thức mới (15 phút)
* **Bản chất File I/O:** Chuyển đổi luồng vào/ra chuẩn từ thiết bị ngoại vi (bàn phím/màn hình) sang tệp văn bản lưu trữ trên ổ đĩa[cite: 25, 26, 190, 191].
* **Ẩn dụ thực tế:** File I/O giống như hình thức giao tiếp bằng hòm thư bưu điện: Đề thi gửi dữ liệu qua phong bì thư đến (`*.INP`), học sinh mở thư đọc đề, giải bài rồi niêm phong đáp án gửi lại vào phong bì thư đi (`*.OUT`). Nếu viết nhầm địa chỉ trên phong bì, giám khảo chấm thi sẽ không nhận được bài.
* **Quy chuẩn đọc/ghi tệp:**
  * **C++:** Sử dụng thư viện `<fstream>` với đối tượng `ifstream` để đọc và `ofstream` để ghi (thao tác tương tự `cin` và `cout`), sau đó gọi phương thức `.close()`[cite: 26, 32, 191, 197].
  * **Python:** Dùng hàm `open('ten_file.INP', 'r')` để đọc dữ liệu dạng chuỗi, dùng `.split()` để tách các giá trị, ép kiểu cần thiết, và dùng `open('ten_file.OUT', 'w')` kèm `.write()` để ghi kết quả[cite: 11, 26, 32, 176, 191, 197].

### 2.3. Thị phạm thuật toán mẫu (30 phút)
* **Bài toán:** Cho tệp `INPUT.INP` gồm 2 dòng: dòng 1 là số nguyên dương $N$ ($N \le 10^5$), dòng 2 gồm $N$ số nguyên[cite: 27, 192]. Tìm số lớn nhất trong mảng và ghi vào tệp `OUTPUT1.OUT`[cite: 27, 192].
* **Ví dụ mẫu:**
  * `INPUT.INP`:
    ```text
    5
    10 3 21 15 4
    ```
  * `OUTPUT1.OUT`:
    ```text
    21
    ```
* **Luồng chạy:** Mở tệp input $\rightarrow$ Đọc số lượng phần tử $N$ $\rightarrow$ Đọc tuần tự $N$ số nguyên vào mảng $\rightarrow$ Đóng tệp input $\rightarrow$ Tìm giá trị lớn nhất $\rightarrow$ Mở tệp output $\rightarrow$ Ghi kết quả $\rightarrow$ Đóng tệp output.

#### Code C++:
```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    // 1. Mo tep de doc du lieu
    ifstream fi("INPUT.INP");
    int n;
    fi >> n; // Doc so luong phan tu
    
    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        fi >> a[i]; // Doc tung phan tu vao mang
    }
    fi.close(); // Dong tep input sau khi doc xong

    // 2. Tim so lon nhat
    int max_val = *max_element(a.begin(), a.end());

    // 3. Mo tep de ghi ket qua
    ofstream fo("OUTPUT1.OUT");
    fo << max_val << "\n";
    fo.close(); // Dong tep output

    return 0;
}