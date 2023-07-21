## Chapter 01 C언어 기반의 C++ 1
### 01-1. printf와 scanf를 대신하는 입출력 방식

기본적인 실행방식은 C 프로그램의 실행방식과 동일하나, 확장자를 .cpp 로 해야 C++ 문법규칙을 적용한 C++ 컴파일러로 컴파일이 된다.
```cpp
#include <iostream>

int main(void) {
    int num = 20;
    std::cout << "Hello World" << "!" << std::endl;
    std::cout << num << ' ' << 'A',
    std::cout << 10 << 3.14 << std::endl;
    return 0;
}
```

C++ 에서 입출력 관련 일을 하기 위해 `#include <iostream>` 헤더파일 선언이 필요하다. ( std, cout, endl 등 )  
C++에서는 프로그래머가 정의하는 헤더파일 선언 대신 표준 헤더파일 선언에서는 확장자를 생략하기로 약속되어 있다.  
과거에는 `#include <iostream.h>` 였으나 새로운 C++ 표준이 도입되면서,  

1. 과거 표준 라이브러리와 새로운 표준 라이브러리 구분하기 위한 목적
2. 새 표준 라이브러리를 사용하는 형태로 소스코드를 쉽게 변경하기 위한 목적

으로 iostream.h 헤더는 과거 표준 입출력 라이브러리 및 헤더를 의미하도록 하고, iostream 이 새로운 표준 입출력 라이브러리 및 헤더를 의미하는 것으로 통용되었다.

- 출력을 위해서는 `std::cout << 출력대상;` 형태를 취한다.  
출력대상은 정수, 실수, 문자열, 변수도 올 수 있다. ( 서식문자로 출력포맷을 지정하지 않아도 좋다. )  

- 또한, << 도 연산자이다. 이 연산자는 둘 이상의 출력대상을 연이어서 출력할 수 있다.
```cpp
std::cout << '출력대상1' << '출력대상2' << '출력대상3';
```

- << 연산자를 이용해 std::endl 를 출력하면 개행할 수 있다. 

```cpp
#include <iostream>

int main(void) {
	int x1;
	std::cout << "1번 : ";
	std::cin >> x1;

	int x2;
	std::cout << "2번 : ";
	std::cin >> x2;

	std::cout << "덧셈 : " << x1 + x2;
	return 0;
}
```

1. 키보드로부터의 데이터 입력에 헤더파일 선언문 `#include <iostream>` 이 필요하다.
2. 키보드로부터의 데이터 입력에는 `std::cin` 과 >> 연산자가 사용된다.
3. 지역변수 선언은 어디서든 가능하다.

C++에서는 데이터의 입력도 데이터의 출력과 마찬가지로 별도 포맷 지정이 필요 없다.  
`std::cin >> x1 >> x2;` 와 같이 연속적으로 데이터를 입력받을 수 있다. ( 데이터 간 경계는 탭, 스페이스 바, Enter 과 같은 공백으로 나뉜다. )  

### 01-2 함수 오버로딩 (Function Overloading)
C언어에서는 동일한 이름의 함수가 정의되는 것을 허용하지 않는다. 함수의 이름만을 이용해서 함수 호출 대상을 찾기 때문이다.
```cpp
#include <iostream>

void myFunc(int a) {
	std::cout << a << std::endl;
}
void myFunc(int a, int b) {
	std::cout << a + b << std::endl;
}

int main(void) {
	myFunc(1);
	myFunc(1, 2);
	return 0;
}
```

함수 오버로딩 (Function Overloading) : C++은 함수호출 시 전달되는 인자를 통해서 호출하고자 하는 함수의 구분이 가능하기 때문에, 매개변수 선언형태가 다르다면 동일한 이름의 함수정의를 사용할 수 있다.  
매개변수의 자료형 또는 개수가 달라야 함수의 오버로딩이 가능하다.

### 01-3 매개변수의 디폴트 값 (Default Value)
C++의 함수에는 기본적으로 설정되어 있는 값을 의미하는 디폴트 값을 설정할 수 있다.

```cpp
#include <iostream>

int Adder(int num1 = 1, int num2 = 2) {
	return num1 + num2;
}

int main(void) {
	std::cout << Adder() << std::endl; // 3
	std::cout << Adder(5) << std::endl; // 7
	std::cout << Adder(3, 5) << std::endl; // 8
	return 0;
}
```

