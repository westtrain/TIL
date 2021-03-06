# What is doctype? Why do u need it?

doctype은 Document Type Definition의 약자인 DTD라고 부르는데 문자 그대로 번역하면 문서 형식을 정의해주는 것이라고 말할 수 있다.

DTD의 역할은 HTML이 어떤 버전으로 작성되었는지 미리 선언해 웹브라우저가 내용을 올바로 표시할 수 있도록 해주는 것이다.

대부분의 브라우저에서 요소를 페이지에 표시하는 방법을 보장합니다. 또한 브라우저를 좀 더 편리하게 사용할 수 있게 해줍니다. 만약 doctype이 불분명하면 브라우저는 문제를 인식하고 쿼크 모드( 추가적으로 이해가 필요한 부분에서 설명 )로 전환됩니다. 또한 마크업의 유효성을 확인하는데도 Doctype이 필요합니다.

- 추가적으로 이해가 필요한 부분

    브라우저가 HTML문서를 처리를 할 경우, HTML DTD가 있으면 그에 맞는 W3C에서 정의한 방식에 따라 처리를 한다. 이를 표준모드라고 하며, 그렇지 않은 경우를 쿼크모드라고 한다.

    쿼크모드에서는 브라우저 회사마다 정의된 방식에 따르며, 그 결과에 차이를 보인다. 대표적으로 박스모델에서 폭(width)과 높이(height)의 여백처리는 IE가 W3C의 표준과 달리 처리하기에 다른 결과를 보인다.

    그러하기에 HTML DTD를 꼭 명시하여, 표준모드로 브러우저가 처리할 수 있게 해야 한다. 이것이 웹표준을 위한 첫 시작이다.

    doctype은 html 파일의 상단에 선언되고 닫히는 테크는 없고 대소문자를 구분하지 않는다

    HTML 4.01에서 DOCTYPE 선언은 SGML을 기반으로 하기 때문에 DTD를 참조해야 한다. 

    하지만 HTML5는 SGML을 기반으로 하지 않기 때문에 DTD를 참조할 필요가 없다.


ref:

[don't forget doctype](https://www.w3.org/QA/Tips/Doctype)

[https://tuhbm.tistory.com/2](https://tuhbm.tistory.com/2)
