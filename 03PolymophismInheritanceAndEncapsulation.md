# 3. Đa hình, kế thừa và đóng gói #
**Dẫn nhập:** Ở phần này chúng ta sẽ tìm hiểu về các tính chất cơ bản của OOP bao gồm đa hình (polymophism), kế thừa (inheritance) và đóng gói (encapsulation). Đây là các thành phần cơ bản và cực kì hữu ích giúp cho việc phát triển một chương trình bằng OOP trở nên thuận tiện và dễ dàng trong việc sửa đổi mã nguồn. 
## 6.1 Đa hình và kế thừa ##
Chúng ta lấy ví dụ về HocSinh, trong một lớp học, sẽ có nhiều chức vụ khác nhau cho HocSinh, ví dụ như lớp trưởng, lớp phó học tập,... Vậy khi cần triển khai các lớp cho mỗi loại HocSinh này chúng ta phải cài đặt từng lớp đối tượng LopTruong, LopPhoHocTap,... mặc dù các lớp này đều có chung một bản chất là HocSinh?

Đa hình và kế thừa sẽ giúp chúng ta tận dụng lại mã nguồn của lớp HocSinh (ví dụ như những phương thức HocBai(), DiemDanh(),... hay các thuộc tính HoTen, MaSo,...)

    class HocSinh
    {
    protected:
    	int MaSo;
    	string HoTen;
		string ChucDanh;
	public:
		void HocBai();
		void DiemDanh();

		virtual string getChucDanh();
	};

	class LopTruong : HocSinh
	{
	public: 
		void BaoCao();

		string getChucDanh();
	};

	class LopPhoHocTap : HocSinh
	{
	public: 
		void ThongBao();

		string getChucDanh();
	};
Ở ví dụ trên, lớp LopTruong sẽ có mọi thuộc tính và phương thức của HocSinh ngoài ra còn có phương thức BaoCao(). Ta gọi LopTruong là lớp được kế thừa từ lớp HocSinh. Lớp LopPhoHocTap cũng tương tự.

Các thuộc tính được kế thừa được nằm dưới từ khóa protected, từ khóa này tương đương với private (tức là các lớp khác không thể truy cập đến các phương thức hay thuộc tính nằm dưới từ khóa private) ngoài ra nó còn cho phép các lớp con kế thừa các thuộc tính hay phương thức nằm dưới từ khóa protected (

Tính đa hình được thể hiện khá rõ ở ví dụ trên qua phương thức getChucDanh(), phương thức này sẽ trả về chức danh của đối tượng. Với từng loại HocSinh sẽ có chức danh khác nhau, đó chính là tính đa hình trong OOP. Để có cơ chế đa hình này thì lớp cha cần sử dụng từ khóa virtual, chúng ta sẽ tìm hiểu ở phần dưới.

Ngoài điểm mạnh về việc tận dụng mã nguồn đã được cài đặt, nó còn giúp cho việc đồng bộ giữa các đối tượng có cùng cha. 

Ví dụ như LopTruong và LopPhoHocTap đều có HocBai giống với HocSinh, khi giáo viên yêu cầu HocSinh học thế nào thì chỉ cần sửa mã nguồn HocBai của HocSinh thì các đối tượng được kế thừa đều thực hiện HocBai như vậy.

## 6.2 Lớp trừu tượng, phương thức ảo và phương thức thuần ảo ##
Chúng ta sẽ tìm hiểu cách sử dụng.

    class HocSinh
    {
    protected:
    	int MaSo;
    	string HoTen;
	public:
		void HocBai();
		void DiemDanh();

		virtual string getChucDanh()
		{
			return "Hoc Sinh";
		}
	};

	class LopTruong : HocSinh
	{
	public: 
		void BaoCao();

		string getChucDanh()
		{
			return "Lop Truong";
		}
	};
	
	int main()
	{
		HocSinh* pHS;
		LopTruong lt;
		HocSinh hs;

		pHS = &hs;
		cout << pHS->getChucDanh();

		pHS = &lt;
		cout << pHS->getChucDanh();
		
		return 0;
	}

Nhờ có từ khóa virtual mà khi pHS gọi getChucDanh() sau khi được trở thành LopTruong sẽ có chức danh "Lop Truong". Và ta gọi phương thức này là phương thức ảo. Nếu như không có từ khóa virtual này thì khi getChucDanh sẽ vẫn là chức danh "Hoc Sinh". 

Vậy thì phương thức "thuần" ảo là gì? Phương thức thuần ảo là phương thức mà cha sẽ không định nghĩa cho nó, mà các lớp con sẽ phải định nghĩa cho nó.

    class HocSinh
    {
    protected:
    	int MaSo;
    	string HoTen;
	public:
		void HocBai();
		void DiemDanh();

		virtual string getChucDanh() = 0; //phuong thuc thuan ao
	};

	class LopTruong : HocSinh
	{
	public: 
		void BaoCao();

		string getChucDanh()
		{
			return "Lop Truong";
		}
	};

Phương thức thuần ảo được khai báo như sau `virtual <Phương thức> = 0;`	lúc này dẫn đến HocSinh trở thành một lớp trừu tượng. Lớp trừu tượng khác với lớp bình thường ở một số đặc điểm sau:


1. Không thể tạo một đối tượng từ lớp trừu tượng, mà ta đã biết một đối tượng sẽ có vùng nhớ của nó, nếu không thể tạo được vùng nhớ thì nó chỉ có thể là một con trỏ. Và ta có thể hiểu lớp trừu tượng chỉ là "khái niệm" chứ không có đối tượng cụ thể.
2. Nếu có một phương thức ảo trong lớp thì lớp đó sẽ trở thành lớp trừu tượng.
3. Các lớp con kế thừa từ lớp trừu tượng bắt buộc phải định nghĩa các phương thức thuần ảo.
		
## 6.3 Đóng gói ##
Đóng gói một lớp ở đây chính là bảo vệ dữ liệu của lớp đó. Bảo vệ ở việc truy cập dữ liệu và các thao tác dữ liệu. Nếu cần lấy hoặc sửa đổi dữ liệu thường thông qua các phương thức get và set (lấy và chỉnh sửa dữ liệu) để từ đó quản lý dữ liệu.

Bảo vệ bản thân lập trình viên tránh khỏi các sai sót khi truy cập giữa các class khác nhau. Nên nhớ rằng OOP là một công cụ "hỗ trợ" lập trình viên, đừng nên cố gắng hoặc lách luật các tính chất của OOP.