### v-if 사용시 재사용 이슈...
- 이것은 항상 바람직하지는 않습니다. 때문에 “이 두 엘리먼트는 완전히 별개이므로 다시 사용하지 마십시오.”라고 알리는 방법을 제공합니다. 유일한 값으로 key 속성을 추가하십시오.
``` html
<template v-if="loginType === 'username'">
  <label>사용자 이름</label>
  <input placeholder="사용자 이름을 입력하세요" key="username-input">
</template>
<template v-else>
  <label>이메일</label>
  <input placeholder="이메일 주소를 입력하세요" key="email-input">
</template>
```
- <label> 엘리먼트는 key 속성이 없기 때문에 여전히 효율적으로 재사용 됩니다.