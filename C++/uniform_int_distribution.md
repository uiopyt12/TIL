
### 예제:

```C++
#include <iostream>
#include <random>


int main()
{
	std::random_device rd;
	std::default_random_engine re(rd());
	std::uniform_int_distribution<int> distribution(1, 6);

	for (int i = 0; i < 10; i++)
	{
		int dice_roll = distribution(re);
		std::cout << dice_roll << ' ';
	}
}
```
위 프로그램을 실행하면 1부터 6까지의 무작위의 수가 10개 출력된다.
***

#### std::random_device
하드웨어 정보를 기반으로 시드를 생성한다.

#### std::random_engine
시드를 인자로 받아 의사 난수를 생성한다.

#### std::uniform_int_distribution<>
하한과 상한을 지정해주면 그 범위 사이의 값들을 균등한 확률에 가깝게 반환한다.
(참고로 uniform distribution은 균등 분포이다.)

***
#### rand() 대신 사용하는 이유
rand()는 0부터 32767 사이의 수를 반환한 값들을 나머지로 나눠주는데 이 과정에서 나누어 떨어지지 않을 경우 작은 수를 더 많이 반환하게 되어 수가 균등하지 않게 나올 수 있다.