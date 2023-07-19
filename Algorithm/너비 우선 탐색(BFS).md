# 너비 우선 탐색(BFS)

- 그래프 혹은 트리에서 <u>모든 노드를 한 번씩 탐색하기 위한 기본적인 방법</u>이다.
- <b>[완전 탐색]</b>을 수행하기 위해 사용할 수 있는 방법 중 하나다.
- (모든 간선의 길이가 동일할 때) 최단 거리를 탐색하기 위한 목적으로 사용할 수 있다.
- <b style="color: red">큐(queue) 자료구조</b>를 사용한다.
- 기본적으로 DFS는 스택, BFS는 큐를 사용한다.

## BFS 기본 동작 방식

1. <b>시작 노드</b>를 큐에 넣고 <b>[방문 처리]</b>한다.
2. 큐에서 원소를 꺼내어 <u>방문하지 않은 인접 노드</u>가 있는지 확인한다.
   - 있다면, 방문하지 않은 인접 노드를 큐에 <b>삽입</b>하고 <b>[방문 처리]</b>한다.
3. 2번 과정을 더 이상 반복할 수 없을 때까지 반복한다.

## BFS 사용 예시

1. 간선의 비용이 동일한 상황에서 <b>[최단 거리]</b> 문제를 해결하는 경우
2. 완전 탐색을 위해 사용한 DFS 솔루션이 메모리/시간 초과를 받아 BFS로 재시도 하는 경우
   - DFS와 BFS 모두 그래프 탐색 목적으로 사용할 수 있으나, 구현이 익숙하다면 BFS를 추천한다.

- 코딩 테스트에서 DFS로 해결할 수 있는 문제는 BFS로도 해결할 수 있는 경우가 많다.
  - DFS는 일반적인 최단 거리 문제를 해결할 수 없다.

## BFS 소스 코드 예시

```javascript
class Queue {
  constructor() {
    this.items = {};
    this.headIndex = 0;
    this.tailIndex = 0;
  }

  enqueue(item) {
    this.items[this.tailIndex] = item;
    this.tailIndex++;
  }

  dequeue() {
    const item = this.items[this.headIndex];
    delete this.items[this.headIndex];
    this.headIndex++;
    return item;
  }

  peek() {
    return this.items[this.headIndex];
  }

  size() {
    return this.tailIndex - this.headIndex;
  }
}

// 각 노드가 연결된 정보를 표현
const graph = [[], [2, 3, 4], [1], [1, 5, 7], [1, 7], [3, 8], [3], [4], [5]];

// 각 노드가 방문된 정보를 표현
const visited = new Array(graph.length).fill(false);

const bfs = (start) => {
  const queue = new Queue();
  queue.enqueue(start);
  // 현재 노드를 방문 처리
  visited[start] = true;
  // 큐가 빌 때까지 반복
  while (queue.size() !== 0) {
    // 큐에서 하나의 원소를 뽑아 출력하기
    const v = queue.dequeue();
    console.log(v);
    // 아직 방문하지 않은 인접한 원소들을 큐에 삽입
    for (const i of graph[v]) {
      if (!visited[i]) {
        queue.enqueue(i);
        visited[i] = true;
      }
    }
  }
};

// 정의된 BFS 함수 호출
bfs(1);
```
