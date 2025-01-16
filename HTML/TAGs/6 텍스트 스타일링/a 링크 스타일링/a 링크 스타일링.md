---
aliases:
  - <a> 링크 스타일링
---
### [Styling some links](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Styling_links#styling_some_links)

Now that we've looked at the default states in some detail, let's look at a typical set of link styles.

To start off with, we'll write out our empty rulesets:

```css
a {
}

a:link {
}

a:visited {
}

a:focus {
}

a:hover {
}

a:active {
}
```

```css
body {
  width: 300px;
  margin: 0 auto;
  font-size: 1.2rem;
  font-family: sans-serif;
}

p {
  line-height: 1.4;
}

a {
  outline: none;
  text-decoration: none;
  padding: 2px 1px 0;
}

a:link {
  color: #265301;
}

a:visited {
  color: #437A16;
}

a:focus {
  border-bottom: 1px solid;
  background: #BAE498;
}

a:hover {
  border-bottom: 1px solid;
  background: #CDFEAA;
}

a:active {
  background: #265301;
  color: #CDFEAA;
}
```

```html
<p>There are several browsers available, such as <a href="#">Mozilla
Firefox</a>, <a href="#">Google Chrome</a>, and
<a href="#">Microsoft Edge</a>.</p>
```

