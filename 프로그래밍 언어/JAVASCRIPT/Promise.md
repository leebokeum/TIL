### Promise 
- 프로미스는 자바스크립트 비동기 처리에 사용되는 객체입니다. 여기서 자바스크립트의 비동기 처리란 ‘특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성’을 의미합니다.

### 프로미스 코드 - 기초
~~~ javascript
만약 콜백함수를 사용하지 않는다면
function getData() {
	var tableData;
	$.get('https://domain.com/products/1', function(response) {
		tableData = response;
	});
	return tableData;
}

console.log(getData()); // undefined

콜백함수를 사용하면
function getData(callbackFunc) {
  $.get('url 주소/products/1', function (response) {
    callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
  });
}

getData(function (tableData) {
  console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});


~~~
- 위와 같이 과거에는 비동기 처리를 위해 프로미스 대신에 콜백 함수를 이용했다.

#### 콜백 지옥 (Callback hell)
~~~ javascript
$.get('url', function(response) {
	parseValue(response, function(id) {
		auth(id, function(result) {
			display(result, function(text) {
				console.log(text);
			});
		});
	});
});
~~~
- 웹 서비스를 개발하다 보면 서버에서 데이터를 받아와 화면에 표시하기까지 인코딩, 사용자 인증 등을 처리해야 하는 경우가 있습니다. 만약 이 모든 과정을 비동기로 처리해야 한다고 하면 위와 같이 콜백 안에 콜백을 계속 무는 형식으로 코딩을 하게 됩니다. 이러한 코드 구조는 가독성도 떨어지고 로직을 변경하기도 어렵습니다. 이와 같은 코드 구조를 콜백 지옥이라고 합니다.

#### 콜백 지옥 promise로 해결
~~~ javascript
function getData(callback) {
  // new Promise() 추가
  return new Promise(function (resolve, reject) {
    $.get('url 주소/products/1', function (response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function (tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});
~~~
- 콜백 함수로 처리하던 구조에서 new Promise(), resolve(), then()와 같은 프로미스 API를 사용한 구조로 바뀌었습니다. 

### 프로미스의 3가지 상태(states)
- new Promise()로 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖습니다.
1. Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
2. Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
3. Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

~~~ javascript
먼저 아래와 같이 new Promise() 메서드를 호출하면 Pending(대기) 상태가 됩니다.
new Promise();

이렇게 new Promise() 메서드를 호출할 때 콜백 함수의 인자로 resolve, reject에 접근할 수 있습니다.
new Promise(function (resolve, reject) {
  // ...
});

여기서 콜백 함수의 인자 resolve를 아래와 같이 실행하면 Fulfilled(이행) 상태가 됩니다.
new Promise(function (resolve, reject) {
  resolve();
});

그리고 이행 상태가 되면 아래와 같이 then()을 이용하여 처리 결과 값을 받을 수 있습니다.

function getData() {
  return new Promise(function (resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function (resolvedData) {
  console.log(resolvedData); // 100
});



~~~

#### Rejected(실패)
new Promise()로 프로미스 객체를 생성하면 콜백 함수 인자로 resolve와 reject를 사용할 수 있다고 했습니다. 여기서 reject 인자로 reject() 메서드를 실행하면 Rejected(실패) 상태가 됩니다.
~~~ javascript
ew Promise(function (resolve, reject) {
  reject();
});

그리고, 실패 상태가 되면 실패한 이유(실패 처리의 결과 값)를 catch()로 받을 수 있습니다.

function getData() {
  return new Promise(function (resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function (err) {
  console.log(err); // Error: Request is failed
});
~~~

### 최종 쉬운 예제
~~~ javascript
function getData() {
  return new Promise(function (resolve, reject) {
    $.get('url 주소/products/1', function (response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// Fulfilled 또는 Rejected의 결과 값 출력
getData().then(function (data) {
  console.log(data); // response 값 출력
}).catch(function (err) {
  console.error(err); // Error 출력
});
~~~


### 여러 개의 프로미스 연결하기 (Promise Chaining)
- 프로미스의 또 다른 특징은 여러 개의 프로미스를 연결하여 사용할 수 있다는 점입니다. 앞 예제에서 then() 메서드를 호출하고 나면 새로운 프로미스 객체가 반환됩니다. 따라서, 아래와 같이 코딩이 가능합니다.

~~~ javascript
function getData() {
  return new Promise({
    // ...
  });
}

// then() 으로 여러 개의 프로미스를 연결한 형식
getData()
  .then(function (data) {
    // ...
  })
  .then(function () {
    // ...
  })
  .then(function () {
    // ...
  });
~~~

### 실무에서 있을 법한 프로미스 연결 사례
~~~ javascript
getData(userInfo)
  .then(parseValue)
  .then(auth)
  .then(diaplay);
~~~


### 프로미스의 에러 처리 방법
1. then()의 두 번째 인자로 에러를 처리하는 방법
~~~ javascript
getData().then(
  handleSuccess,
  handleError
);
~~~
2. atch()를 이용하는 방법
~~~ javascript
getData().then().catch();
~~~
