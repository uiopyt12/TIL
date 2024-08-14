# Heap(힙)
- 완전 이진 트리이다.
- 최대 힙(max heap)은 모든 부모 노드의 값이 자식 노드의 값보다 크거나 같다.
- 원소 삽입과 삭제에 **O(logN)**이 소요된다.
- 최대값/최소값을 찾는데 **O(1)**이 소요된다.
- 왼쪽 노드와 오른쪽 노드 중 어느 노드가 큰 지 모르기 때문에 n번째로 큰 원소를 구하는 것은 O(1)에 할 수 없다.


### 배열을 통해 구현한 **최소힙**과 **push, top, pop** 함수
```C++
int heap[100001]; // 부모 자식 계산의 편의를 위해 1-index 사용
int heapIDX; // 힙의 크기이자, 마지막으로 삽입된 원소를 가리키고 있음

void push(int n)
{
	heap[++heapIDX] = n;
	
	int childIDX = heapIDX;
	int parentIDX = heapIDX / 2;
	while (heap[childIDX] < heap[parentIDX]) // 최소 힙이므로 부모가 자식보다 작아야 함
	{
		swap(heap[childIDX], heap[parentIDX]);
		if (parentIDX == 1) break;
		childIDX /= 2;
		parentIDX /= 2;
	}
}

int top()
{
	if (heapIDX == 0) return 0;
	return heap[1];
}

void pop()
{
	if (heapIDX == 0) // 힙의 크기가 0이면 반환
		return;
	swap(heap[1], heap[heapIDX]); // 마지막 원소랑 루트랑 자리를 바꿈
	heapIDX--; // 힙의 크기를 감소시키고, 마지막으로 삽입된 원소를 가리키게 함
	
	int parentIDX = 1;
	while (parentIDX*2 <= heapIDX) // 왼쪽 자식이 있는 동안
	{
		int minChildIDX = parentIDX * 2; 
		if (minChildIDX + 1 <= heapIDX && heap[minChildIDX] > heap[minChildIDX + 1])
			minChildIDX += 1;
		if (heap[minChildIDX] >= heap[parentIDX]) break;
		swap(heap[parentIDX], heap[minChildIDX]);
		parentIDX = minChildIDX;
	}
}
```****