매개변수에 디폴트 값이 설정되어 있으면, 선언된 매개변수의 수보다 적은 수의 인자전달이 가능하다.  
그리고 전달되는 인자는 왼쪽에서부터 채워져 나가고, 부족분은 디폴트 값으로 채워진다.  

```cpp
#include <iostream>
int Adder(int num1 = 1, int num2 = 2);

int main(void) {
	std::cout << Adder() << std::endl;
	std::cout << Adder(5) << std::endl;
	std::cout << Adder(3, 5) << std::endl;
	return 0;
}

int Adder(int num1, int num2) {
	return num1 + num2;
}
```

함수 프로토타입을 선언하는 경우 선언에만 디폴트 값을 위치시켜야 한다. ( 미리 선언되어야 호출할 때 알 수 있음 )  
또한, 부분적으로 디폴트 값을 설정할 수도 있다. 그러나 오른쪽 매개변수의 디폴트 값을 비우는 형태로는 디폴트 값을 지정할 수 없다.  
-> 함수에 전달되는 인자가 왼쪽에서부터 오른쪽으로 채워지기 때문이다.

```cpp
int myFunc(int a = 10) {
	return a;
}

int myFunc(void) {
	return 10;
}
```

myFunc 함수에 인자를 전달하지 않고 호출하면 오버로딩한 두 함수 호출 조건을 동시에 만족하기 때문에 컴파일 에러가 난다.

### 01-4 인라인(inline) 함수

```cpp
#include <iostream>
#define SQUARE(x) ((x)*(x))

int main(void) {
	std::cout << SQUARE(5) << std::endl;
	return 0;
}
```

매크로 함수는 일반적인 함수에 비해서 실행속도의 이점이 있지만, 정의하기 어렵고 복잡한 함수를 매크로의 형태로 정의하는데 한계가 있다.  
매크로 함수는 정의하기가 복잡하니, 일반 함숴럼 정의가 가능하면 좋겠어서 C++ 의 인라인 함수를 사용한다.

```cpp
#include <iostream>

inline int SQUARE(int x) {
	return x * x;
}

int main(void) {
	std::cout << SQUARE(5) << std::endl;
	return 0;
}
```

매크로를 이용한 함수의 인라인화는 전처리기에 의해 처리되지만, inline 키워드를 이용한 함수의 인라인화는 컴파일러에 의해서 처리가 된다.
( 컴파일러는 함수의 인라인화가 오히려 성능에 해가 된다고 판단할 때 키워드를 무시하기도 하거나, 필요한 경우 임의로 인라인 처리하기도 한다. )

매크로 함수는 자료형에 의존적이지 않은 함수지만 인라인 함수는 자료형을 정의하기 때문에 데이터 손실이 발생할 수도 있다. 함수 오버로딩으로 해결하는 건 여러 개를 더 정의하는 꼴이라..  
그러나 C++의 템플릿이라는 것을 이용하면 매크로 함수와 마찬가지로 자료형에 의존적이지 않은 함수가 완성된다.

```cpp
#include <iostream>

template <typename T>
inline T SQUARE(T x) {
	return x * x;
}

int main(void) {
	std::cout << SQUARE(10) << std::endl;
	std::cout << SQUARE(3.14) << std::endl;
	return 0;
}
```

### 01-5 이름공간(namespace)에 대한 소개
이름공간은 특정 영역에 이름을 붙여주기 위한 문법적 요소이다. 프로그램이 대형화되어 가면서 이름의 충돌문제가 등장한다. C++의 표준에서는 이름공간이라는 문법을 정의해서, 자신만의 이름공간을 만들고 이 안에 함수를 정의하거나 변수를 선언한다.

```cpp
#include <iostream>

namespace NameOne {
	void myFunc(void) {
		std::cout << "NameOne myFunc" << std::endl;
	}
}
namespace NameTwo {
	void myFunc(void) {
		std::cout << "NameTwo myFunc" << std::endl;
	}
}

int main(void) {
	NameOne::myFunc();
	NameTwo::myFunc();
	return 0;
}
```

연산자 :: 은 범위지정 연산자 (scope resolution operator) 라 하며, 이름공간을 지정할 때 사용하는 연산자이다.

