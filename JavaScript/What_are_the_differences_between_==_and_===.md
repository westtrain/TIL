# What are the differences between == and ===?

간단히 설명하면, 동등 연산자(==)은 데이터 타입은 확인하지 않고 비교하고 일치 연산자(===)은 같은 데이터 타입안에서 값을 비교하는 것이다. ==는 내부에서는 비교 대상을 같은 타입으로 바꾸어 비교하여 상대적으로 관대한 비교를 한다.

===는 데이터 타입과 값을 모두 비교한다. 그래서 두개 모두 같을때만 참을 반환하고 다르면 거짓을 반환한다.

예를 들어, 두 문자열을 비교할 때 완전히 동일한 문자열을 비교해야 참을 반환시킬 수 있다. 단지 문자열이라는 데이터 타입만 같고 문자열 속의 단 하나의 글자라도 다르면 거짓을 반환한다. 원시자료형 타입(number, boolean)역시 정확히 같은 값을 가지고 있어야 참을 반환한다.

앞서 동등 연산자(==)는 내부에서 데이터 타입을 바꾸어 관대한 비교를 한다고 했다. 그와 같은 과정에는 규칙이 존재하는데 다음과 같다.

- 만약 두 비교 대상의 데이타 타입이 같다면 일치 연산자(===)처럼 비교한다
- undefined == null
- 만약 데이터 타입이 한쪽이 문자열이고 다른 쪽은 숫자라면, 문자열을 숫자로 바꾸어 비교한다.
- 만약 데이터 타입이 한쪽이 boolean이고 다른 쪽은 non-boolean이면, boolean을 숫자로 바꾼 후 비교한다.
- 객체에서 문자열과 숫자를 비교할땐, 객체를 원시자료형을 바꾸어 비교한다.

객체와 배열은 참조 자료형이기 때문에 동등 연산자나 일치 연산자로 비교할 수 없다. 다만 식별자 번호 즉, 인덱스 번호 또는 키를 이용하여 각 요소를 비교할 수는 있다.

```jsx
let arr1 = [1,2];
let arr2 = [1,2];
arr1 == arr2;       // false
arr1 === arr2;      // false
arr1[1] == arr2[1];  // true
arr1[1] === arr2[1]; // true

let obj1 = {a:1};
let obj2 = {a:1};
obj1 == obj2;        // false
obj1 === obj2;       // false
obj1['a'] == obj2['a'];        // true
obj1['a'] === obj2['a'];        // true

```

추가적으로 NaN, null 그리고 undefined는 다른 모든 데이터 타입과 일치 연산자(===)를 사용해 비교했을 때 반드시 거짓을 반환한다. 심지어 NaN은 자기 자신과 일치 연산자와 비교해도 거짓을 반환한다.

```jsx
// Number
NaN === 1          // false
null === 1         // false
undefined === 1    // false

// String
NaN === '1'         // false
null === '1'        // false
undefined === '1'   // false

//Boolean
NaN === true        // false
null === true       // false
undefined === true  // false

NaN === false       // false
null === false      // false
undefined === false // false

// NaN
NaN === NaN         // false
```
