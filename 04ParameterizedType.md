# 4. Tham số hóa kiểu dữ liệu #
**Dẫn nhập:** OOP chính là một cách để phát triển phần mềm có thể mở rộng một cách dễ dành, chính vì vậy việc tham số hóa kiểu dữ liệu để có thể chỉnh sửa các kiểu dữ liệu bên trong lớp một cách hợp lý là một điều cần thiết.
## 4.1 Tham số hóa cho hàm ##
Đôi khi bạn phải thực hiện nhiều tác vụ tương tự nhau cho từng kiểu dữ liệu.

    int add(int a, int b)
	{
		return a+b;
	}
    long add(long a, long b)
	{
		return a+b;
	}
Để có thể tận dụng lại mã nguồn chung ta có thể tham số hóa cho hàm trên, thay vì viết 2 hàm, chúng ta chỉ cần viết một hàm.

	template <class T>
	T add(T a, T b)
	{
		return a+b;
	}

Chỉ cần như vậy chúng ta có thể tham số hóa cho tất cả các lớp đã định nghĩa toán tử +.
## 4.2 Tham số hóa cho lớp ##
Tham số hóa cho lớp cũng gần tương tự như tham số hóa cho hàm, nếu các bạn đã từng sài đến kiểu dữ liệu vector, kiểu dữ liệu dùng để quản lý mảng, bạn sẽ thấy kiểu vector có cấu trúc khai báo như sau, ví dụ cho khai báo cấu trúc vector gồm các phần tử số nguyên:

    vector<int> vt;

Chúng ta thông báo cho đối tượng vector vt sẽ quản lý các phần tử int.

Để có thể tham số hóa cho một kiểu dữ liệu bất kì, các bạn cài đặt như sau:

    template<class T>
    class tenclass
	{
		T thuoctinh;
		T phuongthuc(T thamso);
	}

Sử dụng T như một kiểu bất kì, các bạn cũng có thể tham số hóa nhiều hơn nữa.

    template<class T, class Z>
    class tenclass
	{
		T thuoctinh;
		T phuongthuc(Z thamso);
	}

Lưu ý Z và T có thể không cùng kiểu dữ liệu với nhau.

Trong quá trình compile trên Visual Studio các bạn có thể gặp lỗi khi tham số hóa (lỗi linker), bạn cần đưa tất cả mã cài đặt phương thức của class đó vào cùng file .h của class bạn cài đặt.