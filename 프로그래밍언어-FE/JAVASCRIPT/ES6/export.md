### default
- ES6의 module 문법 표준에 따르면 export 는 2가지 종류가 있다.
1. named exports (모듈 당 여러 개의 export)
- 하나의 module 파일이라도 이 중 일부만 필요로 하는 경우가 있을 수 있다. 예를 들어 하나의 함수 혹은 하나의 클래스 만 사용하고 싶은 경우이다. 이런 때 es6 module 문법은 다음과 같은 형식으로 이를 가능하게 한다.
~~~ javascript
    //------ lib.js ------
    export const sqrt = Math.sqrt;
    export function square(x) {
        return x * x;
    }
    export function diag(x, y) {
        return sqrt(square(x) + square(y));
    }
    
    //------ main.js ------
    import { square, diag } from 'lib';
    console.log(square(11)); // 121
    console.log(diag(4, 3)); // 5
~~~

2. default exports (모듈 당 하나의 export)
- node 개발자는 변수 하나만 export 하는 등의 방식이 빈번히 사용되는데, front end 개발자의 경우는 constructor나 class를 export 하는 경우가 많다. 이런 경우 하나의 module이 하나의 export만 갖는 경우가 되는데 이런 때 사용할 수 있는 것이 default exports 이다.
~~~ javascript
    //------ myFunc.js ------
    export default function () { ... };
    
    //------ main1.js ------
    import myFunc from 'myFunc';
    myFunc();

    //------ MyClass.js ------
    export default class { ... };
    
    //------ main2.js ------
    import MyClass from 'MyClass';
    let inst = new MyClass();
~~~
