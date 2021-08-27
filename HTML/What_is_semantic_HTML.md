# What is semantic HTML?

  Semantic HTML 또는 'semantically-correct HTML'이라고 불리는 이것은 의미론적인, 의미론적으로 정확한을 의미한다. 단어의 의미처럼 컨탠츠가 의미에 알맞게 선택되고 적용되도록 구조를 만들기 위해  테그를 사용한 HTML이다.

  예를 들어, ```<b></b>``` 와 ```<i></i>```는 잘 사용하지 않는데 이유는 컨텐츠의 구조나 의미와는 상관없이 컨텐츠를 포맷팅하기 때문이다. 그래서 대부분```<strong></strong>```이나 ```<em></em>```을 대신해서 사용해서 문자를 굵게 표시하거나 이테릭체로 변환시킨다. 이렇게 하면 컨텐츠의 구조상에 의미가 부여되어 태그안의 내용이 어떤 컨텐츠인지 식별이 쉽다.

# Why you would like to use semantic tag?

그러면 왜 시맨틱 테그를 쓰는 것이 좋은가?

  첫번째는 SEO때문이다. SEO는 Search Engine Optimization으로 검색 엔진 최적화를 의미한다. 검색 엔진을 가지고 있는 사이트는 봇을 사용해 각 사이트의 정보를 수집하는데 이때 SEO가 잘 만들어져 있는 사이트는 봇이 정보를 쉽게 수정하고 자신의 검색엔진에서 사이트 노출을 쉽게 하도록 도와준다. 시맨틱 테그가 봇이 정보를 수집하는데 최적화되도록 만들어주기 때문이다.

  두번째는 accessibility 즉, 접근성이 좋아지기 때문이다. 사이트는 다양한 디바이스나 브라우저를 통해서 접근하게 된다. 이때 시맨틱 테그를 사용한 사이트는 코드르 더 쉽게 interpret할 수 있기 때문에 접근성을 향상 시켜줄 수 있다. 특히 시각장애인들의 경우, 사이트를 눈으로 볼 수 없기 때문에 스크린 리더와 같은 문서를 소리로 읽어주는 특수 장치를 사용한다. 이때 시맨틱 테그가 빛을 발한다.

  세번째는 light code 즉, 코드가 간결해지고 가독성이 좋아진다. ```<div>, <span>```처럼 의미가 불분명한 테그를 이용해 코드를 작성하면 그 테그가 감싸고 있는 컨탠츠가 어떤 내용인지 바로 이해하기 힘들고 복잡하게 보일 수 있다. 시멘틱 테그는 그점을 수정해서 정확히 각 태그가 감싸고 있는 내용이 어떤 의미인지 한눈에 알아 볼 수 있게 만든다.

<img width="800" alt="Screen Shot 2021-08-26 at 9 22 15 PM" src="https://user-images.githubusercontent.com/24685076/130962016-49565474-9efc-44c8-9081-a4d171c9a6ce.png">


# What does “semantically correct” mean?

**Answer:** read it in [Stackoverflow](https://stackoverflow.com/questions/1294493/what-does-semantically-correct-mean/1294512#1294512)

## Labeling correctly

It means that you're calling something what it actually is. The classic example is that if something is a `table`, it should contain rows and columns of data. To use that for layout is semantically incorrect - you're saying "this is a table" when it's not.

Another example: a list (`<ul>` or `<ol>`) should generally be used to group similar items (`<li>`). You **could** use a `div` for the group and a `<span>` for each item, and style each `span` to be on a separate line with a bullet point, and it might look the way you want. But "this is a list" conveys more information.

## Fits the ideal behind HTML

HTML stands for "HyperText **Markup** Language"; its purpose is to mark up, or label, your content. The more accurately you mark it up, the better. New elements are being introduced in HTML5 to more accurately label common web page parts, such as headers and footers.

## Makes it more useful

All of this semantic labeling helps machines parse your content, which helps users. For instance:

- Knowing what your elements **are** lets browsers use sensible defaults for how they should **look and behave**. This means you have less customization work to do and are more likely to get consistent results in different browsers.
- Browsers can correctly apply your CSS (Cascading **Style** Sheets), describing how each type of content should look. You can offer alternative styles, or users can use their own; as long as you've labeled your elements semantically, rules like "I want headlines to be huge" will be usable.
- Screen readers for the blind can help them fill out a form more easily if the logical sections are broken into `fieldsets` with one `legend` for each one. A blind user can hear the `legend` text and decide, "oh, I can skip this section," just as a sighted user might do by reading it.
- Mobile phones can switch to a numeric keyboard when they see a form input of `type="tel"` (for telephone numbers).
