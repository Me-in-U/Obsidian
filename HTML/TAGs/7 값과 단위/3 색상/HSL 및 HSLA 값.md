RGB 보다 약간 덜 지원되는 HSL 색상은 (이전 버전의 IE 에서는 지원되지 않음) 디자이너의 관심을 끈 후에 구현되었습니다. `hsl()`  함수는 빨강, 녹색 및 파랑 값 대신 색조 (hue), 채도 (saturation) 및 명도(lightness) 값을 받아들입니다. 이 값은 1670만 가지 색상을 구별하는 데 사용되지만 다른 방식으로 사용됩니다.

- **색조 (Hue)**: 색상의 기본 음영입니다. 0 에서 360 사이의 값을 사용합니다.
- **채도 (Saturation)**: 색상이 얼마나 포함되어 있습니까? 0–100% 사이의 값을 취합니다. 여기서 0은 색상이 없고 (회색 음영으로 표시됨), 100% 는 전체 색상 채도입니다.
- **명도 (Lightness)**: 색상이 얼마나 밝습니까? 0–100% 의 값을 받습니다. 여기서 0은 빛이 없고 (완전히 검은색으로 표시됨), 100% 는 완전한 빛 (완전히 흰색으로 표시됨) 입니다.

다음과 같이 HSL 색상을 사용하도록 RGB 예제를 업데이트 할 수 있습니다:

```css
.one {
  background-color: hsl(188, 97%, 28%);
}

.two {
  background-color: hsl(321, 47%, 57%);
}

.three {
  background-color: hsl(174, 77%, 31%);
}
```

```html
<div class="wrapper">
  <div class="box one">hsl(188, 97%, 28%)</div>
  <div class="box two">hsl(321, 47%, 57%)</div>
  <div class="box three">hsl(174, 77%, 31%)</div>
</div>
```


RGB 에 RGBA 가 있는 것처럼, HSL 에는 HSLA 에 상응하는 것이 있으므로, 알파 채널을 지정할 수 있는 동일한 기능을 제공합니다. HSLA 색상을 사용하도록 RGBA 예제를 변경하여 아래에서 이것을 시연했습니다.

```css
.one {
  background-color: hsla(188, 97%, 28%, .3);
}

.two {
  background-color: hsla(321, 47%, 57%, .7);
}

.three {
  background-color: hsla(174, 77%, 31%, .9);

```

```html
<div class="wrapper">
  <div class="box one">hsla(188, 97%, 28%, .3)</div>
  <div class="box two">hsla(321, 47%, 57%, .7)</div>
  <div class="box three">hsla(174, 77%, 31%, .9)</div>
</div>
```

