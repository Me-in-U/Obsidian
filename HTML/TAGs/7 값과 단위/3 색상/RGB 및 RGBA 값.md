### [RGB](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Values_and_units#rgb_%EB%B0%8F_rgba_%EA%B0%92)

여기서 이야기 할 세 번째 방식은 RGB 입니다. RGB 값은 — `rgb()` 함수입니다 — 이 값은 16진수 값과 거의 같은 방식으로 색상의 빨강, 녹색 및 파랑 채널 값을 나타내는 세 개의 매개 변수가 제공됩니다. RGB 와의 차이점은 각 채널이 2개의 16진수가 아니라 0 과 255 사이의 10진수로 표현되어 — 다소 이해하기 쉽다는 것입니다.

```css
.one {
  background-color: rgb(2, 121, 139);
}

.two {
  background-color: rgb(197, 93, 161);
}

.three {
  background-color: rgb(18, 138, 125);
}
```

```html
<div class="wrapper">
  <div class="box one">rgb(2, 121, 139)</div>
  <div class="box two">rgb(197, 93, 161)</div>
  <div class="box three">rgb(18, 138, 125)</div>
</div>
```

### [RGBA 값](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Values_and_units#rgb_%EB%B0%8F_rgba_%EA%B0%92)

RGBA 색상을 사용할 수도 있습니다 — 이 색상은 RGB 색상과 정확히 같은 방식으로 작동하므로 RGB 값을 사용할 수 있지만, 색상의 알파 채널을 나타내는 네 번째 값이 있어 불투명도 (opacity) 를 제어합니다. 이 값을 `0`  으로 설정하면 색상이 완전히 투명해지는 반면, `1`  이면 완전히 불투명하게 됩니다. 그 사이의 값은 다른 수준의 투명성을 제공합니다.

```css
.one {
  background-color: rgba(2, 121, 139, .3);
}

.two {
  background-color: rgba(197, 93, 161, .7);
}

.three {
  background-color: rgba(18, 138, 125, .9);
}
```

```html
<div class="wrapper">
  <div class="box one">rgba(2, 121, 139, .3)</div>
  <div class="box two">rgba(197, 93, 161, .7)</div>
  <div class="box three">rgba(18, 138, 125, .9)</div>
</div>
```
