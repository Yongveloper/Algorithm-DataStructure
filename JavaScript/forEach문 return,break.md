# Array.forEach()에서 return 또는 break 안 되는 이유

## 1. 궁금했던 이유 ❓

알고리즘 문제를 푸는데 반복문을 사용해야 하는 상황이 있어서, 간편한 <code>forEach</code>문을 사용하려 했다.

해당 조건이 만족하면 순회를 멈추고 빈 값을 <code>return</code>해서 반복문을 멈추도록 의도하고 싶었지만 <code>forEach</code>문은 조건이 만족해도 <code>continue</code>를 사용한 것 처럼 건너띄어지고 순회는 멈추지 않았다.

<code>break</code>도 역시 중단이 되지 않았다.

### 예시 코드

```javascript
const array = [1, 2, 3, 4, 5];
array.forEach((num) => {
  if (num === 2) return num;
  console.log(num);
});
return array;
```

### 내 예상 결과

```
1
2
```

### 코드 결과

```
1
3
4
5
```

## 2. <code>return</code>과 <code>break</code> 문이 동작할 거라 생각한 이유 ❓

<code>forEach</code>문 외에도 일반적인 <code>for</code>, <code>for...of</code>, <code>while</code>문 에서는 <code>return</code>과 <code>break</code>가 모두 동작하기 때문에 같은 반복문이라 생각했던 나는 당연히 동작할 것이라고 생각했다.

## 3. <code>forEach</code>에서 <code>return</code>과 <code>break</code>문이 동작하지 않는 이유 💡

<img src="https://user-images.githubusercontent.com/64254228/220912452-37bb014d-f386-4091-9c23-b516eb041994.png" width="800px" height="400px" title="MDN forEach" alt="동작하지 않는 이유"></img><br/>
참고 [MDN 공식문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#%EC%84%A4%EB%AA%85)

### <strong>1. <code>return</code>이 동작하지 않는 이유</strong>

<code>forEach</code> 메서드는 반복문의 각 요소마다 콜백 함수를 호출하며, 콜백 함수 내에서 <code>return</code> 키워드를 사용해도 해당 값은 반환되지 않는다.

이는 <code>forEach</code> 메서드가 반환하는 값이 항상 <code>undefined</code>이기 때문이다. <code>forEach</code> 메서드는 반복문이 동작하는 동안 배열을 변경할 수 있는 기능이 있기 때문에, <code>return</code> 문을 사용하여 값을 반환한다면 코드의 의도를 파악하기 어려워질 수 있다.

만약, 반복문 중간에 <code>return</code>을 사용하여 반복문을 중단하고 싶은 경우에는 <code>forEach</code> 대신에 <code>for...of</code> 루프를 사용하거나, <code>some</code> 또는 <code>every</code>와 같은 적절한 배열 메서드를 사용하는 것이 좋다.

### <strong>2. break문이 동작하지 않는 이유</strong>

<code>forEach</code> 메서드가 <code>ECMAScript</code> 명세에 따라 설계된 메서드이기 때문이다.

반면에, <code>for</code> 루프나 <code>while</code> 루프에서는 <code>break</code> 키워드를 사용하여 반복문을 중단할 수 있습니다. for 루프나 <code>while</code> 루프를 사용하면 <code>break</code> 키워드를 사용하여 반복문을 중단하거나 <code>continue</code> 키워드를 사용하여 다음 반복으로 건너뛸 수 있다.

만약 <code>forEach</code> 메서드에서 반복문을 중단하려면, <code>some</code> 메서드나 <code>every</code> 메서드 등 적합한 다른 배열 메서드를 사용하거나, <code>for...of</code> 루프를 사용하는 것이 좋다. 이러한 방법은 콜백 함수 내에서 <code>return</code> 키워드를 사용하여 반복문을 중단할 수 있다.
