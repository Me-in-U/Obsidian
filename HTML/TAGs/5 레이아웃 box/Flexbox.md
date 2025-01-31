---
tags: html, layout, flexbox
---
- 부모 요소 내부에 포함된 블록 콘텐츠를 세로로 중심부에 맞추기.
- 사용 가능한 너비와 높이에 관계없이 하나의 컨테이너에 포함된 모든 자녀 요소가 주어진 너비와 높이를 똑같은 크기로 점유하기.
- 다단 레이아웃에 포함된 모든 단이 서로 다른 크기의 콘텐츠를 포함하고 있더라도 동일한 높이로 채택하기.

## [flex 모델의 측방](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Flexbox#flex_%EB%AA%A8%EB%8D%B8%EC%9D%98_%EC%B8%A1%EB%B0%A9)

요소들을 flexbox로 레이아웃될 때 그 상자들은 두 개의 축을 따라 배치됩니다.

![[Pasted image 20250116104209.png]]

- **`기본 축`** (`main axis`) 은 flex item이 배치되고 있는 방향으로 진행하는 축입니다(예: 페이지를 가로지르는 행 또는 페이지 밑으로 쌓이는 열). 이 기본 축의 시작과 끝을 일컬어 **main start**과 **main end**라고 합니다.
    
- **`교차축`** (`cross axis`) 은 flex item이 내부에 배치되는 방향에 직각을 이루는 축입니다. 이 축의 시작과 끝을 일컬어 **cross start**과 **cross end**라고 합니다.
    
- `display: flex`이 설정된 부모 요소(우리 예제에서 [`<section>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/section)이 해당)를 일컬어 **`flex container`** (`flex container`) 라고 합니다.
    
- flex container 내부에 flexbox로 레이아웃되는 항목을 일컬어 **`flex item`** (`flex items`) 이라고 합니다(우리 예제에서 [`<article>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/article) 요소가 해당됩니다).
    
- **Flexbox 레이아웃 사용법**
    

```html
<div class="flex-container">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

```css
.flex-container {
  display : flex;
}
.box {
  width : 100px;
  height : 100px;
  background : grey;
  margin : 5px;
}
```

그냥 박스들을 감싸는 부모 요소에게 display : flex를 사용하면 됩니다.

그럼 박스들이 기본적으로 가로정렬로 배치됩니다.

(참고) 인터넷 익스플로러 11 이상에서 사용가능한 속성입니다.

11미만에선 flex 그런거 없다고 에러납니다.

- **Flexbox 세부속성 사용하기**

```css
.flex-container {
  display : flex;
  justify-content : center; /* 좌우정렬 */
	align-items : center; /* 상하정렬 */
	flex-direction : column; /* 세로정렬 */
	flex-wrap : wrap; /* 폭이 넘치는 요소 wrap 처리 */
}
.box {
  flex-grow : 2; /* 폭이 상대적으로 몇배인지 결정 */
}
```

역시 외워봤자 다음날 까먹기 때문에

필요할 때마다 찾아쓰는게 일반적입니다.

- **박스 좌측 & 우측정렬 동시에 하는 법**

```html
<div class="flex-container">
  <div class="box"></div>
  <div class="box" style="flex-grow : 1"></div>
  <div class="box"></div>
</div>
```

그러니까 첫 <div>는 왼쪽,

마지막 <div>는 우측정렬을 하고싶으면 어떻게 하냐는 겁니다.

그건 가운데 임시 <div> 하나 만들어주고

flex-grow: 1 이런 식으로 사이즈를 크게 키워주면 됩니다.

그럼 알아서 나머지 요소들은 좌측 우측으로 퍼집니다.

- **align-content**

참고로 display : flex; 이걸 준 요소에 align-content 속성을 줄 수 있는데

이러면 내부에 들어있는 박스들의 상하정렬이 어떻게 될지 조절할 수 있습니다.

align-content는 박스가 **가로로 여러줄일 때** 박스들의 상하배치를 조절할 수 있는 속성입니다.

![[Pasted image 20250116104306.png]]
