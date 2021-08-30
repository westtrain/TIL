# True false related questions that will trick you.

자바스크립트에서 참은 두가지가 존재한다. 하나는 true고 다른 하나는 거짓이 아닌 모든 것이다.

거짓은 7가지가 있는데 false, null, undefined, 빈문자열(''), 0, NaN 그리고 거짓인 모든 것이다

**Question:** Is `'false'` is false?

**Answer:** 아니다 왜냐하면 이것은 문자열이기 때문이다.
```js
false' === false // true
```
**Question:** Is `' '` is false?

**Answer:** 아니다. 이유는 이것이 빈문자열이 아니라 띄어쓰기 즉 whitespace가 들어가 있기 때문이다.
```js
' ' === false // false
'' === false // false

Boolean(' ') === false // false
Boolean('') === false // true
```
**Question:** What about `{}`?

**Answer: 이것은 참이다. 이유는 내부에 속성은 없지만 객체이기 때문이다.**
```js
{} === false // Uncaught SyntaxError, === 사용불가
Boolean({}) // true
```
**Question:** Tell me about `[]`?

**Answer: 참이다. JS에서는 배열도 객체로 인식한다. 그리고 여기서도 요소가 없어도 동일하게 적용된다.**
```js
[] === false // false (얘는 비교 연산은 된다)
Boolean([]) // true
```
**Question:** You talked about `''` to be falsy. What about `new String('')`?

**Answer:** 문자열 생성자에 빈문자열을 넣으면 문자열 객체가 생성된다. 따라서 이것은 참이다.
```js
new String('') // String {''}
new String() // String {''}
Boolean(new String('')) // true
Boolean(new String()) // true

String('') // ''
String() // ''
Boolean(String('')) // false
Boolean(String()) // false
```
**Question:** Tell me about `new Boolean(false)`

**Answer:** 참. 이유는 이전 문제와 마찮가지로 불리언 객체의 인스턴스를 생성하기 때문에 참이다.
```js
new Boolean(false) // Boolean {false}
new Boolean(false) === false // false
Boolean(new Boolean(false)) // true
```
**Question:** `Boolean(function(){})`

**Answer: 참이다. 함수는 그 자체로 참이다. 그러므로 블리언 생성자에 참을 넣으면 항상 참이 나온다.**
```js
Boolean(function(){}) // true
Boolean(() => {}) // true
```
**Question:** `Boolean(/foo/)`

**Answer: 참**

**Question:** `true%1`

**Answer:**  모듈러 계산은 나머지를 반환하는 것인데, 여기서 true는 1이 되어 1을 1로 나눈 나머지를 반환하게 된다. 그러면 0이 반환됨으로 이것은 거짓이 된다. 흥미롭게도 앞에 true대신 false를 넣어도 같은 값이 나오는데 이유는 false가 0이 되고 0을 1로 나눈 나머지도 0이기 때문이다.
```js
true % 1 // 0
Boolean(true % 1) // false

true % (-1) // 0
true % 2 // 1
true % 0 // NaN

1 % true // 0
```
**Question:** `''%1`

**Answer:** 거짓이다. 나머지는 0이 나오기 때문이다. 앞선 설명에서 알려주는 이유와 같다
```js
'' % 1 // 0
Boolean('' % 1) // false

' ' % 1 // 0
'h' % 1 // NaN
1 % '' // NaN true로는 몫 연산 되면서 아주 지멋대로다
```
