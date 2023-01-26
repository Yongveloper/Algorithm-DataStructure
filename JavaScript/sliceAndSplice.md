# JavaScript Array Methods <code>slice()</code> vs <code>splice()</code>

## 💡 <code>slice()</code> 배열 메서드

> <code>slice()</code> 메서드는 <strong>배열의 복사본을 만들거나 배열의 일부를 반환하는 데 사용할 수 있다.</strong>

> <code>slice()</code> 메서드는 원래 배열을 변경하지 않고 대신 <strong>얕은 복사본</strong>을 생성 한다는 점에 유의해야 한다 .

기본 구문은 다음과 같다.

```javascript
slice(optional start parameter, optional end parameter)
```

이 예시에서는 과일 목록을 만들었다.

```javascript
const fruits = ['apple', 'banana', 'mango', 'melon'];
```

### <code>slice()</code> 메서드를 매개변수 없이 사용하는 방법 ❓

<code>slice()</code> 메서드를 활용해 해당 배열의 얕은 복사본을 만들 수 있다.

```javascript
console.log(fruits.slice()); // ['apple', 'banana', 'mango', 'melon']
```

## start 매개변수를 사용해서 <code>slice()</code> 메서드를 사용하는 방법 ❓

옵션으로 줄 수 있는 start 매개변수를 사용해서 배열에서 요소를 선택하기 위한 시작 위치를 설정할 수 있다.

이 예시에서는 index 2를 시작 우치로 설정해서 index 2부터 마지막 index까지 선택해서 새 배열로 반환한다.

```javascript
const newFruits = fruits.slice(2);

console.log(newFruits); // ['mango', 'melon']
```

원래 배열은 수정되지 않는 것을 볼 수 있다.

```javascript
const fruits = ['apple', 'banana', 'mango', 'melon'];

const newFruits = fruits.slice(2);

console.log('원래 과일: ', fruits); // ['apple', 'banana', 'mango', 'melon']
console.log('새로운 과일: ', newFruits); // ['mango', 'melon']
```

배열 끝에서 부터 선택하고 싶다면 음수 index를 사용할 수도 있다.

```javascript
const newFruits = fruits.slice(-1);

console.log(newFruits); // ['melon']
```

start 매개변수가 배열의 마지막 index 보다 크면 빈 배열이 반환된다.

```javascript
const newFruits = fruits.slice(4);

console.log(newFruits); // []
```

## start 와 end 매개변수를 사용하여 <code>slice()</code> 메서드를 사용하는 방법 ❓

end 위치가 지정된 경우 <code>slice()</code> 메서드는 start 위치에서 end 위치까지 요소를 추출한다.

<strong>end 위치는 새로운 배열의 추출된 요소에 포함되지 않는다.</strong>

```javascript
const fruits = ['apple', 'banana', 'mango', 'melon'];

const newFruits = fruits.slice(1, 3);

console.log(newFruits); // ['banana', 'mango'];
```

## 💡 <code>splice()</code> 배열 메서드

> <code>slice()</code> 메서드와 달리 <code>splice()</code> 메서드는 <strong>원래 배열의 내용을 변경한다.</strong>

> <code>splice()</code> 메서드는 기존 배열의 요소를 추가하거나 제거하는 데 사용되며 반환 값은 <strong>배열에서 제거된 항목이 반환 된다.</strong>

<code>splice()</code> 메서드의 기본 구문은 다음과 같다.

```javascript
splice(start, optional delete count, optional items to add)
```

이 예시에는 요일 항목의 배열이 있다.

```javascript
const week = ['Mon', 'Tue', 'Wen', 'Thu', 'Fri'];
```

## <code>splice()</code> 메서드 사용해서 요소를 추가하는 방법 ❓

배열의 index 1에 다른 요일을 추가하려면 다음과 같이 할 수 있다.

```javascript
week.splice(1, 0, 'Sat');
```

첫 번째 숫자는 시작 index고, 두 번째 숫자는 삭제 횟수다.

아무 항목도 삭제하지 않으므로 삭제 회수는 0이다.

```javascript
const week = ['Mon', 'Tue', 'Wen', 'Thu', 'Fri'];

week.splice(1, 0, 'Sat');

console.log(week); // ['Mon', 'Sat', 'Tue', 'Wen', 'Thu', 'Fri'];
```

## <code>splice()</code> 메서드를 사용해서 요소를 제거하는 방법 ❓

이 예시에서는 배열에서 "Wen"을 제거하려고 한다. start 및 delete 매개변수를 사용해서 제거할 수 있다.

```javascript
week.splice(2, 1);
```

숫자 2는 시작 위치이고, 숫자 1은 삭제 횟수를 나타낸다. "Wen"은 index 2에 위치해 있으므로 배열에서 제거된다.

```javascript
const week = ['Mon', 'Tue', 'Wen', 'Thu', 'Fri'];

week.splice(2, 1);

console.log(week); // ['Mon', 'Tue', 'Thu', 'Fri'];
```

## 📕 결론

<code>slice()</code> 와 <code>splice()</code> 메서드는 서로 비슷해 보일 수 있지만 몇 가지 주요 차이점이 있다.

<code>slice()</code> 메서드는 <strong>배열의 복사본을 만들거나 배열의 일부를 반환 하는데 사용할 수 있고, 원래 배열을 변경하지 않고 대신, 얕은 복사본을 생성한다.</strong>

<code>splice()</code> 메서드는 <strong>원래 배열의 내용을 변경하고, 기존 배열의 요소를 추가 하거나 제거하는 데 사용되며 반환 값은 배열에서 제거된 항목이 된다.</strong>

배열에서 아무 것도 제거되지 않은 경우 반환 값은 빈 배열이다.
