---
tags: html, list
---
[목록](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/HTML_text_fundamentals#lists)  은 대부분 다른 텍스트처럼 작동하지만, 알아야 할 목록과 관련된 몇 가지 CSS 속성과 고려해야 할 모범 사례가 있습니다. 이 기사는 모든 것을 설명합니다.

If you go to the live example now and investigate the list elements using [browser developer tools (en-US)](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools), you'll notice a couple of styling defaults:

- The [`<ul>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/ul) and [`<ol>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/ol) elements have a top and bottom [`margin`](https://developer.mozilla.org/ko/docs/Web/CSS/margin) of `16px` (`1em`) and a [`padding-left`](https://developer.mozilla.org/ko/docs/Web/CSS/padding-left) of `40px` (`2.5em`.)
- The list items ([`<li>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/li) elements) have no set defaults for spacing.
- The [`<dl>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/dl) element has a top and bottom [`margin`](https://developer.mozilla.org/ko/docs/Web/CSS/margin) of `16px` (`1em`), but no padding set.
- The [`<dd>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/dd) elements have [`margin-left`](https://developer.mozilla.org/ko/docs/Web/CSS/margin-left) of `40px` (`2.5em`.)
- The [`<p>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/p) elements we've included for reference have a top and bottom [`margin`](https://developer.mozilla.org/ko/docs/Web/CSS/margin) of `16px` (`1em`), the same as the different list types.

## [Handling list spacing](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Styling_lists#handling_list_spacing)

When styling lists, you need to adjust their styles so they keep the same vertical spacing as their surrounding elements (such as paragraphs and images; sometimes called vertical rhythm), and the same horizontal spacing as each other (you can see the [finished styled example](https://mdn.github.io/learning-area/css/styling-text/styling-lists/) on Github, and [find the source code](https://github.com/mdn/learning-area/blob/master/css/styling-text/styling-lists/index.html) too.)

The CSS used for the text styling and spacing is as follows:

```css
/* General styles */

html {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 10px;
}

h2 {
  font-size: 2rem;
}

ul,ol,dl,p {
  font-size: 1.5rem;
}

li, p {
  line-height: 1.5;
}

/* Description list styles */

dd, dt {
  line-height: 1.5;
}

dt {
  font-weight: bold;
}

dd {
  margin-bottom: 1.5rem;
}
```

- The first rule sets a sitewide font and a baseline font size of 10px. These are inherited by everything on the page.
- Rules 2 and 3 set relative font sizes for the headings, different list types (the children of the list elements inherit these), and paragraphs. This means that each paragraph and list will have the same font size and top and bottom spacing, helping to keep the vertical rhythm consistent.
- Rule 4 sets the same [`line-height` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height) on the paragraphs and list items — so the paragraphs and each individual list item will have the same spacing between lines. This will also help to keep the vertical rhythm consistent.
- Rules 5 and 6 apply to the description list — we set the same `line-height` on the description list terms and descriptions as we did with the paragraphs and list items. Again, consistency is good! We also make the description terms have bold font, so they visually stand out easier.

## [List-specific styles](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Styling_lists#list-specific_styles)

Now we've looked at general spacing techniques for lists, let's explore some list-specific properties. There are three properties you should know about to start with, which can be set on [`<ul>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/ul) or [`<ol>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/ol) elements:

- [`list-style-type` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-type): Sets the type of bullets to use for the list, for example, square or circle bullets for an unordered list, or numbers, letters or roman numerals for an ordered list.
- [`list-style-position` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-position): Sets whether the bullets appear inside the list items, or outside them before the start of each item.
- [`list-style-image` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-image): Allows you to use a custom image for the bullet, rather than a simple square or circle.

[[Bullet styles](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Styling_lists#bullet_styles)]([https://www.notion.so/Bullet-styles-92238e02252844ea8f663683e278c3ca?pvs=21](https://www.notion.so/Bullet-styles-92238e02252844ea8f663683e278c3ca?pvs=21))

[[list-style shorthand](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Styling_lists#list-style_shorthand)]([https://www.notion.so/list-style-shorthand-a30b145b6d314927bff1f51788b2a2db?pvs=21](https://www.notion.so/list-style-shorthand-a30b145b6d314927bff1f51788b2a2db?pvs=21))

[[**list counting**](https://developer.mozilla.org/ko/docs/Learn/CSS/Styling_text/Styling_lists#controlling_list_counting)]([https://www.notion.so/list-counting-ffe8135d2f8a4bea8c628a7093a2de65?pvs=21](https://www.notion.so/list-counting-ffe8135d2f8a4bea8c628a7093a2de65?pvs=21))

[링크에 아이콘 넣기](https://www.notion.so/7c45c9d3fa874bfd925df4bebfd9f5ab?pvs=21)