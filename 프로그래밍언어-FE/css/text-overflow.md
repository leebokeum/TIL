### text-overflow
- 긴 글을 한 줄로 나타내고 영역이 벗어나는 경우 생략기호로 바꾸는 방법

#### 조건
- width 또는 height가 고정적일 것
- overflow: hidden; 을 사용해 영역을 감출 것
- 아래줄로 내려가는 것을 막기위해 white-space: nowrap 등이 필요

```css
text-overflow: ellipsis;

<div>
  <p>이렇게 긴 경우 생략기호가 필요해...</p>
</div>
```