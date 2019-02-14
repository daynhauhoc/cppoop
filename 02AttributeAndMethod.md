# 2. Thuộc tính đối tượng và phương thức #
**Dẫn nhập:** Bài này chúng ta sẽ bắt đầu xây dựng các thành phần cơ bản của một class, cụ thể trong bài này chúng ta sẽ tạo hàm constructor và destructor cho một class.

    class <Tên lớp>
    {
		<Tên lớp>(); //constructor
		~<Tên lớp>(); //destructor
	};
## 1. Phương thức tạo lập (CONSTRUCTOR) ##
Phương thức constructor có nhiệm vụ tạo một đối tượng của lớp đó. Phương thức này có đặc điểm là không có kiểu trả về và được gọi tự động ghi tạo một đối tượng thuộc class đó.

    class <Tên lớp>
    {
		<Tên lớp>(); //constructor
	}

Phương thức constructor có thể có hoặc không có tham số, tùy theo kiểu tham số ta chia ra nhiều loại, phụ thuộc vào từng mục đích sử dụng. **Nhưng cơ bản vẫn là tạo ra một đối tượng từ các tham số truyền vào, xét thuộc tính và có thể thực hiện thêm các thao tác khác**. Một class có thể cài đặt nhiều constructor.
### 1.1 Parameterized constructors ###
Đây là constructor có chứa tham số đơn thuần.

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
	public:
		HocSinh(int MaSo)
		{
			this->MaSo = MaSo;
		}
	};
class `HocSinh` có `Parameterized constructors` là `HocSinh(int MaSo);` khi cần tạo một đối tượng chúng ta sẽ gọi lệnh như sau

	HocSinh hs(186);

hoặc

	HocSinh* hs = new HocSinh(186);

Chương trình sẽ tự động gọi constructor phù hợp với tham số đầu vào. Và kết quả là ta có một đối tượng `hs` có MaSo là 186. 
Trong constructor có sử dụng một biến là `this`, đây là một con trỏ, con trỏ này chứa địa chỉ của đối tượng đó. `this->MaSo` có nghĩa là truy cập đến thuộc tính `MaSo` của đối tượng đó. 
Chúng ta có thể cài đặt đầy đủ

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
	public:
		HocSinh(int MaSo, string HoVaTen)
		{
			this->MaSo = MaSo;
			HoTen = HoVaTen;
		}
	};

HoTen lúc này không cần con trỏ this trỏ đến vì không có tham số nào trùng tên với nó và có thể dùng trực tiếp, trong khi đó thì tên tham số `MaSo` của constructor trùng với tên thuộc tính `MaSo` của class đó, nên cần sử dụng con trỏ `this` để phân biệt.

Ngoài ra bạn có thể tạo constructor như sau.

		HocSinh(int MaSoHS, string HoVaTen):MaSo(MaSoHS),HoTen(HoVaTen)
		{
		}
### 1.2 Default constructors ###
Đây là constructor không có tham số, khá đơn giản để cài đặt.

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
	public:
		HocSinh() //Default constructors
		{

		}
	};
Có thể không cần cài đặt. Compiler đã tự động tạo sẵn một `Default constructors`, vì vậy bạn có thể thấy là không cần cài đặt bất cứ constructor nào mà vẫn tạo được đối tượng là vì Compiler đã tạo sẵn `Default constructors`. Nếu chúng ta muốn thay đổi `Default constructors` thì chỉ cần sửa đổi bên trong constructor là được.

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
	public:
		HocSinh()
		{
			MaSo = 0;
		}
	};

Tốt nhất là luôn tự cài đặt các constructor, đừng nhờ vả đến compiler, vì có thể gây lỗi không đồng bộ khi chuyển code qua các compiler khác để build.
### 1.3 Copy constructors ###
Copy constructors là một dạng "nhái" các thuộc tính của một đối tượng này cho một đối tượng khác.

    HocSinh hs1(186,"ltd");
    HocSinh hs2(hs1); //Copy constructors

Lúc này `hs2` sẽ có thuộc tính giống như hs1, nhưng copy constructor có 2 loại là `deep copy` và `shallow copy`, vì vậy việc copy cũng khác nhau đôi chút.
Shallow copy là copy một cách "nông cạn", chỉ nhái những thứ có thể trực tiếp nhìn thấy được.
Deep copy là copy hoàn toàn tất cả nội dung của đối tượng kia.

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
		HocSinh* Ban;
	public:
		HocSinh(HocSinh& that)
		{
			this->MaSo = that.MaSo;
			this->HoTen = that.HoTen;
			this->Ban = that.Ban;
		}
	};

Đây là một shallow copy thông thường, khá nguy hiểm vì khi này 2 đối tượng có thể dùng chung một vùng nhớ Ban. Chúng ta cần copy một cách rõ hơn và tách biệt giữa 2 đối tượng này.

		HocSinh(HocSinh& that)
		{
			this->MaSo = that.MaSo;
			this->HoTen = that.HoTen;
			this->Ban = new HocSinh(*that.Ban);
		}
## 2. Phương thức hủy (DESTRUCTOR) ##
Tương tự như constructor nhưng destructor được gọi tự động ghi phương thức bị hủy hoặc ra ngoài scope của nó.

    class <Tên lớp>
    {
		~<Tên lớp>(); //destructor
	};
Phương thức destructor sẽ không có tham số, thường trong destructor chúng ta sẽ cài đặt để trả các vùng nhớ mà chúng ta xin cấp phát.
## 3. Định nghĩa toán tử (OPERATOR OVERLOADING) ##
Operator không hề xa lạ với các bạn.

    int a = 3;
    int b = 4;
    int c = a + b;
Operator chính là các phép toán mà ngôn ngữ hỗ trợ `(+,-,*,/,...)`, với mỗi kiểu dữ liệu chúng ta cần định nghĩa các operator cho nó (ví dụ như kiểu int đã được C++ định nghĩa sẵn kèm theo các operator để chúng ta có thể thực hiện được phép cộng). Ở phần này chúng ta sẽ cài đặt các operator cho class.

Cú pháp chung cho việc cài đặt các toán tử như sau.

    <Kiểu Trả Về> operator<Toán Tử>(<tham số>);
Ví dụ

   	HocSinh& operator=(const HocSinh& that)
	{
		this->HoTen = that.HoTen;
		this->MaSo = that.MaSo;
		return *this;
	}

Có các toán tử sau không thể cài đặt chồng là

> `.` (toán tử lấy thành phàn trực tiếp)
> 
> `?:` (toán tử điều kiện)
> 
> `sizeof` (toán tử lấy kích thước)
> 
> `::` (toán tử chỉ phạm vi)
> 
> `.*` (toán tử lấy thành phần thông qua con trỏ)
> 
> `typeid` (toán tử lấy kiểu dữ liệu)

Lưu ý về cài đặt toán tử nhập xuất, chúng ta cần khai báo như sau.

friend ostream& HocSinh::operator<<(ostream &out, const HocSinh& src)

Ở đây có 2 thứ cần chú ý:
1. Chúng ta sử dụng từ khóa friend do toán tử xuất được viết chồng bằng hàm ở bên ngoài nên để tủy cập được các thành phần private bên trong lớp HocSinh chúng ta phải sử dụng từ khóa friend.
2. Cần truyền tham chiếu đối tượng ostream (đây là đối tượng dùng để xuất ra màn hình). 

