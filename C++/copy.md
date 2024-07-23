### 예제

```C++
#include <bits/stdc++.h>

int main()
{
	int src[5] = { 1, 2, 3, 4, 5 };
	int dest[5] = { -1, -2, -3, -4, -5 };
	
	std::copy(&src[0], &src[0]+5, &dest[0]);

	for (int i = 0; i < 5; i++)
		std::cout << dest[i] << ' ';
}
```
  
***
복사를 해주는 std::copy 함수이다.  
참고로 ```std::copy(&src[0], &src[4], &dest[0]);```를 하면 마지막 원소가 복사되지 않는데,  
```copy(first, last, destFirst)```를 했을 때 **[first, last)** 까지, 즉 last는 포함하지 않고 복사되기 때문이다. 끝까지 복사하고 싶다면  
```std::copy(&src[0], &src[0]+5, &dest[0]);``` 혹은  
```std::copy(&src[0], &src[5], &dest[0]);```를 사용해야 한다.