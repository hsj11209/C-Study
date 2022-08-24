##  템플릿 구체화 
### 함수 템플릿,클래스템플릿은 함수와 클래스 자체가 아님 , 클래스나 함수를 만들어 주기 위한 형판에 불과함
### 구체화를 해주지 않으면 compile해도 기계어로 변환 안됨 
### 템플릿을 사용하려면 구체화 해줘야 함

```
	#include <iostream>
	#include <vector>
	using std::cout;
	using std::endl;

	template
	void std::swap<int>(int&, int&); // 명시적 구체화

	int main() 
	{
		// 암시적 구체화
		std::vector<int> v; 
		int x = 10, y = 20;
		std::swap(x, y);
	}

```
### 예시 swap.h
```
#pragma once

template<typename T>
void swap(T& x, T& y);
	
```
### 예시 swap.cpp
```
#include "swap.h"

template<typename T>
void swap(T& x, T& y)
{
	T temp = x;
	x = y;
	y = temp;
}

```
### 예시 main 
```
	#include <iostream>
	#include "swap.h"	
	using std::cout;
	using std::endl;

	int main() 
	{
		int x = 10, y = 20;
		swap(x, y);
	}

```
### 이대로 빌드시 에러가 남 -> header파일의 선언을 찾을 수 있으나 -> cpp파일에 정의는 찾을 수 없음
### main에서 호출 시 암시적 구체화를 하였음 swap<int>(x,y)를 호출했음 -> 템플릿이 아닌 일반 함수는 링크 되지만 함수 템플릿은 기계어로 안만들어 짐
### 기계어로 안만들어져서 암시적 구체화일 때 기계어로 만들어야 되는데 코드가 없음
### swap cpp파일 수정
```
	#include <iostream>
	#include "swap.h"	
	using std::cout;
	using std::endl;

	int main() 
	{
		int x = 10, y = 20;
		swap(x, y);
	}

```
### 헤더파일에 구현을 해줘야 함 

	
