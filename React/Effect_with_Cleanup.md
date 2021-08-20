# Memory Leak When using useEffect
## Case
```javascript
export const App = () => {
  const handleCardClick = (e) => {
    setClickMovie(e);
  };
  const [movies, setMoviesList] = useState(mockMovie);
  useEffect(() => {
    getMovies()
      .then(data => {
          setMoviesList(data);
      })
}, []);

  return (
    <>
      <div className='header'>
        <Header />
      </div>
      <div className='body'>
        <MovieRankList movies={movies} handleCardClick={handleCardClick} />
      </div>
    </>
  );
};
```
위의 에시 코드에서 state에 getMovies() 함수를 통해 전달받은 데이터를 setState하고 그 데이터를 props로MovieRankList 컴포넌트에 전달해서 영화 리스트를 화면에 랜더링할 수 있도록 구현되어 있다. 그리고  setState는 useEffect안에서 작동하게 되어 있어서 state의 데이터가 변경될 때 재랜더링할 수 있도록 구현되어 있다.
그런데 문제는 이 코드에서 메모리 누수 혹은 충돌이 발생할 수 있다는 것이다. (실제 코드를 서버에서 실행했을때 간헐적으로 setState가 반복되고 랜더링도 반복되는 현상이 발견되었다)
이러한 문제가 발생하는 이유에 관해 공식 문서에서는 다음과 같이 알려준다
" When exactly does React clean up an effect? React performs the cleanup when the component unmounts. However, as we learned earlier, effects run for every render and not just once. This is why React also cleans up effects from the previous render before running the effects next time. We’ll discuss why this helps avoid bugs and how to opt out of this behavior in case it creates performance issues later below.
또한 Dan Abranmov의 'A Complete Guide to useEffect' 번역본에서는 이렇게 알려준다
" 컴포넌트가 랜더링 안에 있는 모든 함수는 (이벤트 핸들러, 이펙트, 타임아웃이나 그 안에서 호출되는 API 등) 랜더가 호출될 때 정의된 props와 state 값을 잡아둔다.
## Solution
```javascript
useEffect(() => {
    let unmounted = false;
    getMovies()
      .then(data => {
        if(!unmounted){
          setMoviesList(data);
        }
      })
      // .catch(error => {error.message});
      return () => {unmounted = true;}
}, []);
```
위 코드에서처럼 변수를 선언해 useEffect가 Cleanup없이 리랜더링하지 못하도록 방지할 수 있다.

## Conclude
공식 문서와 위에 언급된 책의 내용을 근거로 보자면 랜더링의 작동 원리와 관련이 있는 것으로 생각이 든다. 리엑트는 브라우저가 페인트를 하고 난 이후에 이펙트를 실행하기 때문에 스크린 업데이트를 가로막지 않고 빠르게 앱을 만들 수 있는 장점이 있지만 이로 인해 이펙트의 Cleanup이 미루질 수 있다. 그러는 바람에 Effect 새로 전달 받은 props의 값으로 리렌더링된 이후에 Cleanup을 하게 된다. 이때 Cleanup은 여전히 이전 props값을 보고 있다. 즉, Cleanup이 정의된 시점의 랜더링에 있던 값을 읽어오는 것이다. 그로인해 이전 값과 새로 받은 값이 충돌되어 메모리 누수가 날 수 있다는 것이다. 
완벽한 정리가 아니라 추후 수정과 업데이트가 있을 수 있다.

## 이점과 관련되 더 배워야 할 부분
라이프사이클..

## References
[React Official Docs]: https://reactjs.org/docs/hooks-effect.html
[A Complate Guide to useEffect]: https://rinae.dev/posts/a-complete-guide-to-useeffect-ko#%EA%B7%B8%EB%9F%AC%EB%A9%B4-%ED%81%B4%EB%A6%B0%EC%97%85cleanup%EC%9D%80-%EB%AD%90%EC%A7%80

