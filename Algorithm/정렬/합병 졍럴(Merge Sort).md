# 합병 정렬(Merge Sort)

<strong>합병 정렬(merge sort)</strong>은 대표적인 <strong>분할 정복(divide and conquer)</strong> 알고리즘 중 하나로, 리스트를 반으로 나눈 뒤 각각을 재귀적으로 정렬하고, 정렬된 두 개의 리스트를 합쳐서 정렬된 하나의 리스트를 만드는 알고리즘이다.

## 작동 개념 💡

합병정렬은 일반적으로 다음과 같은 세 단계로 구성된다.

1. <strong>분할(divide)</strong>: 입력 리스트를 같은 크기의 두 개의 부분 리스트로 분할합니다. 이때 분할은 리스트의 중간 지점에서 수행된다.

2. <strong>정복(conquer)</strong>: 각 부분 리스트를 재귀적으로 합병정렬을 이용해 정렬합니다. 이 과정은 입력 리스트의 크기가 충분히 작아질 때까지 반복된다.

3. <strong>합병(merge)</strong>: 정렬된 두 부분 리스트를 하나의 정렬된 리스트로 합병한다.

---

- 0개 요소, 1개 요소 배열이 이미 정렬되어 있다는 점을 활용한다.
- 배열을 더 작은 배열로 나누는 방식이다. <strong>분할 정복</strong> 알고리즘이라 알려진 방식이다. 더 큰 배열을 나누고, 더 작은 하위 배열로 정렬한다. 0이나 1 요소 배열이 될 때까지 계속한다.
- 계속 분할한 다음 다시 병합시킨다.

<img src="https://user-images.githubusercontent.com/64254228/220133878-8bda1492-7e2e-41b2-b0d5-fee16533d949.png" width="650px" height="300px" title="합병정렬 분할" alt="표"></img>

## Merging Arrays 코드 ❓

```javascript
function merge(arr1, arr2) {
  let results = [];
  let i = 0;
  let j = 0;

  while (i < arr1.length && j < arr2.length) {
    if (arr2[j] > arr1[i]) {
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }

  while (i < arr1.length) {
    results.push(arr1[i]);
    i++;
  }

  while (j < arr2.length) {
    results.push(arr2[j]);
    j++;
  }

  return results;
}
```

1. 입력 두 개를 취하는 함수를 정희하여 빈 배열을 만들고,마지막에 반환할 빈 배열을 만든다.
2. 각 입력 배열에서 가장 작은 값(처음)부터 시작한다.
3. <code>i</code> 와 <code>j</code> 두 개의 카운터가 있다. 이 카운터들은 0부터 시작한다.
4. 아직 살펴보지 않은 값이 있다면, 즉 <code>i</code>와 <code>j</code>가 각각의 배열 끝에 도달하지 않았다면
   - 첫 번째 배열의 값으로 첫 번째 항목을 취한 다음 두 번째 배열의 첫 번째 항목 값과 비교한다.
   - 첫 번째 항목이 더 작다면 <code>results</code> 배열에 넣고 다음 첫 번째 배열의 다음 항목으로 넘어간다.
   - 반대로 첫 번째 배열에 잇는 항목이 더 크다면 두 번째 배열의 값을 취하여 <code>results</code> 배열에 넣은 다음 두 번째 배열의 다음 값으로 넘어간다.
5. 배열 하나를 완료한 다음에는 다른 배열의 남은 값을 모두 넣는다.

## 합병 정렬 구현 코드 👀

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

console.log(mergeSort([10, 24, 76, 73])); // [10, 24, 73, 76]
```

1. 배열의 길이가 1 또는 0이 될 때까지 <code>mergeSort</code> 함수를 호출 한다.
2. 배열의 절반을 자르기 위해서 <code>mid</code>라는 변수에 배열 길이 / 2 내림 값을 저장해준다.
3. 왼쪽 절반과 오른쪽 절반을 <code>slice</code> 메서드를 통해서 나눠줬는데, 이들에게 <code>mergeSort</code>를 호출해준다.
   <img src="https://user-images.githubusercontent.com/64254228/220137211-d94c8899-fc0a-4f33-b387-74a504ad0e5f.png" width="650px" height="300px" title="합병정렬 분할" alt="표2"></img>

## 합병 정렬 Big O ⭐

<img src="https://user-images.githubusercontent.com/64254228/220137606-2445e0db-0a48-4a18-a9b1-8ef1a97cde99.png" width="650px" height="100px" title="합병정렬빅오" alt="빅오"></img>
합병 정렬에서는 예외 케이스가 없다. 계속 나누고 나눈 다음 합치고 또 합칠 뿐이다.

<code>O(log n)</code>은 만약 32개의 요소가 있다면 2x2x2x2x2라는 의미인데, <code>n log n</code>은 각 분할마다, 합병할 때 <code>O(n)</code>번 비교한다. <code>n</code>의 길이가 늘어난다면, 합병 정렬이 아닌 합병 알고리즘 자체는 <code>O(n)</code>의 시간 복잡도를 갖게 되는데 그래서 종합적으로 보면 합병 정렬의 Big O는 O<code>(n log n)</code>이 된다.

정리 하자면 <code>log n</code>은 <code>n</code>증가에 따르는 분할 수이다. <code>n</code>에 따라 분할할 횟수를 말한다. 배열이 늘어나면 <code>log n</code> 비율로 늘어난다.
</br>합병을 실제로 수행하려면 <code>O(n)</code> 비교가 필요하고 결과적으로는 총 <code>O(n log n)</code>이 된다.
