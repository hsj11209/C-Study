# Template
##  개념
### 두개의 값을 바꿔주는 함수가 있음
```
#include <iostream>

using std::cout;
using std::endl;

void _swap(int& x, int& y)
{
	int temp = x;
	x = y;
	y = temp;
}
int main() 
{
	int x = 10, y = 20;
	_swap(x, y);
	cout << x << endl;
	cout << y << endl;
}

```
### 정수가 아닌 다른 타입으로 연산하려면 매번 다른 타입의 함수를 생성해줘야 해서 번거로움 -> 이를 편하게 해주는 것이 template
```
#include <iostream>

using std::cout;
using std::endl;

template<typename T>
void _swap(T& x, T& y)
{
	T temp = x;
	x = y;
	y = temp;
}
int main() 
{
	int x = 10, y = 20;
	_swap(x, y);
	cout << x << endl;
	cout << y << endl;
}
```
#### typename -> class로 변경 가능
```
template<typename T>
void _swap(T& x, T& y)
{
	T temp = x;
	x = y;
	y = temp;
}
```
#### 위 부분 자체는 함수가 아님 함수 템플릿임
```
_swap(x, y);
```
#### 이런 시긍로 호출하는 순간 함수 코드가 생성됨

