##  가변 인자
### 가변 인자란 갯수가 변할 있는 인자 


```
	#include <iostream>
	#include <cstdarg>
	#include "swap.h"	
	using std::cout;
	using std::endl;

	int sum(int count, ...) //...을 넣으면 가변인자를 넣을 수 있음
	{
		int result = 0;
		va_list args;
		va_start(args, count);

		for (int i = 0; i < count; ++i)
		{
			result += va_arg(args, int);
		}
		va_end(args);
		return result;
	}
	int main() 
	{
		cout << sum(4, 10, 20, 30, 40) << endl; //10,20,30,40 은 스택에 계속 쌓임
	}

```
### 위의 코드에는 단점이 있음 count를 지정해 줘야 함
### template를 통해 보완
```
	#include <iostream>
	#include <cstdarg>

	using std::cout;
	using std::endl;

	int sum(int value) // 탈출 조건 마지막 40이 될 때 여기로 옴
	{
		return value;
	}

	template<typename... Args> // 템플릿 매개변수 팩 
	int sum(int value, Args... args) // 함수 매개변수 팩 ... 이 팩 int value로 언팩 
	{
		return value + sum(args...); // 재귀로 구현
	}
	int main() 
	{
		cout << sum(10, 20, 30, 40) << endl; //10,20,30,40 은 스택에 계속 쌓임
	}
	
```
### 여러 자료형 받게 typename 추가 
```
	#include <iostream>
	#include <cstdarg>

	using std::cout;
	using std::endl;

	template<typename T>
	T sum(T value) // 탈출 조건 마지막 40이 될 때 여기로 옴
	{
		return value;
	}

	template<typename T, typename... Args> // 템플릿 매개변수 팩 
	T sum(T value, Args... args) // 함수 매개변수 팩 ... 이 팩 int value로 언팩 
	{
		return value + sum(args...); // 재귀로 구현
	}
	int main() 
	{
		cout << sum(10.3, 20.3f, 30, 40) << endl; //10,20,30,40 은 스택에 계속 쌓임
	}

```
