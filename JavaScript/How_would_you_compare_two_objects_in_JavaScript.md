# How would you compare two objects in JavaScript?

기본적인 이해: 자바스크립트는 값을 비교하기 위한 두가지 다른 접근법이 있다. 하나는 원시형 타입 즉, 문자열과 숫자인데 이것은 값 자체만으로도 서로 비교할 수 있다. 다른 하나는 참조 자료형인데 즉, 배열과 사용자가 정의한 객체들이 있는데 이것들은 참조 자료에 의해 비교된다. 다시 말해 두 객체가 같은 메모리 주소를 참조하는지를 비교하는 것이다.

질문에서 두개의 객체가 같은지의 여부를 확인하는 방법은 참조하는 주소를 말하는 것이 아니다. 두 객체가 같은 객체인지 비교하는 보통의 방법은 각 객체가 같은 속성과 같은 값을 가지고 있는지 확인하는 것이다. 그래서 비교하기 위해 두 객체에서 키를 가져와야 한다. 먼저, 속성의 개수가 같은지 확인해서 같으면 이 두 객체는 같다고 할 수 없다. 다음으로는 객체의 각각의 속성이 같은 값을 가지고 있는지 확인하는 것이다. 만약 모든 속성들이 같은 값을 가지고 있다면 그 두 객체는 같다고 할 수 있다. 

코드를 통해 예를 들어보자

```jsx
const obj1 = {a:1,b:2};
const obj2 = {a:1,b:2};
const obj3 = {a:1};
const obj4 = {a:1,b:1};
// 위 4개의 객체가 같은 확인하기 위한 함수를 만들어보자
function isEqual(a, b) {
    let aProps = Object.getOwnPropertyNames(a);  
    let bProps = Object.getOwnPropertyNames(b);

    if (aProps.length != bProps.length) {       // 속성의 개수 즉 키의 개수가 같은지 확인
        return false;
    }

    for (var i = 0; i < aProps.length; i++) {   
        var propName = aProps[i];
        
        if (a[propName] !== b[propName]) {      // 각 키가 가지고 있는 값이 같은지 비교
            return false;
        }
    }
    return true;
}

isEqual(obj1, obj2);      // 두 객체는 같다
isEqual(obj1, obj3);      // 두 객체는 다르다. 이유는 속성의 개수가 다르기 때문에
isEqual(obj1, obj4);      // 두 객체는 다르다. 이유는 키가 가지고 있는 값이 다르기 떄문에

```
