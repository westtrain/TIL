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
