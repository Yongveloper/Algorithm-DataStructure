# 버블 정렬(Bubble Sort)

- 버블 정렬은 별로 효율적이지는 않고 흔히 사용되지 않는다.

## 기본 개념

버블 정렬의 개념은 만약 배열을 오름차순으로 정렬하는 상황에서 더 큰 숫자가 한 번에 하나씩 뒤로 이동을 하는 방법이다.</br>
기본적으로 어떤 항목이 더 크면 교환으로 하고, 다음 항목과 비교하고, 다음 항목보다 더 크면 또 교환을 하고, 다시 다음 항목과 비교하면서 반복을 한다.</br>
오름차순의 상황에서는 가장 큰 값이 상단을 향해서 값을 정렬하는 방식으로 목록을 만든다.

## 덜 최적화된(?) 버블 정렬 코드 ❓

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```

해당 코드는 이미 정렬이 된 상태에서는 버블 정렬이 작동하는 원리 때문에 끝 부분에 index가 없는 곳과 비교해서 <code>undifined</code>와 무의미한 비교를 하고, 정렬이 된 상태에서도 무의미한 비교를 하며 루프를 돌게 된다.

## 덜 최적화된 코드 약간의 해결책 ❗

```javascript
function bubbleSort(arr) {
  for (let i = arr.length; i > 0; i--) {
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```

해당 코드는 루프가 실행 되면서 정렬을 똑같이 하는데, 정렬이 되면서 점점 비교 횟수를 줄인다.

## 버블 정렬 코드 최적화 ✅

```javascript
function bubbleSort(arr) {
  let noSwaps;
  for (let i = arr.length; i > 0; i--) {
    noSwaps = true;
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        noSwaps = false;
      }
    }
    if (noSwaps) break;
  }
  return arr;
}
```

어느정도 정렬이 된 상태의 데이터에서 루프가 돌면서 확인을 할 때 정렬이 일어나지 않으면 루프를 끝낸다.</br>
배열이 거의 정렬된 상테라면, 배열의 길이가 길어짐에 따라 전 코드와는 아주 큰 차이가 생긴다.

## 버블 정렬 Big O ⭐

일반적으로는 <code>n^2</code>이다. 왜냐면 중첩 루프가 있고, 대략적으로 비교하기 때문이다.</br>
배열의 각 항목마다 n번의 비교를 하고 배열의 다른 모든 항목 하나하나와 비교한다.</br>
그러나 데이터가 거의 정렬 됐거나 이미 정렬이 끝난 상태에서 <code>noSwaps</code> 변수가 있는 코드를 사용할 때는 선형 시간(linear time)에 더 가깝다. 가능한 최고의 경우이고 이 경우엔 <code>O(N)</code>이 된다.
