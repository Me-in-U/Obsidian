**좌표속성이 있습니다.**

```css
.box {
  top : 20px;
  left : 30%;
}
```

top, left, bottom, right 라는 속성을 사용하면

요소의 상하좌우 위치를 변경할 수 있습니다.

하지만 이 좌표속성을 사용하려면 position 속성이 필요합니다.

position 속성은 좌표속성을 적용할 **기준점**이 여기에요~! 라고 지정해주는 역할입니다.

**position 속성은 크게 4개 값이 있습니다.**

```css
.box {
  position : static;/* 기준이 엄서요 (좌표적용 불가) */
	position : relative;/* 기준이 내 원래 위치요 */
	position : absolute;/* 기준이 내 부모요 */
	position : fixed;/* 기준이 브라우저 창이요 (viewport) */
}
```

여기서 원하는 기준을 선택하시면 됩니다. 그럼 이제 좌표속성으로 좌표 값을 줄 수 있습니다.

position : absolute는 부모 박스를 기준으로 찰싹 달라붙은 뒤에 좌표값을 적용하게 되는데,

정확히 말하면 부모가 아니라 부모 중에 **position : relative를 가지고 있는 부모가 기준**입니다.

**position : absolute 를 적용한 요소 가운데 정렬**

```css
.button {
  position : absolute;
  left : 0;
  right : 0;
  margin-left : auto;
  margin-right : auto;
  width : 적절히
}
```

적어도 5개의 속성이 있어야 가운데 정렬이 가능합니다.

5개라니 약간 귀찮아집니다.