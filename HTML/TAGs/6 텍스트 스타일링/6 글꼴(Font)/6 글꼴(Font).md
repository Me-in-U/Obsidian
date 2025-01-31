---
tags:
  - html
  - font
---
## [글꼴](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Fundamentals#%EA%B8%80%EA%BC%B4)

글꼴 스타일링의 속성을 살펴보도록 하겠습니다. 이 예에서는 동일한 HTML 샘플에 몇 가지 다른 CSS 속성을 적용합니다:

### [글꼴 종류](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Fundamentals#%EA%B8%80%EA%BC%B4_%EC%A2%85%EB%A5%98)

텍스트에 다른 글꼴을 설정하려면, [`font-family`](https://developer.mozilla.org/ko/docs/Web/CSS/font-family) 속성을 사용하여 브라우저에서 선택한 요소에 적용할 글꼴 (또는 글꼴 목록) 을 지정할 수 있습니다. 브라우저는 웹 사이트에 액세스하는 컴퓨터에서 글꼴을 사용할 수 있는 경우에만 글꼴을 적용합니다; 그렇지 않으면, 브라우저 [default font](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Fundamentals#default_fonts) 만 사용합니다. 간단한 예는 다음과 같습니다:

```css
p {
  font-family: arial;
}
```

이렇게하면 페이지의 모든 단락이 임의의 컴퓨터에 있는 arial 글꼴을 채택하게 됩니다.

## 기본글꼴

serif	serifs 가 있는 글꼴 (the flourishes and other small details you see at the ends of the strokes in some typefaces)	My big red elephant
sans-serif	serifs 가 없는 글꼴.	My big red elephant
monospace	모든 문자의 너비가 같은 글꼴로, 일반적으로 코드 목록에 사용됩니다.	My big red elephant
cursive	Fonts that are intended to emulate handwriting, with flowing, connected strokes.	My big red elephant
fantasy	장식용 글꼴.	My big red elephant

## 웹 안전 글꼴

Arial	sans-serif	It's often considered best practice to also add Helvetica as a preferred alternative to Arial as, although their font faces are almost identical, Helvetica is considered to have a nicer shape, even if Arial is more broadly available.
Courier New	monospace	Some OSes have an alternative (possibly older) version of the Courier New font called Courier. It's considered best practice to use both with Courier New as the preferred alternative.
Georgia	serif	
Times New Roman	serif	Some OSes have an alternative (possibly older) version of the Times New Roman font called Times. It's considered best practice to use both with Times New Roman as the preferred alternative.
Trebuchet MS	sans-serif	You should be careful with using this font — it isn't widely available on mobile OSes.
Verdana	sans-serif	

## **Font stacks**

웹 페이지에서 글꼴의 사용가능 여부를 보장할 수 없으므로 (어똔 이유로 웹 글꼴이 실패할 수 있음) 브라우저에서 선택할 수 있는 **글꼴 스택 (font stack)**  을 제공할 수 있습니다. 여기에는 여러 글꼴 이름으로 구성된 `font-family`  값이 포함됩니다. 예제:

```css
p {
  font-family: "Trebuchet MS", Verdana, sans-serif;
}
```

이 경우, 브라우저는 목록 시작 부분에서 시작하여 해당 글꼴이 시스템에서 사용 가능한지 확인합니다. 이 글꼴이 있으면, 해당 글꼴이 선택한 요소에 적용됩니다. 그렇지 않으면, 다음 글꼴로 이동합니다.

나열된 글꼴 중 사용 가능한 글꼴이 없는 경우, 브라우저가 최소한 대략 비슷한 것을 제공할 수 있도록 스택 끝에 적절한 일반 글꼴 이름을 제공하는 것이 좋습니다.이 점을 강조하기 위해 다른 옵션 — 일반적으로 Time New Roman — 을 사용할 수 없는 경우 단락에 기본 serif 글꼴이 제공됩니다. 이는 san-serif 글꼴에 적합하지 않습니다!

