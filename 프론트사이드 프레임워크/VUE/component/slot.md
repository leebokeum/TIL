### slot
```html
<div>
  <h2>나는 자식 컴포넌트의 제목입니다</h2>
  <slot>
    제공된 컨텐츠가 없는 경우에만 보실 수 있습니다.
  </slot>
</div>

그리고 그 컴포넌트를 사용하는 부모는

<div>
  <h1>나는 부모 컴포넌트의 제목입니다</h1>
  <my-component>
    <p>이것은 원본 컨텐츠 입니다.</p>
    <p>이것은 원본 중 추가 컨텐츠 입니다</p>
  </my-component>
</div>

아래처럼 렌더링 됩니다.

<div>
  <h1>나는 부모 컴포넌트의 제목입니다</h1>
  <div>
    <h2>나는 자식 컴포넌트의 제목 입니다</h2>
    <p>이것은 원본 컨텐츠 입니다.</p>
    <p>이것은 원본 중 추가 컨텐츠 입니다</p>
  </div>
</div>
```

#### 이름을 가지는 slot

```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

<app-layout>
  <h1 slot="header">여기에 페이지 제목이 위치합니다</h1>

  <p>메인 컨텐츠의 단락입니다.</p>
  <p>하나 더 있습니다.</p>

  <p slot="footer">여기에 연락처 정보입니다.</p>
</app-layout>
```

#### 범위를 가지는 slot
``` html
<div class="child">
  <slot text="hello from child"></slot>
</div>

<div class="parent">
  <child>
    <template slot-scope="props">
      <span>hello from parent</span>
      <span>{{ props.text }}</span>
    </template>
  </child>
</div>
```