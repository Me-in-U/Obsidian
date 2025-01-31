---
tags: html, flexbox, layout, grid
---
## [그리드 레이아웃이란 무엇인가?](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids#%EA%B7%B8%EB%A6%AC%EB%93%9C_%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83%EC%9D%B4%EB%9E%80_%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)

그리드는 수평선과 수직선으로 이루어진 집합체로, 디자인 요소를 정렬할 수 있는 대상 패턴을 생성한다. 이 디자인은 페이지에서 페이지로 이동할 때 요소가 널뛰거나 너비가 바뀌지 않는 디자인 생성에 도움을 주어 웹 사이트의 일관성을 높여준다.

하나의 그리드은 대게 **columns**, **rows**로 구성되며, 각 행과 열 사이에 공백이 있는데, 대게는 이를 일컬어 **gutters**라고 부른다.

[`display`](https://developer.mozilla.org/ko/docs/Web/CSS/display) 속성에 `grid` 값을 사용해 그리드를 규정한다. 이로써 Flexbox와 마찬가지로 그리드 레이아웃으로 전환하며, 컨테이너의 직계 자식 전체가 그리드 아이템이 됩니다. 내려받은 시작 파일 내부 CSS 부분에 다음을 추가하세요:

```css
.container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
			or grid-template-columns: repeat(3, 1fr);
}
```


![[Pasted image 20250116104449.png]]
### [트랙사이 간격](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids#%ED%8A%B8%EB%9E%99%EC%82%AC%EC%9D%B4_%EA%B0%84%EA%B2%A9)

우리가 트랙사이 간격을 생성하려면 열 사이 간격에 대해선 [`grid-column-gap` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/column-gap) 속성을 사용하고, 행 사이 간격에 대해선 [`grid-row-gap` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/row-gap)를 사용하고, 단번에 둘 다 설정하려면 [`grid-gap` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/gap)를 사용한다.

```css
.container {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    grid-gap: 20px; or gap: 20px;
}
```

![[Pasted image 20250116104503.png]]

### [암시적 그리드와 명시적 그리드](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids#%EC%95%94%EC%8B%9C%EC%A0%81_%EA%B7%B8%EB%A6%AC%EB%93%9C%EC%99%80_%EB%AA%85%EC%8B%9C%EC%A0%81_%EA%B7%B8%EB%A6%AC%EB%93%9C)

지금까지는 열 트랙만 지정했지만, 콘텐츠를 저장하기 위해 행도 만들어지고 있다. 이것은 명시적 그리드 대항 암시적 그리드의 한 예다. 명시적 그리드는 당신이 `grid-template-columns` 또는 `grid-template-rows`를 사용하여 생성하는 것을 말한다. 암시적 그리드가 생성되는 시점은 콘텐츠가 해당 그리드 외부에 배치될 때이다. 예를 들어 콘텐츠가 행렬 내부에 진입할 시점이 된다. 명시적 및 암시적 그리드는 가변상자의 주축 및 교차축과 유사하다.

기본값으로 암시적 그리드 상에 생성된 트랙은 `auto` 크기로 되며, 이는 일반적으로 콘텐츠를 알맞게 들여놓기에 충분히 크다는 것을 의미한다. 당신이 암시적 그리드 트랙에 크기를 지정하려면 [`grid-auto-rows` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-rows)와 [`grid-auto-columns` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-columns) 속성을 사용할 수 있다. 당신의 작업 CSS에 `100px`값을 `grid-auto-rows`에 추가하게 되면 생성된 행이 이제 100 픽셀 높이가 되는 걸 보게 된다.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 100px;
  grid-gap: 20px;
}
```

![[Pasted image 20250116104525.png]]
### [minmax() 함수](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids#minmax_%ED%95%A8%EC%88%98)

100픽셀 높이의 트랙은 100픽셀 이상의 트랙에 콘텐츠를 추가할 경우 별로 유용하지 않을 것이다. 그 경우 오버플로를 야기하니 말이다. _적어도_ 100픽셀 높이의 트랙이 있고, 거기에 더 많은 콘텐츠가 들어가더라도 여전히 확장될 수 있다면 더 나을 수 있다. 웹에 관한 상당히 기본적인 사실은 어떤 것의 높이가 앞으로 얼마나 커질지 결코 모른다는 점이다. 추가 내용 또는 더 큰 글꼴 크기는 모든 면에서 픽셀 크기의 완전성을 추구하는 디자인의 경우 문제를 일으킬 수 있다.

`minmax`는 트랙의 최소 및 최대 크기를 설정할 수 있게 해준다. 예를 들어 `minmax(100px, auto)`. 최소 크기는 100 픽셀이지만 최대 크기는 `auto`로써 콘텐츠에 들어맞게 확장된다. 최소최대값을 사용하려면 `grid-auto-rows`를 변경해보라

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: minmax(100px, auto);
    grid-gap: 20px;
}
```