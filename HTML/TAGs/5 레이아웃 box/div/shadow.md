---
tags: html, div, flexbox, shadow
---
```css
/* offset-x | offset-y | color */
box-shadow: 60px -16px teal;

/* offset-x | offset-y | blur-radius | color */
box-shadow: 10px 5px 5px black;

/* offset-x | offset-y | blur-radius | spread-radius | color */
box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);

/* inset | offset-x | offset-y | color */
box-shadow: inset 5em 1em gold;

/* Any number of shadows, separated by commas */
box-shadow: 3px 3px red, -1em 0 0.4em olive;

/* Global keywords */
box-shadow: inherit;
box-shadow: initial;
box-shadow: unset;
```

- 두 개에서 네 개의 [`<length>`](https://developer.mozilla.org/ko/docs/Web/CSS/length) 값.
    
    - 두 개의 값을 사용하면 `<offset-x><offset-y>`로 분석합니다.
    - 세 번째 값이 주어지면 `<blur-radius>`로 분석합니다.
    - 네 번째 값이 주어지면 `<spread-radius>`로 분석합니다.
- 선택사항으로 `inset` 키워드.
    
- 선택사항으로 [`<color>`](https://developer.mozilla.org/ko/docs/Web/CSS/color_value) 값.
    
- `inset`
    
    - : 값을 지정하지 않으면(기본값) 요소가 공중에 떠있는 것처럼 밖에 드리우는 그림자가 됩니다. `inset` 키워드가 존재하면 요소가 움푹 들어간 것처럼 그림자가 요소의 테두리 안, 배경색 위, 내부 콘텐츠 밑에 그려집니다.
- `<offset-x>` `<offset-y>`두 값이 모두 `0`이면 그림자가 요소 바로 뒤쪽에 위치하며, `<blur-radius>` 또는 `<spread-radius>`가 존재하면 흐려지는 효과를 볼 수 있습니다.
    
    - : 그림자의 위치를 설정하는 두 개의 [`<length>`](https://developer.mozilla.org/ko/docs/Web/CSS/length) 값입니다. `<offset-x>`는 수평 거리를 의미하며 음수 값은 그림자를 요소의 왼쪽에 표시합니다. `<offset-y>`는 수직 거리를 의미하며 음수 값은 그림자를 요소의 위쪽에 표시합니다. 가능한 단위는 [`<length>`](https://developer.mozilla.org/ko/docs/Web/CSS/length)를 참고하세요.
- `<blur-radius>`…for a long, straight shadow edge, this should create a color transition the length of the blur distance that is perpendicular to and centered on the shadow’s edge, and that ranges from the full shadow color at the radius endpoint inside the shadow to fully transparent at the endpoint outside it.
    
    - : 세 번째 [`<length>`](https://developer.mozilla.org/ko/docs/Web/CSS/length) 값입니다. 크면 클 수록 그림자 테두리가 흐려지므로 크기는 더 커지고 색은 더 밝아집니다. 음수 값은 사용할 수 없습니다. 값을 설정하지 않으면 `0`이 되어 테두리가 선명해집니다. 명세는 흐림 효과의 지름을 어떻게 계산해야 하는지 정확한 알고리즘은 명시하지 않았지만 대신 다음과 같이 설명하고 있습니다.
- `<spread-radius>`
    
    - : 네 번째 [`<length>`](https://developer.mozilla.org/ko/docs/Web/CSS/length) 값입니다. 양수 값은 그림자가 더 커지고 확산하며, 음수 값은 그림자가 줄어듭니다. 기본값은 `0`(그림자와 요소 크기 동일)입니다.
- `<color>`
    
    - : 가능한 키워드와 표기법은 [`<color>`](https://developer.mozilla.org/ko/docs/Web/CSS/color_value)를 참고하세요. 기본값은 브라우저에 따라 다릅니다. 보통 [`color`](https://developer.mozilla.org/ko/docs/Web/CSS/color) 속성의 값을 사용하지만, Safari는 투명한 그림자가 기본값입니다.