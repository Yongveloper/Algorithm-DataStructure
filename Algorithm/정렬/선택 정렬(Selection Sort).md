# 선택 정렬(Selection Sort)

- 주어진 리스트에서 가장 작은 값을 선택하여 맨 앞에 위치시키고, 그 다음으로 작은 값을 찾아 두 번째 위치에 위치시키는 과정을 반복하여 정렬하는 알고리즘이다.
- 앞으로 보내진 원소는 더 이상 위치가 변경되지 않는다.

## 기본 개념 💡

- 선택 정렬은 간단하면서도 이해하기 쉬운 알고리즘이지만, 그만큼 시간 복잡도가 높아 대규모 데이터를 정렬할 때는 성능이 떨어지는 단점이 있다.
- 선택 정렬의 <strong>시간 복잡도는 O(n^2)</strong>으로, 입력 데이터의 크기가 커질수록 성능 저하가 더욱 심해진다.
- 코드 구현이 쉽다.

### 버블 정렬 vs 선택정렬❓

버블 정렬보다 더 나은 시나리오는 단 하나의 경우인데 어떠한 이유에서 메모리 사용을 고려하는 경우라면 버블 정렬보단 선택 정렬이 더 나은 선택이 될 수 있다.

## 선택 정렬 구현 코드

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }

  return arr;
}

// Example usage
const unsortedArr = [3, 1, 6, 2, 9, 0];
const sortedArr = selectionSort(unsortedArr);
console.log(sortedArr); // [0, 1, 2, 3, 6, 9]
```

배열의 길이를 n으로 저장한 뒤, 바깥쪽 for 루프에서 i를 0부터 n-2까지 증가시키면서, 현재 인덱스 i부터 끝까지의 값 중 가장 작은 값을 찾아서 i번째 위치에 놓게 된다.</br>
이 과정을 n-1번 반복하면 모든 값이 정렬되어 나열된다.
