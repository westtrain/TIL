### 코드 시간 재기

- `perfomance.now()`함수로 성능을 확인할 코드 앞뒤로 실행시켜 시간차를 계산(정밀도 5밀리세컨드)``
    
    ```jsx
    let t1 = performance.now();
    console.log(addToUp(100000000)); // 1부터 100000000까지 더하는 함수
    let t2 = performance.now();
    console.log(`Time Elapsed: ${(t2 - t1) / 10000} seconds.`);  
    // 초단위로 계산 후 출력
    ```
    
    - 작동 환경에 따라 재는 시간이 다를 수 있음
    - 같은 작동 환경에서도 재는 시간이 다르게 나올 수 있음
    - 빠른 알고리즘의 속도를 재는 충분하지 않을 수 있음
- `Date.now()`는 ms를 리턴하는데 시스템 시간에서 차이를 리턴한다.(오차 발생)
    - System time을 기반으로한 Date를 기준으로 실제 사용자를 모니터링하는 것은 적절치 않다. 대부분의 시스템은 정기적으로 시간을 동기화 하는 데몬을 실행한다. 그리고 그 시계는 15분 내지 20분 마다 몇 ms 씩 조정되는 것이 일반적이다. 따라서 그 속도에서 측정된 10 초간격의 1% 정도가 부정확할 것이다.
    Ref: [https://developers.google.com/web/updates/2012/08/When-milliseconds-are-not-enough-performance-now](https://developers.google.com/web/updates/2012/08/When-milliseconds-are-not-enough-performance-now)
- `Performance.mark` 와 `Performance.measure`
    - `Performance.mark`라는 이름에서 느껴지는 것 처럼, 코드 내에서 마킹을 할 수 있는 용도다.이 마크는 performance buffer에서 timestamp를 생성하여 나중에 코드의 특정 부분을 실행하는데 걸린 시간을 측정하는데 사용 가능하다. 마킹을 생성하기 위해서는, string을 파라미터로 함수를 호출해야 하며, 이 string은 나중에 식별자 용도로 사용된다. 마찬가지로 최대 정밀도는 **`5µs`**정도다.
    
    [performance.mark() - Web API | MDN](https://developer.mozilla.org/ko/docs/Web/API/Performance/mark)
    
    - `Performance.measure`함수는 1~3개의 arguments를 받는다. 첫번째 인수는 `name`이고, 나머지는 측정하고 싶은 마킹 영역을 넣으면 된다.
    
    [https://developer.mozilla.org/en-US/docs/Web/API/Performance/measure](https://developer.mozilla.org/en-US/docs/Web/API/Performance/measure)
    
- `performance entry buffer`로 결과 데이터 수집
    - 측정 결과가 `performance entry buffer`에 수집되는데, 여기에 접근하여 값을 가져오기 위해 performance API는 3종류의 api를 제공한다.
    - `performance.getEntries()`: `performance entry buffer`에 저장된 모든 것을 보여준다.
    - `performance.getEntriesByName('name')`
    - `performance.getEntriesByType('type')`: 특정 타입에 대해서만 보여준다. `measure`, `mark`만 가능
        
        ```jsx
        performance.mark('mark-1')
        // 성능을 측정할 코드
        performance.mark('mark-2')
        performance.measure('test', 'mark-1', 'mark-2')
        console.log(performance.getEntriesByName('test')[0].duration)
        ```
        
- `console.time` 을 통해서 간단하게 측정하기
    - 단순히 `console.time`을 호출하고, 측정 종료 시점에 `console.timeEnd`를 호출하면 된다.
        
        ```jsx
        console.time('test')
        // 성능을 측정할 코드
        console.timeEnd('test')
        ```
### 시간복잡도 시각화(Time Complex Visualization)

- 아래의 함수를 통해서 연산자 갯수가 함수 실행 속도에 얼마나 영향을 주는지 그래프로 확인해보자
    
    ```jsx
    function addUpToSecond(n){
    	return n * (n + 1) / 2;
    }
    ```
    
    - n = 10000인 경우 아래의 그래프가 만들어진다. y축의 단위는 마이크로초이다.
        
        ![Screen Shot 2022-08-10 at 12.48.55 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9738efd7-a76d-4d37-8c49-7654ddca0da3/Screen_Shot_2022-08-10_at_12.48.55_AM.png)
        
    - n = 100000인 경우, 아래의 그래프를 만듬
        
        ![Screen Shot 2022-08-10 at 12.50.11 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ee84456-21f8-484c-a50a-ffed3c7f0d47/Screen_Shot_2022-08-10_at_12.50.11_AM.png)
        
    - 단순하게 보면 그래프가 크게 변동되어 속도에 큰 영향을 주는 것 같지만 사실 y축은 단위가 마이크로초이기 때문에 변동폭이 크다고 볼 수 없다. 연산자가 아무리 많아도 속도에 큰 영향을 주지 않는다.
    - 아래의 함수를 통해 반복 연산이 실행 속도에 얼마나 영향을 주는지 살펴보자.
        
        ```jsx
        function addUpToFirst(){
        	var total = 0;
        	for(let i = 0; i <= n; i++){
        		total += 1;
        	}
        	return total;
        }
        ```
        
        - n = 10000인 경우, 파란색 그래프처럼 나타나고 아래의 회색 그래프보다 속도가 매우 느린 것을 확인할 수 있다.
            
            ![Screen Shot 2022-08-10 at 12.54.47 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56869402-2b92-44d5-ba83-15ea868464c9/Screen_Shot_2022-08-10_at_12.54.47_AM.png)
            
        - n = 1000000000인 경우, 속도는 1초를 넘어섰다. (파란색 그래프)
            
            ![Screen Shot 2022-08-10 at 12.56.12 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7accf692-f954-482d-86a1-6d9b747a6ea1/Screen_Shot_2022-08-10_at_12.56.12_AM.png)
            
- 두 함수가 만드는 그래프를 통해서 시간복잡도에 연산자의 숫자로만 이루어진 함수가 훨씬 유리하다는 점을 확인 가능하다.
