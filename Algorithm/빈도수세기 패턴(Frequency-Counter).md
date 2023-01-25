# 빈도수 세기 패턴 (Frequency-Counter)

> 여러 데이터와 입력값이 서로 비슷한 값으로 구성되어 있는지, 서로 간의 아나그램인지, 값이 다른 값에 포함되는지 여부를 비교하거나, 데이터를 입력값이나 두 개 이상의 빈도 혹은 특정하게 발생하는 빈도와 비교할 때 유용하다.

## 📖 문제 예시

2개의 배열을 받는 <code>same</code>이라는 함수를 작성하는데, 첫 번째 배열의 각 값의 제곱이 두 번째 배열에 속해 있으면 <code>true</code>를 반환 하고 아니면 <code>false</code>를 반환하는 함수를 만든다.
각각의 빈도수가 맞아야 한다.

```javascript
same([1, 2, 3], [4, 1, 9]); // true
same([1, 2, 3], [1, 9]); // false
same([1, 2, 1], [4, 4, 9]); // false
```

### 1. 중첩 for문<code>(O(N^2))</code> 해결책

```javascript
function same(arr1, arr2) {
  if (arr1.length !== arr2.length) {
    return false;
  }
  for (let i = 0; i < arr1.length; i++) {
    let correctIndex = arr2.indexOf(arr1[i] ** 2);
  }
  if (correctIndex === -1) {
    return false;
  }
  arr2.splice(correctIndex, 1);
}
return true;
```

<code>for</code>문 안에 <code>indexOf</code>를 사용하여 값을 찾기 때문에 시간 복잡도는 <code>O(N^2)</code>이 된다.

### 2. 빈도수 세기<code>(O(N))</code> 패턴 해결책

```javascript
function same(arr1, arr2) {
  if (arr1.length !== arr2.length) {
    return false;
  }
  let frequencyCounter1 = {};
  let frequencyCounter2 = {};
  for (let val of arr1) {
    frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1;
  }
  for (let val of arr2) {
    frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1;
  }
  console.log(frequencyCounter1);
  console.log(frequencyCounter2);
  for (let key in frequencyCounter1) {
    if (!(key ** 2 in frequencyCounter2)) {
      return false;
    }
    if (frequencyCounter2[key ** 2] !== frequencyCounter1[key]) {
      return false;
    }
  }
  return true;
}
```

외부에 총 3개의 <code>for</code>문이 있지만 2개의 <code>for</code>문이 for문 내부에 중첩된 <code>for</code>문보다 시간복잡도성에서 훨씬 낫다.
외부 <code>for</code>문에 1,000번을 적용한 후, 다음 내부 <code>for</code>문에 1,000번을 적용하면 1,000 \* 1,000 = 1,000,000 번이 된다.

결론은 첫 번째<code>O(N^2)</code>의 코드보다 두 번째 <code>O(N)</code>의 코드가 효율성에서 훨씬 낫다.

### ❗ 주의사항

> 정렬된 요소에서 해당 패턴 사용이 가능하다

## 💡 정리

> 빈도수 세기 패턴 개념은 보통 객체를 사용한다. 객체를 사용하여 프로파일을 구성하는 것은 배열이나 문자열의 내용을 분석하는 방법이다. 보통 배열이나 문자열과 같은 선형 구조를 구성한다. 그러면 해당 분석을 문자열이나 배열에서 생성된 다른 객체의 형태와 신속하게 비교할 수 있다.
