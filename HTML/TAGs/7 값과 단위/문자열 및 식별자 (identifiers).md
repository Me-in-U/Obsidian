위의 예에서, 키워드가 값으로 (예: `red`, `black`, `rebeccapurple` 및 `goldenrod`, 와 같은 `<color>` 키워드) 사용되는 위치를 확인했습니다. 이러한 키워드는 CSS 가 이해하는 특수한 값인 **_식별자 (identifiers)_ **로, 보다 정확하게 설명됩니다. 따라서 인용되지 않으며 — 문자열로 취급되지 않습니다.

CSS 에서 문자열을 사용하는 장소가 있습니다. 예를 들면, [생성된 콘텐츠를 지정할 때 (en-US)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements). 이 경우 값은 문자열임을 보여주기 위해 인용됩니다. 아래 예제에서는 인용되지 않은 색상 키워드와 인용된 생성된 콘텐츠 문자열을 사용합니다.

```css
.box {
  width:400px;
  padding: 1em;
  border-radius: .5em;
  border: 5px solid rebeccapurple;
  background-color: lightblue;
}

.box::after {
  content: "This is a string. I know because it is quoted in the CSS."
}
```

```html
<div class="box"></div>
```

