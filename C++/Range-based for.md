### 예제

```C++
#include <iostream>

int main()
{
	int a[10] = { 1,2,3,4,5,6,7,8,9,10 };
	for (const auto& it : a)
		std::cout << it << ' ';
}
```

***
for 루프를 돌기 쉽게 도와주는 기능이다.

- auto를 통해 컴파일러가 타입을 추론하도록, 그리고 값을 복사해오지 않도록 참조를 통해 접근하는 것이 권장된다.
    ```C++
	int a[10] = { 1,2,3,4,5,6,7,8,9,10 };
	for (const auto& it : a)
		std::cout << it << ' ';
    ```
  
- 아래는 인접리스트를 통해 구현한 그래프를 너비 우선 탐색하는 함수인데 auto를 쓸 경우 아래처럼 코드를 읽기 쉽게 만들 수 있다.
    ```C++
    vector<vector<int>> adjList(1005);
    bool isVisited[1001];

    void bfs(int curVertex)
    {
        isVisited[curVertex] = true;	
        queue<int> q;
        q.push(curVertex);
        while (!q.empty())
        {
            int cur = q.front(); 
            q.pop();
            for (const auto& nxt : adjList[cur]) // adjList[cur]이 1차원 벡터이므로 nxt는 int로 추론될것임
            {
                if (isVisited[nxt] == true) continue;
                isVisited[nxt] = true;
                q.push(nxt);
            }
        }
    }
    ```

- 아래 예제는 2차원 배열을 넘겨주었으므로 auto에 의해 arr이 1차원 배열로 추론한 예제이다.
    ```C++
    #include <bits/stdc++.h>
    using namespace std;

    int main()
    {
        int a[10][10] =
        {
            {1,2,3,4},
            {11,22,33,44},
            {111,222,333,444}
        };

        for (const auto& arr : a)
            cout << arr[1] << ' ';
    }
    ```
출력 : ```2 22 222 0 0 0 0 0 0 0```