```cpp
#include <iostream>

namespace NameOne {
	void myFunc(void);
}
namespace NameTwo {
	void myFunc(void);
}

int main(void) {
	NameOne::myFunc();
	NameTwo::myFunc();
	return 0;
}

void NameOne::myFunc(void) {
	std::cout << "NameOne myFunc" << std::endl;
}
void NameTwo::myFunc(void) {
	std::cout << "NameTwo myFunc" << std::endl;
}
```

함수의 선언과 정의를 구분할 수도 있다.

```cpp
#include <iostream>

namespace NameOne {
	void myFunc(void);
}
namespace NameTwo {
	void myFunc(void);
	void myFunc2(void);
}

int main(void) {
	NameOne::myFunc();
	NameTwo::myFunc();
	return 0;
}

void NameOne::myFunc(void) {
	std::cout << "NameOne myFunc" << std::endl;
	NameTwo::myFunc();
}
void NameTwo::myFunc(void) {
	std::cout << "NameTwo myFunc" << std::endl;
	myFunc2();
}
void NameTwo::myFunc2(void) {
	std::cout << "NameTwo myFunc2" << std::endl;
}
```

동일한 이름공간에 정의된 함수를 호출할 때에는 이름공간을 명시할 필요가 없다.

```cpp
#include <iostream>

namespace NameOne {
	int n = 0;
	namespace SubOne {
		int n = 10;
	}
	namespace SubTwo {
		int n = 20;
	}
}
int main(void) {
	std::cout << NameOne::n << std::endl;
	std::cout << NameOne::SubOne::n << std::endl;
	std::cout << NameOne::SubTwo::n << std::endl;
	return 0;
}
```

이름공간은 다른 이름공간 안에 삽입될 수 있다.  
지금까지 콘솔 입출력에 사용한 std::cout, std::cin, std::endl 은 이름공간 std 안에 선언되어 있다는 것을 알 수 있다.
using 선언을 통해서 이름공간의 정의 없이 함수를 호출할 수 있다.

```cpp
#include <iostream>

namespace NameOne {
	void myFunc(void) {
		std::cout << "NameOne myFunc" << std::endl;
	}
}
namespace NameTwo {
	void myFunc(void) {
		std::cout << "NameTwo myFunc" << std::endl;
	}
}
int main(void) {
	using NameOne::myFunc;
	myFunc();
	return 0;
}
```

`using NameOne::myFunc; ` 선언은 곧 "myFunc 함수를 이름공간 NameOne 에서 찾으라는 의미이다. using 선언 지역을 벗어나면 선언 효력을 잃게 된다. 그래서 전역 선언으로 해주는 것이 좋다.

```cpp
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int main(void) {
	int n; cin >> n;
	cout << "입력된 숫자는" << endl;
	cout << n << endl;
	return 0;
}
```

일일이 using 선언을 하는 것이 귀찮다면, 이름공간에 선언된 모든 것에 대해 이름공간 지정을 생략하도록 명령할 수 있다.

```cpp
#include <iostream>
using namespace std;

int main(void) {
	int n; cin >> n;
	cout << "입력된 숫자는" << endl;
	cout << n << endl;
	return 0;
}
```

이름충돌이 발생할 확률이 높아지지만, 편하게 사용할 수 있다.

```cpp
#include <iostream>
using namespace std;

namespace AAA {
	namespace BBB {
		namespace CCC {
			namespace DDD {
				void myFunc(void) {
					cout << "Hello World!" << endl;
				}
			}
		}
	}
}

int main(void) {
	AAA::BBB::CCC::DDD::myFunc();

	namespace ABC = AAA::BBB::CCC::DDD;
	ABC::myFunc();
	return 0;
}
```

이름공간이 너무 중첩된다면, `namespace ABC = AAA::BBB::CCC::DDD;` 선언처럼 이름공간에 별칭을 줄 수 있다.  
또한, 범위지정 연산자는 다른 기능으로 사용할 수 있는데, 지역변수가 있는 상태에서 전역변수에 접근할 수 있다.

```cpp
#include <iostream>
using namespace std;

int a = 20;

void myFunc(void) {
	int a = 10;
	cout << a << endl;
	cout << ::a << endl;
}

int main(void) {
	myFunc();
	return 0;
}
```