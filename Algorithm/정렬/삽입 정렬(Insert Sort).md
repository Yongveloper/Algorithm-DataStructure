# 삽입 정렬(Insert Sort)

- 간단하고 직관적인 정렬 알고리즘 중 하나다.</br>
- 배열의 원소를 순서대로 탐색하며, 각 원소를 이미 정렬된 배열 부분과 비교하여 적절한 위치에 삽입하는 방식으로 정렬한다.
- 대부분의 경우 다른 고급 정렬 알고리즘보다 성능이 떨어진다. 따라서, 매우 큰 배열이나 시간 제한이 있는 경우에는 다른 정렬 알고리즘을 사용하는 것이 좋다.

---

## 구현 코드 👀

### 첫번째 방법(코드)

```javascript
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while (j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

1. 배열의 두 번째 원소부터 시작하여, 첫 번째 원소와 비교한다.
2. 첫 번째 원소보다 작은 경우, 첫 번째 원소와 위치를 바꾼다.
3. 세 번째 원소부터 시작하여, 이미 정렬된 배열 부분에서 자신의 위치를 찾아 삽입한다.
4. 배열 전체를 탐색하면서 2~3단계를 반복한다.

### 두번째 방법(코드)

```javascript
function insertSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    for (let j = i; j > 0; j--) {
      // 인덱스 j부터 1까지 1씩 감소하며 반복
      if (arr[j] < arr[j - 1]) {
        // 한 칸씩 왼쪽으로 이동
        // swap
        [arr[j], arr[j - 1]] = [arr[j - 1], arr[j]];
      } else {
        // 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
        break;
      }
    }
  }
}
```

---

## 삽입 정렬 Big O ⭐

시간 복잡도는 <code>O(n^2)</code>다. 하지만, 배열의 크기가 작은 경우에는 다른 정렬 알고리즘보다 빠를 수 있으며, 이미 정렬된 배열에 대해서는 최선의 경우 <code>O(n)</code>의 시간 복잡도를 가진다.
