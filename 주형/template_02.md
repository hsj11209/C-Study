#include <iostream># Template
##  클래스 템플릿
### 함수도 클래스를 붙였던 것처럼 클래스에도 템플릿을 붙일 수 있음
### 클레스에 템플릿을 붙여 정수 형 및 string형도 가능한 queue 구현
```
#include <iostream>

using std::cout;
using std::endl;

template <typename T>

class Queue
{
private:
	size_t _size;
	size_t _capacity;
	T* _items;

public:
	Queue()
		:_size(0)  // 외부에서 봤을 때 Queue 원소 갯수
		, _capacity(4) // items의 사이즈를 가지고 있음
		, _items(new T[_capacity])
	{

	}

	~Queue()
	{
		delete[] _items; // 배열 해제시에는 delete[] 사용
	}

	void push(T item)
	{
		if (_size < _capacity)
		{
			_items[_size++] = item;
		}

		else
		{
			size_t newCapacity = _capacity * 2;

			T* oldItems = _items;
			T* newItems = new T[newCapacity];

			std::copy(oldItems, oldItems + _capacity, newItems);
			
			_capacity = newCapacity;
			_items = newItems;

			delete[] oldItems;

			push(item);
		}

	}

	void pop()
	{
		--_size;
	}

	T& top()
	{
		return _items[_size - 1];
	}
};

int main() 
{
	Queue <int> q0; 
	q0.push(1);
	q0.push(2);
	q0.push(4);
	cout << q0.top() << endl; //4
	q0.pop();
	cout << q0.top() << endl; //2

	Queue <std::string> q1;
	q1.push("abcd");
	q1.push("123");
	cout << q1.top() << endl; //123
	q1.pop();
	cout << q1.top() << endl; //abcd
}
