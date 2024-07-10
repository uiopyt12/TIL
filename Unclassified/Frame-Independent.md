
### 예제:

```C++
std::chrono::time_point<std::chrono::steady_clock> previous_time;
const unsigned FRAME_DURATION = 16667; // 마이크로초 단위 16667 / 1,000,000 초 = 16667µs 
// 프레임 속도를 초당 60 프레임으로 설정
unsigned lag = 0;

previous_time = std::chrono::steady_clock::now();
// 메인 게임 루프
while (window.isOpen() == true) {
        unsigned delta_time = std::chrono::duration_cast<std::chrono::microseconds>(std::chrono::steady_clock::now() - previous_time).count();
        lag += delta_time;
        previous_time = std::chrono::steady_clock::now(); 
        // previous_time += std::chrono::microseconds(delta_time);와 같다.

        while (lag >= FRAME_DURATION) {
                lag -= FRAME_DURATION;
                
                // 게임 로직 업데이트 
                update();
        }

        // 렌더링
        render();
}

```
FRAME_DURATION 변수와 lag 변수를 사용해 Frame-independent하게 만들어주는 코드이다.  
  
lag이 FRAME_DURATION보다 작다면 FRAME_DURATION보다 커질 때까지 대기하고  
lag이 FRAME_DURATION보다 크거나 같아질 때 while 루프로 들어가 다시 lag -= FRAME_DURATION를 통해 lag 값을 낮춰준다.  
lag이 FRAME_DURATION보다 많이 커서 루프를 여러번 돌며 lag -= FRAME_DURATION이 여러번 실행될 수 있다.  
***

### **Frame (프레임)**
- 화면이 갱신되는 하나의 사이클이다.
  
- 위 코드에서는 ```while (window.isOpen() == true)``` 의 내부 코드가 한 번 실행되는 것이 하나의 프레임이다.  
  
- 하드웨어나 이런저런 차이에 의해 코드의 실행시간은 달라질 수 있고, 이에 따라 프레임 또한 달라질 수 있다.   
  
- 궁금하다면 아래 코드를 실행시켜보자
```C++
#include <iostream>
#include <chrono>
#include <SFML/Graphics.hpp>

int main() {
        sf::RenderWindow window(sf::VideoMode(800, 600), "FPS Example");
        sf::Clock clock;  // SFML 시계를 사용하여 시간 측정
        sf::Time previousTime = clock.getElapsedTime();
        sf::Time currentTime;
        unsigned int frameCount = 0;

        while (window.isOpen()) {
                sf::Event event;
                while (window.pollEvent(event)) {
                        if (event.type == sf::Event::Closed)
                                window.close();
                }

                window.clear();
                window.display();

                // FPS 계산
                currentTime = clock.getElapsedTime();
                frameCount++;
                if (currentTime.asSeconds() - previousTime.asSeconds() >= 1.0f) {
                        window.setTitle("FPS: " + std::to_string(frameCount)); // 타이틀 바에 FPS 출력
                        std::cout << "FPS: " << frameCount << std::endl; // 콘솔에 FPS 출력
                        frameCount = 0;
                        previousTime = currentTime;
                }
        }

        return 0;
}

```  
위 코드를 실행시켜보면 알 수 있는 것처럼 한 컴퓨터에서도 프레임의 변화폭이 클 수 있고, 따라서 프레임 종속적으로 게임 로직을 업데이트한다면 게임 속도가 빨라졌다가 느려졌다 하는 등 불안정할 것이다.   




##### 참고
- Chat GPT
- https://github.com/Kofybrek/Tetris