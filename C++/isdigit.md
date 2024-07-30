### 예제

```C++
#include <iostream>
#include <cctype>

int main()
{
	char abc[10] = "1q2w3e4r5";

	for (int i = 0; i < 9; i++)
		printf("%2c", abc[i]);
	std::cout << '\n';
	for (int i = 0; i < 9; i++)
		printf("%2d", isdigit(abc[i]));
}
```

***
함수는 아래와 같은 형태이다.
```c
 int isdigit ( int c );
```
인자가 0부터 9면 **0이 아닌 수(참)** 를  
아니면 **0(거짓)** 을 반환하는 함수이다.  
 
사용하려면 헤더를 포함해줘야하니  
아래와 같이 사용하는 것이 편할 것 같다.  

```c
if (c>='0' && c<='9')
```

