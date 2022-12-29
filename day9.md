# day9

```c++
可变参
#include <iostream>
#include <string>
#include <stdarg.h>
using namespace std;
//实现可变参数
//原理：因为函数的形参都是连续存放在栈空间的
//条件：函数的参数一定要有特殊的作用（标明后面的参数的个数或类型）
int func(int num1, int num2,...)//第一个参数表示参数的个数
{
	va_list v1;		//va_list指针，用于va_start取可变参数，为char*
	va_start(v1, num1);	//使用v1,使其指向后面的可变参数
	printf("v1 = %d\n", *v1);
	int res;
	for (int i = 0; i < num1; i++)
	{
		res = va_arg(v1, int);//这里把v1往后跳sizeof（int）个字节，指向下一个参数
		printf("result = %d\n", res);
	}
	va_end(v1);//释放指针
	return 0;
}
int main()
{
	func(5, 6, 5, 4, 3, 4);
	return 0;
}

```





```c++
#include <iostream>
#include <string>
#include <stdarg.h>
using namespace std;
class A
{
public:
	A(const initializer_list<int> &v)
	{
		for (auto temp : v)//范围for，将v的值挨个赋给temp，再打印temp的值
		{
			cout << temp << endl;
		}
	}
	int num;
	int count;
};
void func(initializer_list<int> &v)
{
	for (auto temp : v)
	{
		cout << temp << endl;
	}
}
int main()
{
	//int a = { 3.14 };//列表初始化不会进行收缩转换，会报错
	A a1{ 1,2 };

	initializer_list<int> init_list{ 1,2,2,3,4,5,6,8,9 };

	for (auto temp : init_list)
	{
		cout << temp << endl;
	}

	for (auto it = init_list.begin(); it != init_list.end(); it++)
	{
		cout << *it << endl;
	}
	return 0;
}

```

