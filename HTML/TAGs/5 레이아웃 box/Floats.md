- 우선순위

## z-index
```css
.css {
	z-index: 5;
}
```

띄운 개체 높으면 더 앞으로
## [floats의 배경](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Floats#floats%EC%9D%98_%EB%B0%B0%EA%B2%BD)

float 속성은 웹 개발자가 텍스트 열 내부에 float하는 이미지를 포함하고, 아울러 해당 이미지의 좌측 우측 주변으로 텍스트를 둘러싸는 간단한 레이아웃을 구현할 수 있도록 도입되었습니다. 이런 것은 신문 레이아웃에서 볼 수 있는 종류입니다.

그러나 웹 개발자들은 이미지뿐만 아니라 무엇이든 float할 수 있음을 빠르게 깨달았고, 그래서 floats 사용이 확대되었습니다. 앞서 살펴본 [고급 단락 예제](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements#active_learning_a_fancy_paragraph)는 재미있는 드롭캡 효과를 생성하는 데 floats를 어떻게 사용할 수 있는지를 보여줍니다.

floats는 일반적으로 상대 요소와 나란히 놓이도록 float(浮動)하는 다단 정보를 갖춘 웹 사이트의 전체 레이아웃을 만들는데 널리 사용되어 왔다(기본 행동은 다단 무리가 소스에서 보이는 순서와 같은 순서대로 상대 요소 아래에 자리잡기하는 것이다). 더 새롭고 더 나은 레이아웃 기술이 나와있으므로 이러한 방식으로 floats를 사용하는 것은 [낡은 기술](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Legacy_Layout_Methods)로 간주되어야 합니다.

```css
.box {
  float: left;

  margin-right: 15px;
  width: 150px;
  height: 100px;
  border-radius: 5px;
  background-color: rgb(207,232,220);
  padding: 1em;
}
```
![[Pasted image 20250116104602.png]]