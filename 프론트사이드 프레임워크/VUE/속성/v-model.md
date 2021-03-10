### v-model
- `v-model`은 모든 form 엘리먼트의 초기 `value`와 `checked` 그리고 `selected` 속성을 무시합니다. 항상 Vue 인스턴스 데이터를 원본 소스로 취급합니다. 컴포넌트의 `data` 옵션 안에 있는 JavaScript에서 초기값을 선언해야합니다.
- text 와 textarea 태그는 value속성과 input이벤트를 사용합니다.
- 체크박스들과 라디오버튼들은 checked 속성과 change 이벤트를 사용합니다.
- Select 태그는 value를 prop으로, change를 이벤트로 사용합니다.

#### 체크박스, 라디오, 셀렉트

``` html
<input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no"
>

// 체크된 경우
vm.toggle === 'yes'
// 체크 되지 않은 경우
vm.toggle === 'no'

<input type="radio" v-model="pick" v-bind:value="a">
// 체크 하면:
vm.pick === vm.a

<select v-model="selected">
  <!-- inline object literal -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>

// 선택 하면:
typeof vm.selected // -> 'object'
vm.selected.number // -> 123
```

#### .lazy
- 기본적으로, v-model은 각 입력 이벤트 후 입력과 데이터를 동기화 합니다. (단 앞에서 설명한 IME 구성은 제외됩니다.) .lazy 수식어를 추가하여 change 이벤트 이후에 동기화 할 수 있습니다.

#### v-model.number, v-model.trim