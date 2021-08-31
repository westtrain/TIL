# What the heck is this in JavaScript?

   함수가 실행될 때, 자바스크립트 엔진은 현재 실행 컨텍스트가 참조하는 함수를  `this` 라고 불리는 함수로 설정한다.  `this` 는 항상 객체를 참조하는데 함수를 호출하는 방법에 따라 달라진다. 

다음의 7가지 다른 경우들을 통해 `this` 가 무엇을 의미하는지 이해보자

1. 전역 컨텍스트 또는 함수 내부에서 `this` 는 window 객체를 참조한다.

    window 객체는 브라우저의 요소들과 자바스크립트 엔진, 그리고 모든 변수를 담고 있는 객체입니다.

    ```jsx
    function sum(a, b){
    // 여기서 this를 사용하면 전역변수와 window객체의 모든 값을 가져올 수 있다
    	this.open() // 새창을 여는 window객체의 메소드
    	return a + b;
    }
    // 하지만 this를 생략해도 문제는 없다.
    ```

2. 만약 IIFE 내부에서 "use strict"을 사용하면, `this` 는 undefined를 갖는다. 따라서 IIFE 내부에서 window 객체에 접근하려면 인자형태로 넘겨 받아야 한다.

    ```jsx
    "use strict";        // 만약 use strict를 사용하지 않으면 콘솔에는 윈도우 객체가 찍힌다.
    (function(a,b){
    console.log(this);   // undefined
    return a + b})(1,2)

    "use strict";
    (function(a,b,func){
    console.log(func);
    return a + b})(1,2,this.open)  // 이렇게 인자로 넘겨주면 콘솔에 open()함수가 찍힌다.
    console => ƒ open() { [native code] }
    ```

3. 객채의 컨텍스트에서 함수가 실행되는 동안,  객체는 `this` 의 값이 된다.

    ```jsx
    const obj  = { a : function(a,b){
                           console.log(this);
                           return a+b }
    	     }
    obj.a(1,2) // 객체에서 함수가 실행되는 동안 this는 객체를 가지고 있음을 콘솔보여준다.
    console => {a: ƒ}

    ```

4. setTimeout함수 내부에서 `this` 는 window 객체를 값으로 가진다.

    ```jsx
    setTimeout(function(){ alert("Hello"); }, 3000);
    // 나중에 추가 설명 필요.
    ```

5. 만약 생성자를 사용해 새로운 객체를 만들면 `this` 는 새로 생성된 객체의 참조 값을 가진다.

    ```jsx
    function MyFunc() {
        this.x = 100;
    		console.log(this);  // 콘솔에서 새로 만들어진 객체 MyFunc()를 this참조한다고 알려줌
    }

    let obj1 = new MyFunc(); // new keyword를 이용해서 새 객체를 만듬
    obj1.x;

    console => MyFunc {x: 100}

    // 만약 아래 코드처럼 함수를 선언하고 그냥 함수를 호출하면 윈도우 객체가 콘솔에 찍힌다.
    function MyFunc() {
        this.x = 100;
    		console.log(this); 
    }
    MyFunc();
    ```

6. 객체를 bind, call, apply의 첫번째 매개변수로 전달하여 임의의 객체에 `this` 의 값을 설정할 수 있다.

    ```jsx
    // 나중에 코드 추가
    ```

7. 돔 이밴트 핸들러에서는 이밴트를 발생시킨 요소가 `this` 의 값이 된다.

    ```jsx
    // 나중에 코드 추가
    ```
