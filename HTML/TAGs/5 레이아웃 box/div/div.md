---
tags:
  - html
  - div
  - layout
---
```css
.box {
	width : 150px;
	height : 150px;

  margin : 20px; 
  padding : 30px;
  border : 1px solid black;
  border-radius : 5px;
	background-color: white;

	display : block
	margin-left : auto
	margin-right : auto
}
```

margin은 바깥 여백

padding은 안쪽 여백

border는 테두리 (차례로 두께, 선의 종류, 색상)

border-radius는 테두리 둥글게

display : block

margin-left : auto

margin-right : auto



```css
.container{
	width: min(100% - 15px, 850px);
	margin-inline: auto;
}
```