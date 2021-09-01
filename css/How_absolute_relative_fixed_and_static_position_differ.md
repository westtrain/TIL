# How absolute, relative, fixed and static position differ?

- absolute: 부모 엘리먼트 내부에 속박되지 않고, 독립된 배치 문맥(positioning context)을 가지게 된다. 마치 포토샵 같은 그래픽 툴에서 새로운 레이어를 추가하는 효과에 비슷하다고 생각하면 된다. 따라서, 엘리먼트를 기본적으로 브라우저 화면(viewport) 상에서 어디든지 원하는 위치에 자유롭게 배치시킬 수 있으며, 심지어 부모 엘리먼트 위에 겹쳐서 배치할 수도 있다. 단, 상위 엘리먼트 중에 `position` 속성이 `relative`인 엘리먼트가 있다면, 그 중 가장 가까운 엘리먼트의 내부에서만 엘리먼트를 자유롭게 배치할 수 있다. 즉, 전체 화면이 아닌 해당 상위 엘리먼트를 기준으로 offset 속성(`top`, `left`, `bottom`, `right`)이 적용된다.
- relative: element를 자기 자신의 상대적 위치에 배치한다. 예를 들어, element를 기준으로 위치를 상단으로부터 10칸으로 설정하면 원래 위치보다 10칸 아래에 위치한다.
- fixed: CSS의 fixed positioning은 브라우저의 전체 화면(viewport)을 기준으로 엘리먼트를 배치할 때 사용한다. CSS의 position 속성은 엘리먼트가 어떻게 배치되는가를 결정하는데, 이 속성의 값을 fixed로 지정해주면 fixed positioning이 적용된다. fixed positioning이 적용된 엘리먼트는 부모 엘리먼트로 부터 완전히 독립되어 다른 엘리먼트의 구애받지 않고 화면에 어디든지 원하는 위치에 자유롭게 배치될 수 있다. 또한, fixed positioning이 적용된 엘리먼트는 다른 엘리먼트들이 스크롤링(scrolling)되는 동안에도 지정된 자리에서 고정되어 움직이지 않는 특징을 가지고 있다.
- static: 문서의 보통의 흐름에 기반하여 element의 위치를 정해 배치한다. 일반적으로는 차례대로 왼쪽에서 오른쪽, 위에서 아래로 쌓인다.

    ref:

    [Engineering Blog by Dale Seo](https://www.daleseo.com/?tag=position)

    [(CSS) CSS 포지션(position) - static, relative, absolute, fixed](https://www.zerocho.com/category/CSS/post/5864f3b59f1dc000182d3ea1)
