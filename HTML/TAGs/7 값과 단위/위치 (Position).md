[`<position>`](https://developer.mozilla.org/en-US/docs/Web/CSS/position_value) 데이터 형식은 배경 이미지 ([`background-position`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position) 를 통해) 와 같은 항목을 배치하는 데 사용되는 2D 좌표를 나타냅니다. `top`, `left`, `bottom`, `right` 및 `center` 와 같은 키워드를 사용하여 항목을 2D 박스의 특정 범위에 맞춰 길이와 함께 박스의 위쪽 및 왼쪽 가장자리에서 offset 을 나타냅니다.

일반적인 position 값은 두 가지 값으로 구성됩니다 — 첫 번째는 위치를 가로로 설정하고, 두 번째는 세로로 설정합니다. 한 축의 값만 지정하면 다른 축은 `center` 으로 설정됩니다.

다음 예제에서는 키워드를 사용하여 container 의 위쪽과 오른쪽에서 40px 의 배경 이미지를 배치했습니다.

```css
.box {
  height: 300px;
  width: 400px;
  background-image: url(star.png);
  background-repeat: no-repeat;
  background-position: right 40px;
}
```

```html
<div class="box"></div>
```
