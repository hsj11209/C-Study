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

#### 위 부분 자체는 함수가 아님 함수 template임(type을 parater로 넘김 -> type을 선언하는 위치에 T가 있음)
```
template<typename T>
void _swap(T& x, T& y)
{
	T temp = x;
	x = y;
	y = temp;
}
```

#### 이런 식으로 호출하는 순간 함수 코드가 생성됨
```
_swap(x, y);
```

#### int를 parameter로 들어가서 아래와 같이 컴파일 타임에 암시적으로 추론 
```
_swap<int>(x, y);
```

#### Template은 일반화 프로그래밍(Generic programing)을 가능하게 해줌
#### 타입에 의존하지 않고 하나의 값을 여러 데이터 타입을 가져 재사용성을 높이는 방식




