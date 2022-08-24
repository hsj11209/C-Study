##  템플릿 특수화 
### 템플릿의 특정 패턴에 대해서 별도의 처리가 하고 싶을 경우

```
#include <iostream>
#include <vector>
using std::cout;
using std::endl;

class Test // 이 클래스에 대해서만 다른 템플릿 처리를 해주고 싶을 때 
{

};

template <typename T>
void change(T& x, T& y)
{
	cout << "swap" << endl;
	T temp = x;
	x = y;
	y = temp;
}

template<>
void change<Test>(Test& x, Test& y)
{
	cout << "swap<Test>" << endl;
}

int main() 
{
	Test t0, t1;
	change(t0, t1);
}

```
### 완전 특수화, 부분 특수화 
```
#include <iostream>
#include <vector>
using std::cout;
using std::endl;

template<typename T, typename S>
class Test // 이 클래스에 대해서만 다른 템플릿 처리를 해주고 싶을 때 
{
public:
	T num0;
	S num1;
};

template<>
class Test<int, float> // 완전 특수화
{

};

template<typename T> //  타입이 완전히 정의되지 않음 부분 특수화 
class Test<T, T>
{
public:
	T nums;
};

int main() 
{
	Test<int, int> t0;   // 세번째 템플릿으로 특수화
	Test<int, float> t1; // 두번째 템플릿으로 특수화
	Test<float, int> t2; // 첫번째 템플릿으로 특수화
}

	
```
	
### vector<bool>은 특수화 되어있음
```
		#include <iostream>
	#include <vector>
	using std::cout;
	using std::endl;

	int main() 
	{
		std::vector<int> iv; 
		std::vector<float> fv;
		std::vector<bool> bv; // vector는 bool이 특수화 되어 있음
	}
	/*
	* bool은 1byte true false를 8개 표현할 수 있음 이를 효율적으로 표현하기 위해 특수화 함
	*/


```
	
### 메소드 특수화 
```
	#include <iostream>
	#include <vector>
	using std::cout;
	using std::endl;

	template<typename T>
	class Queue
	{
	private:
		std::vector<T> _items;

	public:
		void push(T item)
		{
			_items.push_back(item);
		}
	};

	template<>  // 메소드에 대한 특수화
	void Queue<int>::push(int item)
	{
		cout << "int" << endl;
	}

	int main() 
	{
		Queue<float> q0;
		q0.push(1);
		Queue<int> q1;
		q1.push(1.f);

	}

```
