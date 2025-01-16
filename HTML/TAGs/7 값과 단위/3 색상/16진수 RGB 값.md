다음 형식의 색상 값은 16진수 코드입니다. 각 16진수 값은 hash/pound 기호 (#) 와 6개의 16진수로 구성되며, 각 16진수는 0 과 f (15를 나타냄) 사이의 16개 값 중 하나를 사용할 수 있으므로 — `0123456789abcdef` 입니다. 각 값 쌍은 채널 중 하나 — 빨강, 녹색 및 파랑 — 을 나타내며 각각에 대해 256개의 사용 가능한 값 (16 x 16 = 256) 을 지정할 수 있습니다.

이 값은 좀 더 복잡하고 이해하기 쉽지 않지만 기워드보다 훨씬 더 다양합니다 — 16진수 값을 사용하여 색상표에 사용하려는 색상을 나타낼 수 있습니다.

```css
.one {
  background-color: #02798b;
}

.two {
  background-color: #c55da1;
}

.three {
  background-color: #128a7d;
}
```

```html
<div class="wrapper">
  <div class="box one">#02798b</div>
  <div class="box two">#c55da1</div>
  <div class="box three">#128a7d</div>
</div>
```
