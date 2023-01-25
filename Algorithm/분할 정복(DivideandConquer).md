# 분할정복(Divide and conquer)

> 이 알고리즘은 주로 배열이나 문자열 같은 큰 규모의 데이터셋을 처리한다. 연결 리스트나 트리가 될 수도 있다. 즉, 큰 데이터 덩어리를 작은 조각으로 나눈다.

> 분할정복 알고리즘은 문제를 나눌 수 없을 때까지 나누어서 각각을 풀면서 다시 합병하여 문제의 답을 얻는 알고리즘이다.

## 📖 이진 탐색 기본 문제 예시

배열은 정렬된 상태여야 한다.
배열과 숫자를 받는 <code>search</code> 함수를 작성한다.
해당 함수는 숫자로 받는 값을 배열에서 찾아 해당 index를 return 하고 없으면 -1를 return 한다.

```javascript
serach([1, 2, 3, 4, 5, 6], 4); //3
serach([1, 2, 3, 4, 5, 6], 6); // 5
serach([1, 2, 3, 4, 5, 6], 11); // -1
```

### 1. for loop 해결책 <code>O(N)</code>

```javascript
function serach(arr, val) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === val) {
      return i;
    }
  }
  return -1;
}
```

### 2. 이진 탐색 해결책 <code>O(Log(N))</code>

```javascript
function search(arr, val) {
  let min = 0;
  let max = arr.length - 1;

  while (min <= max) {
    let middle = Math.floor(min + max) / 2;
    let currentElement = arr[middle];

    if (currentElement < val) {
      min = middle + 1;
    } else if (currentElement > val) {
      max = middle - 1;
    }
  }
}
```

중간 index에서 시작 하고 중간 값이 목표값보다 작으면 최솟값을 중간index + 1, 크면 최댓값을 중간index -1를 해주면서 절반 씩 나누면서 값을 찾아간다.

## 💡 정리

> 입력값의 길이가 짧으면 굳이 필요하진 않지만, 수백개 수천개의 길이를 담고 있다면 이진 탐색 해결법이 더 나은 방법이 될 수 있다.

> 분할정복에는 이진 탐색, 병합 정렬, 퀵 정렬 등 많은 분할정복 알고리즘이 있다. 앞으로 더욱 학습해야 한다.(2023.01.21)
