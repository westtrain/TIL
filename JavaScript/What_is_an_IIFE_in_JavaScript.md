# What is an IIFE in JavaScript?

IIFE는 Immediately Invoked Function Expression의 약자로 번역하면 즉시 실행 함수 표현이다. 

간단하게 말하면 정의되자마자 즉시 실행되는 함수를 가리킨다.

이것은 Self-Execution Anonymous Function 즉, 스스로 실행하는 익명 함수의 디자인 패턴이다. 여기에는 크게 두 부분이  포함된다.

1. 괄호로 둘러싸인 익명함수: 이것은 전역 스코프에 불필요한 변수를 선언해서 오염되지 않도록 방지한다. 그리고 IIFE 내부 안으로 다른 변수의 접근을 막을 수 있다.
2. 즉시 실행 함수를 생성하는 (): 자바스크립트 엔진이 직접 interpret해서 함수를 실행시킨다.

```jsx
// 일반 함수의 경우
function sum(a,b){
	return a + b;
}

// IIFE의 경우
(function (a,b){
	return a + b;
})()

// IIFF에서 변수의 오염으로부터 방지되는 이유
(function (){
	// code ..
	let firstVariable;
	// code ..
})();
// 이 경우 IIFE함수는 즉시 실행되고 내부의 변수 firstVariable은 실행이 끝나는 순간 정리된다
// 그래서 다시 사용할 수 없기 떄문에 오염으로부터 방지될 수 있다.
// 좀 더 복잡한 코드를 보자

// 아래는 계좌에 돈을 넣고 뺄때 남은 금액을 보여주는 함수로 IIFE패던으로 작성되었다
const makeWithdraw = balance => (function(copyBalance) {
  let balance = copyBalance; // This variable is private
  let doBadThings = function() {
    console.log("I will do bad things with your money");
  };
  doBadThings();
  return {
    withdraw: function(amount) {
      if (balance >= amount) {
        balance -= amount;
        return balance;
      } else {
        return "Insufficient money";
      }
    },
  }
})(balance);

// 먼저 함수를 100과 함께 실행한 결과를 변수 firstAccount에 넣는다
// 이 경우 보통은 그냥 firstAccount가 makeWithdraw함수를 가지고 있어서 
// firstAccount라는 이름으로 함수를 부를 수 있다.
// 근데 makeWithdraw함수는 IIFE패턴으로 만들었기 때문에 이 과정에서 즉시 실행된다
// 그래서 balnce에 100이 들어가고 doBadThings가 실행되어 콘솔에 문장을 표시한다.
const firstAccount = makeWithdraw(100); // "I will do bad things with your money"

// 그런데 아래처럼 balance가 가지고 있는 금액을 확인하기 위해 찍으면 100이 나오는게 아니라 
// undefined가 나온다.
console.log(firstAccount.balance); // undefined

// 내부 콜백 함수인 withdraw를 호출해서 금액을 넣으면 처음에 넣은 100에서 20을 뺀 80이 반환된다.
console.log(firstAccount.withdraw(20)); // 80
// 또한 내부 함수인 doBadThings에는 private이라 접근할 수도 없다
console.log(firstAccount.doBadThings); // undefined, this method is private

// 변수 balnce는 100이라는 값을 가지고 있지만 firstAccount는 접근하거나 열람할 수 없다
// 이렇게 내부 변수를 외부의 오염으로부터 보호할 수 있다

const secondAccount = makeWithdraw(20); // "I will do bad things with your money"
secondAccount.withdraw(30); // "Insufficient money"
secondAccount.withdraw(20);  // 0
```

Ref: 

[IIFE - MDN Web Docs Glossary: Definitions of Web-related terms | MDN](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)
