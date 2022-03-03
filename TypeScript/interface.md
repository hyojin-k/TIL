# 인터페이스 (interface)

- 타입 체크를 위해 사용되며 변수, 함수, 클래스에 사용
- 프로퍼티 또는 메소드를 정의해서 객체를 표현하고자할 때 사용하며, **일관성을 유지**할 수 있도록 함
- 인터페이스는 타입스크립트 파일을 자바스크립트 파일로 트랜스컴파일 되면서 삭제됨

## 변수

- ? (옵셔널/선택적 프로퍼티)
  - 생략해도 에러가 발생하지 않음
- readonly
  - 읽기 전용 (수정 불가능)
- [key:number] : string
  - **key(숫자):value(문자열)** 인 프로퍼티를 여러개 받을 수 있음 (없어도 에러 발생 x)

```
type Score = 'A' | 'B' | 'C' | 'F'; // 문자열 리터럴

interface User {
    name: string;
    age: number;
    gender? : string;
    readonly birthYear: number;
    [grade:number] : Score;
}

let user : User = {
    name: 'kim',
    age: 10,
    birthYear : 2000,
    1: 'A',
    2: 'B',
}

user.age = 20;
user.gender = 'male'; // ? 를 사용하지 않은 상태라면 에러 발생
user.bitrhYear = 2010; // readonly이기 때문에 수정 불가능

```

**인터페이스를 사용하여 함수 파라미터 타입 선언**

```
interface User {
    name: string;
    age: number;
    gender? : string;
    readonly birthYear: number;
}

let users: User[] = [];

function addUser(user2: User){
    users = [...users, user2]
}

const newUser: User = {
    name:'jin',
    age: 12,
    gender: 'F',
    birthYear: 2010
}

addUser(newUser);
console.log(users); // [{name:'jin', age:12, gender:'F', birthYear:2010}]
```

## 함수

- 인터페이스를 함수의 타입으로 사용
- 타입이 선언된 파라미터 리스트와 리턴 타입 정의

```
interface Add {
    (num1:number, num2: number) : number; // (파라미터 리스트) : 리턴 타입
}

const add : Add = function(x,y){
    return x+y;
}

console.log(add(10,20));
```

**화살표 함수 사용**

```
interface IsAdult {
    (age:number):boolean;
}

const age : IsAdult = (age) =>{
    return age >19;
}

a(30); // true
```

## 클래스

- implements 키워드 뒤에 인터페이스를 선언하면 해당 클래스는 지정된 인터페이스를
  따라야함
- 프로퍼티와 메소드를 가질 수 있다는 점에서 클래스와 유사하나 직접 인스턴스를 생성할 수는 없음

```
interface Car {
    color: string;
    wheels: number;
    start():void;
}

class Bmw implements Car{
    color: 'black';
    wheels: 4;
    start(){
        console.log('start');
    }
}

<!-- 컴파일 형태 -->
class Bmw {
    constructor(){
        this.color = 'black';
        this.wheels = 4;
    }
    start(){
        console.log('start');
    }
}
```

**constructor 사용**

- 생성될 때 color를 입력받음

```
interface Car {
    color: string;
    wheels: number;
    start():void;
}

class Bmw implements Car{
    color;
    wheels = 4;
    constructor(c:string){
        this.color = c;
    }
    start(){
        console.log('start');
    }
}

const b = new Bmw('white');

<!-- 컴파일형태 -->
class Bmw {
    constructor(c){
        this.wheels = 4;
        this.color = c;
    }
    start(){
        console.log('start');
    }
}

const b = new Bmw('white');
console.log(b);
b.start();
```

**interface 확장(extends)**

- 기존 인터페이스를 상속받아 확장 가능
- 복수의 인터페이스 상속 가능

```
interface Car {
    color: string;
    wheels: number;
    start():void;
}

interface Owner{
    name: string;
}

<!-- 2개의 인터페이스 상속 -->
interface Benz extends Car, Owner {
    door: number;
    stop():void;
}

const benz : Benz ={
    name: 'kim',
    color: 'red',
    wheels: 4,
    door: 4,
    start(){
        console.log('start')
    },
    stop(){
        console.log('stop')
    }
}

console.log(benz)
```

**참고**

[TypeScript - Interface](https://poiemaweb.com/typescript-interface)
