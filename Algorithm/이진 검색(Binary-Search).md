# 이진 검색(Binary Search)

- 이진 검색에서는 확인을 할 때마다 남은 항목의 절반을 없앨 수 었다.
- <b>정렬된 배열</b>을 대상으로만 작동되기 때문에 데이터가 정렬이 되어 있어야 한다.

## 기본 개념 💡

이진 검색의 기본적인 개념은 분할 정복(dividing and conquering)이다.</br>
그래서 <b>배열을 두 부분으로 나눈다.</b></br>
그 다음 보통 중간에 있는 중간점을 선택하고, 우리가 찾는 값이 중간점을 기준으로 좌측 절반과 우측 절반 중 어느 쪽에 있을지 확인한다.

## 이진 검색 문제 유형의 대표적인 사례

1. <b>매우 넓은(억 단위 이상) 탐색 범위</b>에서 최적의 해를 찾아야 하는 경우
2. 데이터를 정렬한 뒤에 다수의 쿼리(query)를 날려야 하는 경우

## 예시 👀

```javascript
해당 배열에서 15를 찾는다.
[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 16, 17, 18, 19];
```

이진 검색으로 15를 찾는데,</br>
좌측은 1, 우측은 19, 중간점은 11로 시작한다. 중간점을 찾을 때 데이터의 길이가 홀수면 올림이나 버림을 사용해서 중간점을 선택한다.

1. 우리가 찾고자 하는 15가 중간점인 11보다 크다. 좌측 전부를 배제하고 새로운 좌측은 12로 정해준다. 새로운 우측은 이전과 동일하다. 새로운 중간점은 17이 된다.
2. 17은 15보다 크다. 우측 부분을 모두 배제하고 새로운 우측이 16이 된다. 새로운 중간점은 15가 된다.
3. 우리가 찾고자 하는 값이 중간점 15와 같다.

따라서 확인(추측)을 겨우 세 번만 하고 값을 찾는데 성공했다.</br>
처음에 중간점이 11이라는 걸 확인했고, 15가 11보다 크다는 것을 알았다.</br>
그래서 두 번째 확인을 했고, 중간점이 17이 됐고, 그 다음에는 15를 선택했는데 우리가 찾던 값이었다.
</br></br>
맨 처음부터 시작했다면 1,2,3,4... 선형 검색을 사용 하면 9번의 확인 끝에 15를 찾았을 것이다.

## 이진 검색 코드 예시 👀

```javascript
function binarySearch(arr, num) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === num) {
      return mid;
    }
    if (arr[mid] < num) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

## 이진 검색 코드 예시(재귀함수)

```javascript
function binarySearch(arr, target, start, end) {
  if(start > end) return -1
  let mid = Math.floor((start _ end)/2)
  // 찾은 경우 중간점 인덱스 반환
  if(arr[mid] === target){
    return mid;
  }else if(arr[mid] > target) {
    // 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    return binarySearch(arr, target, start, mid - 1);
  } else {
    // 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    return binarySearch(arr, target, mid + 1, end);
  }
}
```

## 정렬된 배열에서 특정 원소의 개수 구하기

- 코딩 테스트에서는 정렬된 배열에서 값이 특정 범위에 해당하는 원소의 개수를 계산하는 것을 요구하는 경우가 종종 있다.
- 이러한 문제를 해결하기 위해 <code>lowerBound()</code> 함수와 <code>upperBound()</code> 함수를 사용할 수 있다.
- 하지만 JavaScript에서는 제공하지 않는 함수이기 때문에 직접 작성을 해야한다.

### 하한선과 상한선 함수

- <code>lowerBound(arr, x)</code>: 정렬된 순서를 유지하면 배열 arr에 x를 넣을 가장 왼쪽 인덱스를 반환
- <code>upperBound(arr, x)</code>: 정렬된 순서를 유지하면 배열 arr에 x를 넣을 가장 오른쪽 인덱스를 반환

```javascript
// 정렬된 순서를 유지하면서 배열에 삽입할 가장 왼쪽 인덱스 반환
function lowerBound(arr, target, start, end) {
  while (start < end) {
    let mid = Math.floor((start + end) / 2);
    if (arr[mid] >= target) {
      end = mid; // 최대한 왼쪽으로 이동하기
    } else {
      start = mid + 1;
    }
  }
  return end;
}

// 정렬된 순서를 유지하면서 배열에 삽입할 가장 오른쪽 인덱스를 반환
function lowerBound(arr, target, start, end) {
  while (start < end) {
    let mid = Math.floor((start + end) / 2);
    if (arr[mid] > target) {
      end = mid;
    } else {
      start = mid + 1; // 최대한 오른쪽으로 이동하기
    }
  }
  return end;
}

// 값이 [leftValue, rightValue]인 데이터의 개수를 반환하는 함수
function countByRange(arr, leftValue, rightValue) {
  // 유의: lowerBound와 upperBound는 end 변수의 값을 배열의 길이로 설정
  const leftIndex = lowerBound(arr, leftValue, 0, arr.length);
  const rightIndex = lowerBound(arr, rightValue, 0, arr.length);

  return rightIndex - leftIndex;
}

// 배열 선언
const arr = [1, 2, 3, 3, 3, 3, 4, 4, 8, 9];
// 값이 4인 데이터 개수 출력
console.log(countByRange(arr, 4, 4));
// 값이 [-1,3] 범위에 있는 데이터 개수 출력
console.log(countByRange(arr, -1, 3));
```

## 이진 검색의 Big O ⭐

- 최악의 경우 또는 평균: <code>O(log n)</code>
- 최고의 상황: <code>O(1)</code> (처음 중간점과 찾고자 하는 값이 같은 경우)
