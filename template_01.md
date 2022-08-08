# Template
##  개념
### 두개의 값을 바꿔주는 함수
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
