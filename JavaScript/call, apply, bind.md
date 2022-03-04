# call, apply, bind

- this를 window가 아닌 다른 객체로 만들어 주는 함수
- 자바스크립트에서는 함수 호출 방식과 상관없이 this를 지정할 수 있음

## call

- **함수를 호출**하면서 첫 번째 매개변수로 전달한 객체가 this에 바인딩 됨
- 매개변수를 , 를 사용하여 **리스트** 형식으로 전달

```
const zoe = {
    name: 'Zoe'
};

function showThisName() {
    console.log(this.name);
}

showThisName(); // this는 window

<!-- call을 사용하여 this로 사용할 객체를 넘김 -->
showThisName.call(zoe); // Zoe (this는 zoe)
```

**객체의 정보 업데이트**

- 첫번째 매개변수 : this로 사용될 값
- 두번째 매개변수 ~ : 함수가 사용할 매개변수 순서대로 입력

```
const zoe = {
    name: 'Zoe'
};

function update(age, location){
    this.age = age;
    this.location = location;
}

update.call(zoe, 20, 'seoul');
console.log(zoe); // {name: 'Zoe', age: 20, location:'seoul'}
```

## apply

- 매개변수를 처리하는 방법을 제외하고 **call과 동작 방식 동일**
- call은 매개변수를 리스트 형식으로 받지만, apply는 매개변수를 **배열**로 받음

```
const hyo = {
    name: 'Hyo'
}

update.call(hyo, [30, 'busan']);
console.log(hyo); // {name: 'Hyo', age: 30, location:'busan'}
```

- 배열 요소를 함수의 매개변수로 사용할 때 유용

```
const nums = [3,10,1,6,4];

<!-- spread 연산자 사용 -->
const minNum = Math.min(...nums);

<!-- call 사용 (this가 필요하지 않기 때문에 null 입력) -->
const maxNum = Math.max.call(null, ...nums); // (null, 3,10,1,6,4)

<!-- apply 사용 -->
const maxNum = Math.max.apply(null, nums); // (null, [3,10,1,6,4])
```

## bind

- 함수의 this 값을 영구적으로 바꿀 수 있음
- call, apply와 달리 **함수를 호출하지 않음**
- 새로 바인딩한 함수를 생성하여, 매개변수로 받은 값을 항상 this로 받음

```
const zoe = {
    name: 'Zoe'
}

function update(age, location){
    this.age = age;
    this.location = location;
}

<!-- 새로 바인딩한 함수 생성 -->
const updateZoe = update.bind(zoe); // this는 항상 zoe

updateZoe(10, 'LA');
console.log(zoe); // {name: 'Zoe', age: 10, location: 'LA'}
```

## call, apply, bind 비교

```
const user = {
    name: 'hyo',
    showName: function (){
        console.log(`hello, ${this.name}`);
    }
}

user.showName(); // hello, hyo

let fn = user.showName;

fn(); // hello, (this를 잃음)

<!-- call, apply -->
fn.call(user); // hello, hyo
fn.apply(user); // hello, hyo

<!-- bind -->
let bindFn = fn.bind(user);
bindFn(); // hello, hyo
```
