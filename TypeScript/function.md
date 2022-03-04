# 함수 (function)

- 매개변수 타입과 함수가 반환하는 타입 입력
- 반환 타입을 파악할 수 있으므로 반환 타입 생략 가능

```
function add(num1: number, num2: number): number { // (매개변수 타입):리턴 값 타입
    return num1 + num2;
}

function isAdult(age:number): boolean{
    return age > 19;
}

<!-- return을 하지 않는 경우 void -->
function add(num1: number, num2: number): void{
    console.log(num1 + num2);
}
```

## ? (선택적 매개변수)

- 입력해도되고 안해도 되는 매개변수

```
function hello(name?: string){
    return `Hello, ${name || 'world'}`;
}

const result = hello();
```

- 기본-초기화 매개변수

```
<!-- 매개변수의 default 값 지정 (? 사용한 함수와 같은 함수) -->
function hello2(name = 'world'){
    return `Hello, ${name}`;
}

const result = hello2();
```

- 선택적 매개변수가 필수 매개변수보다 먼저 있으면 안됨

```
function hello3(name:string, age?: number):string{
    if(age !== undefined){
       return `Hello ${name}. You are ${age}`
    }else{
        return `Hello ${name}`
    }
}

console.log(hello3('kim'))

<!-- 선택적 매개변수를 먼저 쓰고 싶을 때 (undefined 전달) -->
function hello3(age: number | undefined, name:string ):string{
    if(age !== undefined){
       return `Hello ${name}. You are ${age}`
    }else{
        return `Hello ${name}`
    }
}
console.log(hello3(20, 'kim'))
console.log(hello3(undefined, 'kim'))
```

## ... (나머지 매개변수)

- 매개변수의 갯수가 바뀔 수 있음
- 전달받은 매개변수를 배열로 나타낼 수 있음

```
function add(...nums: number[]){
    return nums.reduce((result, num) => result + num, 0);
}

console.log(add(1,2,3)); // 6
console.log(add(1,2,3,4,5)); // 15
```

## this

- 함수의 첫번째 매개변수에 (this:type) 입력

```
interface User{
    name: string;
}

const Zoe: User = {name: 'Zoe'};

function showName(this:User, age:number, gender:'m'|'f'){
    console.log(this.name, age, gender)
}

const a = showName.bind(Zoe)

<!-- this를 제외한 매개변수 전달 -->
a(20, 'f'); // Zoe, 20, f
```

## 오버로드

- 전달받은 매개변수의 갯수나 타입에 따라 다른 방식으로 동작하여 리턴값이 달라지는 경우 사용

```
interface User {
    name: string;
    age: number;
}

<!-- 오버로드 -->
function join(name: string, age:number) : User;
function join(name: string, age:string) : string;

function join(name: string, age:number|string): User |string{
    if(typeof age === 'number'){
        return{
            name,
            age
        }
    }else{
        return '나이는 숫자로 입력하세요'
    }
}

const zoe: User = join('zoe', 10);
const hyo: string = join('hyo', '20')
```
