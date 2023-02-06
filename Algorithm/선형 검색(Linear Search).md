# 선형 검색(Linear Search)

> 1. 배열에서 검색하는 방법 중 가장 원초적이고 구현하기 쉬운 방법 중 하나이다.</br>
> 2. 데이터를 앞에서부터 뒤로, 또는 뒤에서부터 앞으로 순차적으로 확인하는 방법이다.</br>
> 3. 자바스크립트에서 <code>indexOf</code>, <code>includes</code>, <code>find</code>, <code>findIndex</code>와 같은 함수들도 선형 검색 기능을 사용한다.

## 기본 예제 📖

> 특정 숫자의 위치를 찾는 함수

```javascript
linearSearch([1, 32, 3, 53, 34, 22], 34); // 4
```

```javascript
function linearSearch(arr, num) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === num) return i;
  }
  return -1;
}
```

## 선형 검색의 시간 복잡도 💡

결론부터 말하면 선형 검색의 시간 복잡도는 <strong>O(N)</strong>이다.</br>
이유는 <strong>Big O는 광범위한 경향에만 신경을 쓰기 때문이다.</strong></br>
선형 검색에서 찾고자 하는 것이 처음 발견 되었다면 시간 복잡도는 O(1)가 되겠지만 n이 증가할 수록 배열의 길이나 문자열 등 우리가 사용하는 데이터의 길이도 길어진다. 그러면서 평균 소요 시간도 늘어난다.
