# Lớp và đối tượng #
**Dẫn nhập:** Đối với các bạn mới bắt đầu học lập trình, các bạn được làm quen với lập trình hướng thủ tục, tất cả các hàm đều được viết chung với nhau trên cùng một file. Mỗi lệnh đều là một hoạt động theo sau đó là các đối tượng tham gia hoạt động đó. `increase(value);`

```cpp
    #include <iostream>
    int increase(int a)
    {
    	return a+1;
    }
    int main()
    {
		int value = 1;
    	std::cout << increase(value);
    	return 0;
    }
```
Trong khóa học này các bạn sẽ được làm quen với lập trình hướng đối tượng. Mỗi lệnh của các bạn sẽ bắt đầu bằng một đối tượng và sau đó là hoạt động mà đối tượng đó thực hiện. `a.increase();`

```cpp
    #include <iostream>
    class sohang
    {
    private:
    	int value;
    public:
    	void setValue(int v)
    	{
    		value = v;
    	}
    	int increase()
    	{
    		return a+1;
    	}
    };
    int main()
    {
    	sohang a;
    	a.setValue(1);
    	std::cout << a.increase();
    }
```

Lập trình hướng đối tượng là kĩ thuật rất cơ bản và quan trọng. Các điểm mạnh sẽ được giới thiệu qua từng bài học.
Lập trình theo hướng đối tượng cho phép bạn quản lý các vấn đề trong bài toán theo đối tượng.
Ở bài học đầu tiên các bạn sẽ 
## 1.1 Khái niệm về lớp và đối tượng ##

Có hai khái niệm cơ bản trong lập trình hướng đối tượng là lớp (class) và đối tượng (object). Lớp chỉ là một khái niệm, trong khi đối tượng là một thứ cụ thể (được khai báo và có vùng nhớ riêng có).

Ví dụ: Học sinh nói chung không chỉ rõ là ai nhưng ta vẫn biết học sinh có thể làm gì và có tính chất gì. Học sinh A là một học sinh cụ thể.

Bạn có thể nhớ rằng class chỉ là một bản vẽ nhà và object là một ngôi nhà.
### 1.1.1 Khai báo lớp: tên lớp, thuộc tính, phương thức ###
Một lớp gồm có 3 thành phần chính:

- Tên lớp
- Thuộc tính (attribute)
- Phương thức (method)

Cấu trúc khai báo lớp đơn giản trong C++ như sau:

    class <Tên lớp>
    {
    	<Thuộc tính>;
    	<Phương thức>;
    };

Ví dụ cụ thể cho lớp HocSinh:

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
    public:
    	void DiHoc();
    };
	
Ở đây thuộc tính là `MaSo` và `HoTen`, phương thức là `DiHoc`. 

Ngoài ra trong khi khai báo có sử dụng 2 từ khóa là `private` và `public`. 

`private` là từ khóa giúp bạn bảo vệ một phương thức hoặc một thuộc tính, cụ thể ở ví dụ trên là các lớp khác lớp HocSinh sẽ không thể truy cập các thuộc tính hoặc các phương thức có từ khóa private. Lưu ý nếu các thuộc tính và phương thức không có từ khóa nào phía trước thì sẽ mặc định là private trong C++.

`public` thì thoải mái hơn, tất cả các lớp đều có thể thực hiện các phương thức hoặc truy cập các thuộc tính có từ khóa public. Ngoài ra còn có từ khóa protected, cũng là một cách thức để bảo vệ các phương thức và thuộc tính, sẽ được giới thiệu ở bài học sau.


### 1.1.2 Cài đặt các phương thức của lớp ###
Có 2 cách để cài đặt phương thức cho lớp:

- Cách 1: khai bào đồng thời cài đặt ngay trong class.
Dành cho các class nhỏ. 
Ví dụ:

> 	//sohang.h
>     #include <iostream>
>     
>     class sohang
>     {
>     private:
>     	int value;
>     public:
>     	void setValue(int v)
>     	{
>     		value = v;
>     	}
>     	int increase()
>     	{
>     		return a+1;
>     	}
>     };


- Cách 2: tách rời phần khai báo và cài đặt. 	
>     //sohang.h
>     #include <iostream>
>     
>     class sohang
>     {
>     private:
>     	int value;
>     public:
>     	void setValue(int v);
>     	int increase();
>     };
>     
> 	//sohang.cpp
> 	#include "sohang.h"
> 	void sohang::setValue(int v)
> 	{
> 		value = v;
> 	}
> 	int sohang::increase()
> 	{
> 		return a+1;
> 	}

Cài đặt dành cho các class lớn, giúp việc quản lý và sửa đổi các phương thức dễ dàng.
Lưu ý rằng: phần khai báo sẽ nằm trong file `.h`, phần cài đặt sẽ nằm trong file `.cpp`
### 1.1.3 Khái niệm về đối tượng và chu kỳ sống ###
Một đối tượng luôn có một vùng nhớ riêng cho nó. Vì vậy chu kỳ sống của một đối tượng hiểu nôm na là từ khi nó được cấp vùng nhớ cho đến khi nó được thu hồi. Chi tiết hơn là từ khi nó thực hiện `constructor` cho đến khi nó thực hiện `destructor`. 2 quá trình này đều là phương thức của class, việc cài đặt giống như các phương thức khác, sẽ được giới thiệu ở bài sau.
## 1.2 Sự che chắn, bao bọc dữ liệu và phương thức ##
Ở trên đã giới thiệu 2 từ khóa là public và private. Đây là một cách để bảo vệ dữ liệu và phương thức của một class.

    class HocSinh
    {
    private:
    	int MaSo;
    	string HoTen;
    	void TuHoc();
    public:
    	void DiHoc();
    };
Lấy ví dụ như class HocSinh đã được giới thiệu ở trên nhưng ta thêm một phương thức là TuHoc (tự học). Phương thức này được nằm dưới từ khóa private. Khi có từ khóa private thì phương thức này chỉ có thể truy cập bởi chính đối tượng đó hoặc các đối tượng khác cũng là lớp HocSinh. Các đối tượng còn lại không thể bắt HocSinh phải tự học được.

Cũng như trên, phương thức DiHoc là một phương thức public cho nên các đối tượng khác có thể bắt HocSinh phải đi học, ví dụ như đối tượng ChaMe bắt HocSinh phải đi học chẳng hạn.
## 1.3 Tạo lập, sử dụng và hủy đối tượng ##
Để tạo và hủy một đối tượng C++ có hỗ trợ 2 toán tử new và delete.
### 1.3.1 Toán tử new ###
Đây là toán tử giúp tạo một đối tượng mới. Toán tử new sẽ trả về một con trỏ đến một vùng nhớ, nếu không thể tạo được sẽ trả về `NULL`

    sohang* a = new sohang;

### 1.3.2 Toán tử delete ###
Đây là toán tử giúp hủy một đối tượng. 

	delete a;
