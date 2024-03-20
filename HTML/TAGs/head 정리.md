---
tags: tag, head, css, style, title, meta, Favicon
---
```html
<!DOCTYPE HTML>
<head>
  어쩌구
</head>
<body>
  저쩌구
</body>
```

HTML 문서의 기본 템플릿은 꼭 head와 body 태그를 포함해야합니다.
head태그는 사이트 내에서 눈에는 보이지 않는 중요한 정보들이 들어갈 수 있는데
head태그 내에서 쓸 수 있는 중요한 태그들을 몇개 나열해보겠습니다.

## **1. 각종 CSS 파일들**
```
<head>
  <link href="css/main.css" rel="stylesheet">
</head>
```
CSS 파일들을 첨부할 때 링크태그를 집어넣을 수 있습니다.
위 경로는 현 HTML 파일과 같은 위치에 있는 css폴더 안에 있는 main.css 파일을 첨부하라고 되어있네요.

1. css/main.css
2. /css/main.css
참고로 위 두개의 경로는 다른 경로입니다.
- 1번은 현재 HTML파일과 같은 경로에 있는 css라는 폴더 내의 main.css 파일을 의미하고
- 2번은 현재 사이트의 메인경로 (codingapple.com)부터 시작해서 codingapple.com/css/main.css 파일을 첨부해라 라는 뜻입니다.

슬래쉬 기호가 첨부터 붙어있으면 사이트 메인경로부터 시작해라~ 라는 의미입니다.
멋진 말로 **1번은 상대경로**, **2번은 절대경로**라고 합니다.

## **2. 스타일 태그**
``` html
<head>
  <style>
    .button {
      color : red;
    }
  </style>
</head>
```

CSS 파일을 만들기 귀찮으면 `<style>` 태그를 열어서 CSS를 작성하기도 합니다.
CSS 파일과 유사하게 동작합니다.
`<body>` 안에 넣어도 동작하는데 html 파일안의 코드는 **위에 있을 수록 먼저 읽기 때문에**
`<body>`태그 맨 밑 같은 곳에 두면 사이트 로딩시 스타일이 잠깐 깨질 수 있습니다.
그래서 넣을거면 `<head>`에 넣는 사람이 많습니다.

## **3. 사이트 제목**
```html
<head>
  <title>네이버입니다</title>
</head>
```

사이트 제목을 넣을 수 있습니다. (브라우저 탭에 뜨는 이름입니다)

## **4. 여러가지 meta 태그**
```html
<head>
  <meta charset="UTF-8">
  <meta name="description" content="자바스크립트 인강 전문 코딩애플입니다.">
  <meta name="keywords" content="HTML,CSS,JavaScript,자바스크립트,코딩">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

1. 사이트의 인코딩 형식을 지정할 때 charset="UTF-8" 이라고 속성을 적을 수 있습니다.
2. 사이트의 검색 결과 화면에 뜨는 글귀를 수정하고 싶으면 이런 속성들을 추가할 수 있습니다. name="description" content="어쩌구"

description은 구글 검색시 파란 제목으로 뜨는 글귀,

keywords는 검색에 도움을 주는 키워드 등입니다.

(이런건 온라인 마케팅 하는 사람들이 잘 압니다)

3. 사이트 초기 zoom 레벨이나 폭을 지정해주려면 name="viewport" 라는 속성을 부여하시면 됩니다.

width=device-width는 모바일 기기의 실제 폭으로 렌더링 해주세요 라는 뜻입니다.

요즘 스마트폰 가로 해상도가 1920px을 넘어가는 폰들이 많죠.

그럼 이것만 보고 1920px 에 해당하는 페이지를 띄워줄 수는 없겠죠?

그래서 실제 접속시 스마트폰 기기의 실제 가로폭을 보고 렌더링하라고 명령하는 부분이라고 보시면 됩니다.

initial-scale=1 이 부분은 접속시의 화면 줌레벨 설정입니다.

그래서 반응형 웹을 만들 때 저 meta 태그를 복붙하시고 시작하시면 되겠습니다.

## **5. open graph**
```html
<head>
  <meta property="og:image" content="/이미지경로.jpg">
  <meta property="og:description" content="사이트설명">
  <meta property="og:title" content="사이트제목">
</head>
```

facebook이 만든 og 라는 메타태그가 있습니다.
여러분이 가끔 카톡 페북 이런 곳에 링크를 공유하면
![[open graph.png]]
▲ 이런 식으로 박스가 뜨고 사이트 설명, 제목, 이미지가 뜹니다.

이걸 커스터마이징하고 싶으면 저런 meta 태그를 따로 집어넣으면 됩니다.

## **6. Favicon**
```html
<head>
  <link rel="icon" href="아이콘경로.ico" type="image/x-icon">
</head>
```

여러분의 웹사이트 제목 옆에 뜨는 아이콘을 커스터마이징하려면
이렇게 link 태그로 첨부하면 됩니다.
![[Favicon.png]]
그럼 이렇게 아이콘이 생깁니다.

- ico 대신 png 파일로 넣어도 됩니다. ico가 호환성은 가장 좋습니다.
- 요즘은 32 x 32 사이즈로 제작하면 됩니다.
- 그리고 웹사이트를 바탕화면에 바로가기추가했을 경우 뜨는 아이콘도 커스터마이징 가능합니다.

rel="apple-touch-icon-precomposed"

이런 식으로 rel 속성을 조정하면 되는데 OS마다 요구하는 rel 속성이 달라서 필요해지면 찾아 적용하시거나

favicon generator 이런거 검색해서 한번 써보시면 OS별로 알아서 만들어줍니다.