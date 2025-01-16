**배경관련 CSS 속성들**

```css
.main-background {
  background-image : url(../img/shoes.jpg);
  background-size : cover;
  background-repeat : no-repeat;
  background-position : center;
  background-attachment : fixed;
}
```

background-size는 px, % 단위도 가능하고

cover는 배경으로 꽉채워주세요

contain은 배경이 짤리지 않게 꽉채워주세요 라는 뜻입니다.

background-attachment는 웹사이트가 스크롤될 때 배경이 신기하게 동작하게 만들고 싶으면 써보도록 합시다.

**배경 두개 겹치기 신공**

```css
.main-background {
  background-image : url(../img/shoes.jpg), url(person.jpg);
}
```

콤마로 이미지 두개를 첨부하시면 됩니다.

투명도를 지원하는 png 이미지를 사용하면 더 재밌는 디자인을 만들 수 있겠군요

**배경에 검은색 틴트 주기**

```
.main-background {
  background-image: linear-gradient( rgba(0,0,0,0.5), rgba(0,0,0,0.5) ), url(이미지경로~~) ;

}
```

linear-gradient 이건 색이 점진적으로 변하는 gradient를 줄 수 있는 키워드인데

여기에 투명도 0.5의 검은색을 입힌 후에 배경겹치기 스킬을 사용하면 됩니다.

**주의해야할 margin 버그**

```
<div class="배경">
  <p>안에 글씨</p>
</div>
```

div 박스 안에 p 태그를 사용했습니다.

p 태그에 상단 margin을 주기 위해 margin-top을 주게 되면

div와 p가 동시에 margin-top이 생기게 됩니다. 뭔가 이상합니다.

이 현상은 margin collapse effect 라고 부르는 일종의 버그입니다.

원래 박스들의 테두리가 만나면 margin이 합쳐집니다. (박스가 내부에서 만나든 외부에서 만나든 상관없습니다.)

정확히 말하면

1. 마진을 하나로 합쳐주고
    
2. 혹여나 둘 다 마진이 있으면 둘 중에 더 큰 마진을 하나만 적용하게 됩니다.
    

그래서 두 박스의 테두리가 **겹치지 않도록** 해주시면 보다 더 정확한 마진 노가다를 하실 수 있습니다.

강의 예제에선 부모 박스에 padding을 1px 이렇게 조금 주는 것으로 쉽게 해결 가능합니다.