```html
<nav class="container">
  <a href="#">Home</a>
  <a href="#">Pizza</a>
  <a href="#">Music</a>
  <a href="#">Wombats</a>
  <a href="#">Finland</a>
</nav>
```

```css
body,html {
  margin: 0;
  font-family: sans-serif;
}

.container {
  display: flex;
  gap: 0.625%;
}

a {
  flex: 1;
  text-decoration: none;
  outline: none;
  text-align: center;
  line-height: 3;
  color: black;
}

a:link, a:visited, a:focus {
  background: yellow;
}

a:hover {
  background: orange;
}

a:active {
  background: red;
  color: white;
}
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/329f2a25-8017-4ed7-a418-cc5bcbf5f412/Untitled.png)

The HTML defines a [`<nav>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav) element with a `"container"` class.

The `<nav>` contains our links.