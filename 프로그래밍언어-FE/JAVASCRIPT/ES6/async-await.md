### async & await
- Promise가 기존 콜백지옥에서 코드를 조금은 동기적으로 개선했 지만 코드의 실행순서나 복잡함에 있어서는 손볼 곳이 있었습니다.
그래서 이를 간편하게 만드는 "Async Await"가 도입됐습니다.

### async & await 기본문법
~~~ javascript
async function 함수명() {
  await 비동기_처리_메서드_명();
}
~~~
- 먼저 함수의 앞에 async 라는 예약어를 붙입니다. 그러고 나서 함수의 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 await를 붙입니다. 여기서 주의하셔야 할 점은 비동기 처리 메서드가 꼭 프로미스 객체를 반환해야 await가 의도한 대로 동작합니다.

### async & await 간단한 예제
~~~ javascript
function fetchItems() {
  return new Promise(function(resolve, reject) {
    var items = [1,2,3];
    resolve(items)
  });
}

async function logItems() {
  var resultItems = await fetchItems();
  console.log(resultItems); // [1,2,3]
}
~~~
- 먼저 fetchItems() 함수는 프로미스 객체를 반환하는 함수입니다. 프로미스는 “자바스크립트 비동기 처리를 위한 객체“라고 배웠었죠. fetchItems() 함수를 실행하면 프로미스가 이행(Resolved)되며 결과 값은 items 배열이 됩니다.


### async & await 실용 예제
- async & await 문법이 가장 빛을 발하는 순간은 여러 개의 비동기 처리 코드를 다룰 때
~~~ javascript
function fetchUser() {
  var url = 'https://jsonplaceholder.typicode.com/users/1'
  return fetch(url).then(function(response) {
    return response.json();
  });
}

function fetchTodo() {
  var url = 'https://jsonplaceholder.typicode.com/todos/1';
  return fetch(url).then(function(response) {
    return response.json();
  });
}

1. fetchUser()를 이용하여 사용자 정보 호출
2. 받아온 사용자 아이디가 1이면 할 일 정보 호출
3. 받아온 할 일 정보의 제목을 콘솔에 출력

async function logTodoTitle() {
  var user = await fetchUser();
  if (user.id === 1) {
    var todo = await fetchTodo();
    console.log(todo.title); // delectus aut autem
  }
}
~~~
- logTodoTitle()를 실행하면 콘솔에 delectus aut autem가 출력될 것입니다. 위 비동기 처리 코드를 만약 콜백이나 프로미스로 했다면 훨씬 더 코드가 길어졌을 것이고 인덴팅 뿐만 아니라 가독성도 좋지 않았을 겁니다. 이처럼 async await 문법을 이용하면 기존의 비동기 처리 코드 방식으로 사고하지 않아도 되는 장점이 생깁니다.

### 참조
https://joshua1988.github.io/web-development/javascript/js-async-await/#async--await%EB%8A%94-%EB%AD%94%EA%B0%80%EC%9A%94