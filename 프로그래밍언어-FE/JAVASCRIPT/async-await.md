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
