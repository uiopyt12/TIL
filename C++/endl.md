### 예제

```C++
#include <iostream>

int main()
{
	std::cout << "Hello" << std::endl;
}

```

***

#### **std::endl**과 **\n**의 차이점
**endl**은 개행을 하고 버퍼를 플러시해준다.  
**\n**은 개행 역할만 한다.  
코딩테스트나 온라인 저지에서 출력에 개행을 많이 포함하게 된다면  
매 개행마다 버퍼를 플러시하는 endl보다는 \n이 시간 측면에서 매우 유리하다.  

(std::endl은 쉽게 생각해서 \n + std::flush라고 생각하면 된다.)