# What are the differences between null and undefined?

> 자바스크립트에는 비었다를 설명하는 두개의 특별한 값이 있다.

## undefined

undefined는 변수의 값이 정의되지 않았음을 의미한다. 자바스크립트는 전역 변수를 undefined로 가지고 있는데 typeof undefined로 데이터 타입을 확인해도 undefined라고 나온다. 기억해야 할 점은 undefined는 상수(constant)나 키워드가 아니라는 것이다. undefined는 하나의 undefined라는 값인 동시에  데이터 타입이기도하다. undefined에  새로운 값을   할당해도  undefined 타입의 값은 변경되지 않는다.

### undefined가 나오는 8가지 경우

- 값을 주지 않고 변수를 선언하는 경우

    ```jsx
    let value; 
    console.log(value);
    ```

- 리턴값이 존재하는 함수에 리턴하는 코드가 빠진 경우

    ```jsx
    function plus(a,b){
    	let sum = a + b;
    }
    plus(1,2);
    ```

- 명시적으로 반환할 필요가 없는 함수의 경우

    ```jsx
    const originalArr = [1,2];
    function swap(arr){
    	let temp = arr[0];
    	arr[0] =  arr[1];
    	arr[1] = temp;
    }
    swap(originalArr); 
    ```

- 객체 안에 존재하지 않는 속성을 찾는 경우

    ```jsx
    const obj = {a:1,b:2};
    console.log(obj['c']); // undefined
    ```

- 함수의 파라미터에 아무것도 들어오지 않은 경우

    ```jsx
    function func(a){
    	console.log(a) // a는 undefiend 
    }
    func();
    ```

- undefined로 값이 설정된 경우

    ```jsx
    let value = undefined;
    ```

- void형태로 만들어진 모든 표현식의 경우

    ```jsx
    let test = void(1+2);
    console.log(test);
    // undefiend
    // 1+2 를 수행하지만 test 변수에는 undefined 가 됩니다.
     
    let test2 = void(test = 10);
    console.log(test2);
    // undefiend
    console.log(test);
    // 10
    ```

- 전역 변수의 기본값의 경우 (var에 해당)

    ```jsx
    var value; // undefined로 초기화된다
    ```

## null

null은 프로그래머가 값이 비었다 또는 값이 존재하지 않는다는 의미를 전달하기 위해 사용한다. null은 원시 자료형의 값이고 어떤 변수에도 할당할 수 있다. 
때때로 null이 객체라고 오해하는 경우가 있는데 이유가 typeof를 통해 데이타 타입을 확인하면 object가 나오기 때문이다. 그러나 null은 객체가 아니라 원시 자료형이다.

참고로, 두 값은 분명 다른 값이지만 동시에 같다라고 할 수 있다. 

```jsx
null == undefined // true
```
