# this
- 함수를 **호출하는 방법**에 의해 결정되는 **자기 참조변수**

- 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조변수
    - 객체의 메서드 내부 또는 생성자 함수 내부에서만 의미가 있음
    - 일반 함수 내부에서는 this를 사용할 필요가 없기 때문에 undefined가 바인딩 됨
- this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있음

### 일반 함수 호출
- 기본적으로 this에는 **전역 객체**가 바인딩

```
function foo() {
    console.log("foo's this: ", this); // window
    function bar() {
        console.log("bar's this: ", this); // window
    }
    bar();
}
foo();
```

- 객체를 생성하지 않는 일반 함수에서 this는 의미가 없음
- strict mode가 적용된 일반 함수 내부의 this에는 **undefined** 바인딩

```
functino foo() {
    'use strict';

    console.log()("foo's this: ", this);  // undefined
    function bar() {
        console.log("bar's this: ", this);  // undefined
    }
    bar();
}
foo();
```
- 메서드 내에서 정의한 중첩 함수나 콜백 함수가 일반 함수로 호출되면 함수 내부의 this에는 전역 객체가 바인딩 
- 일반 함수로 호출된 모든 함수 내부의 this에 전역 객체가 바인딩

### 메서드 호출
- 메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 **호출한 객체**에 바인딩 됨
- 메서드는 프로퍼티에 바인딩된 함수로, 객체에 포함된 것이 아닌 독립적으로 존재하는 별도의 객체이기 때문에, 다른 객체의 프로퍼티에 할당되어 다른 객체의 메서드가 될 수도 있고, 일반 변수에 할당되어 일반 함수로 호출될 수도 있음

### 생성자 함수 호출
- 생성자 함수 내부의 this는 **생성자 함수가 생성할 인스턴스**를 가리킴


**참고**

모던 자바스크립트 Deep Dive