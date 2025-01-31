---
tags:
  - html
  - div
  - boxed
  - position
---
**겹치는 박스 만들기**

**당연히 position 속성을 사용하면 되겠죠?**

**absolute, relative, fixed 중 하나를 사용하면 됩니다.**

## [](https://www.notion.so/position-1ba47f038c4c44f883d0853e5be63da4?pvs=21)[https://www.notion.so/position-1ba47f038c4c44f883d0853e5be63da4](https://www.notion.so/position-1ba47f038c4c44f883d0853e5be63da4)

하지만 박스를 만들 때 주의점이 하나 있습니다.

원래 div 박스의 width를 주게되면 padding, border를 고려하지 않습니다.

padding 안쪽 부분만 실제 width로 설정합니다.

![https://codingapple.com/wp-content/uploads/2019/06/캡처333.jpg](https://codingapple.com/wp-content/uploads/2019/06/%EC%BA%A1%EC%B2%98333.jpg)

이걸 그림을 그려보면... 파란색 저 부분만 실제 width라는겁니다.

그래서 200px의 박스를 만들어도, padding을 많이 주게 되면 실제 보여지는 박스의 폭이 padding 만큼 늘어날 수 있습니다.

웹사이트 대충 만드는 초보는 별 상관 없겠지만

실제 업무에서는 사이즈 조금만 잘못되어도 다른 요소에 크게 영향을 줄 수 있습니다.

**박스의 폭을 border까지 설정해주고 싶을 때 쓰는 속성**

```css
.box {
  box-sizing : border-box;/*박스의 폭은 border까지 포함입니다*/
	box-sizing : content-box;/*박스의 폭은 padding 안쪽입니다*/
}
```

box-sizing이라는 속성을 주게되면 border까지를 실제 박스의 폭으로 설정해줍니다.

아주 고마운 속성입니다.

빨리 모든 div 박스에 추가해보도록 합시다.