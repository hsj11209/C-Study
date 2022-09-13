##  템플릿 메타 프로그램밍
### 템플릿 함수, 함수 템플릿, 클래스 템플릿은 클래스나 함수 자체가 아님 단순한 템플릿, 함수와 클래스 코드를 만들어 주는 것이 메타프로그래밍
### 코드를 컴파일타임에 만들어야 하기 때문에 추론을함 예를 들어 factorial을 컴파일 타임에 만들 수 있음


```
	#include <iostream>
	#include <cstdarg>

	using std::cout;
	using std::endl;

	int factorial(int value)
	{
		if (value == 1)
			return value;
		return value * factorial(value -1);
	}

	int main()
	{
		cout << factorial(5) << endl;
	}

```
### 위의 코드에 템플릿 메타프로그래밍을 사용하면 컴파일 타임에 만들 수 있음
### 피보나치 수열을 구현

```
	#include <iostream>
	#include <cstdarg>

	using std::cout;
	using std::endl;

	int factorial(int value)
	{
		if (value == 1)
			return value;
		return value * factorial(value -1);
	}

	template<int N>
	struct Factorial
	{
		static const int value = N * Factorial<N - 1> ::value;
	};

	template<> // 템플릿 특수화
	struct Factorial<1>
	{
		static const int value = 1;
	};

	int main()
	{
		cout << factorial(5) << endl;
		cout << Factorial<5>::value << endl; // 컴파일 타임에 추론 됨 
	}
	
```
### 위에 같이 템플릿 메타프로그래밍을 사용하면 컴파일 타임은 길어질 수 있어도 런타임 기간은 짧아짐 -> 결과 계산을 이미 해버림
```
		#include <iostream>
	#include <cstdarg>

	using std::cout;
	using std::endl;

	int fib(int value)
	{
		if (value <= 1)
			return value;
		return fib(value - 1) + fib(value - 2);
	}

	template<int N>
	struct Fib
	{
		static const int value = Fib<N - 1>::value + Fib<N - 2>::value;
	};

	template<>
	struct Fib<0>
	{
		static const int value = 0;
	};

	template<>
	struct Fib<1>
	{
		static const int value = 1;
	};

	int main()
	{
		cout << Fib<6>::value << endl;
		cout << fib(6) << endl;
	}
```
