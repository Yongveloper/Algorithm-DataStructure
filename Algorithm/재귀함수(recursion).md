# 재귀함수(recursion)

> 재귀는 자기 자신을 호출하는 절차다.

> 재귀 함수는 스스로를 호출한다.

## ❗ 갖춰야 하는 두 가지 요소

1. 기본적인 개념은 동일한 함수를 계속 호출하면서, 하나의 함수가 <strong>자기 자신을 재귀적으로 호출</strong>하게 하는 것
2. 종료 조건. 즉, <strong>재귀가 멈추는 시점</strong>

## ❓ 팩토리얼 함수 구현하기

### 1. 반복문으로 구현

```javascript
function factorial(num) {
  let total = 1;
  for (let i = num; i > 1; i--) {
    total *= i;
  }
  return total;
}
```

### 2. 재귀 함수로 구현

```javascript
function factorial(num) {
  if (num === 1) return 1;
  return num * factorial(num - 1);
}
```

## ❗ 재귀의 주의사항

    1. 종료 조건이 없거나 잘못되는 경우
    2. 잘못된 값을 반환 하거나, 반환 하는 걸 잊는 경우

## helper 메소드 재귀 ❓

> 헬퍼 메소드 재귀는 재귀형이 아닌 외부 함수가 재귀형인 내부 함수를 호출하는 형태이다.

> 헬퍼 메소드는 재귀와 함께 사용되는 설계 패턴이다.

## helper 메소드 재귀 예시

    홀수를 판별하는 함수를 작성

```javascript
collectOaddValues([1, 2, 3, 4, 5]); // [1, 3, 5]
```

### 1. helper 메소드 재귀 함수 코드

```javascript
function collectOddValues(arr) {
  let result = [];

  function helper(helperInput) {
    if (helperInput.length === 0) {
      return;
    }

    if (helperInput[0] % 2 !== 0) {
      result.push(helperInput[0]);
    }

    helper(helperInput.slice(1));
  }

  helper(arr);

  return result;
}
```

재귀적이지 않은 외부 함수가 재귀적인 내부 함수를 호출하는 패턴을 가지고 있다.

### 2. 일반 재귀 함수 코드

```javascript
function collectOddValues(arr) {
  let newArr = [];

  if (arr.length === 0) {
    return newArr;
  }

  if (arr[0] % 2 !== 0) {
    newArr.push(arr[0]);
  }

  newArr = newArr.concat(collectOddValues(arr.slice(1)));
  return newArr;
}
```

### ✅ helper vs Puer 차이

코드를 보면 helper 메소드 재귀가 훨씬 직관적으로 보인다. 하지만 두 번째 메소드를 만들려면 코드를 더 많이 작성해야 하지만 큰 문제는 아니다.

## 순수 재귀 함수 작성 팁

1. 배열을 사용하고 helper 메소드 없이 순수 재귀 함수를 작성하는 경우에 배열을 복사하는 <code>slice</code>, <code>spread 연산자(...)</code>, <code>concat</code> 같은 메소드를 사용하면 배열을 변경할 필요가 없다. 그러므로써, 결과를 축적할 수 있다.
2. 문자열은 변경할 수 없다. 그래서 <code>slice</code>나 <code>substring</code>을 사용해서 복사본을 만들어야 한다.
3. 객체의 경우, <code>Object.assign</code>이나 <code>spread 연산자(...)</code>를 사용하면 유용하다.
