# 비동기 처리
>  비동기(asychronous) 작업이란?
- 동기적(synchronous) 처리 방시은 하나의 작업이 끝날때까지 기다리는 동안 중지 상태가 되어 다른 작업을 동시에 할 수 없는 반면, 비동기적 작업은 동시에 여러가지 작업 처리 가능
- Ajax, setTimeout, setInterval ....

> 자바스크립트가 동작하는 방식
- 싱글 스레드(single thread) 방식 : 자바스크립트는 하나의 실행 컨텍스트 스택을 가지고 있고, 이는 2개 이상의 함수를 동시에 실행할 수 없음을 뜻함
- 콜백 패턴을 사용 -> 콜백 헬(비동기가 중첩이 되면서 코드가 깊어지고 문제를 해결하기가 어려워지는 현상) 발생 


메모리 힙, 콜스택, 콜백큐, 콜백함수, 이벤트 루프


> 콜백이란?
* 자바스크립트가 비동기 처리를 하기 위한 패턴 중 하나

콜백함수 - 어떤 함수의 인수로 넘겨주는 함수

콜백 헬 - 비동기가 중첩이 되면서 코드가 깊어지고 문제를 해결하기가 어려워지는 현상

> Promis (프로미스)
- 콜백 헬을 해결하기 위해 도입됨
- 비동기 처리가 종료된 이후에 결과를 알기 위해 사용하는 객체
- 작업이 성공했는지 실패했는지 프로미스의 선택값으로 알 수 있음

* 프로미스의 상태값
pending : 아직 처리되지 않음
fulfilled : 성공
rejected : 실패
settled : 성공 or 실패

* 프로미스 후속처리 메소드를 통해 비동기 처리 결과를 받음
성공시 .then
실패시 .catch 로 받아옴

> 프로미스로 콜백 헬을 해결하는 방식
* 후속처리 메소드(.then)를 이어서(체이닝) 여러개의 프로미스를 연결해 해결

> async, await
async 
* 함수 앞에 async를 붙이면 항상 프로미스를 반환(프로미스를 만들지 않아도 프로미스 상태값 반환)

await
* async 없이 사용 x (async 함수 안에서만 동작)
* 프로미스가 처리 될 때 까지 기다렸다가 처리 결과를 반환하고 다음 동작을 처리

async function myFunc1(){
    let promise = new Promise((resolve, reject) =>{
        setTimeout(() => resolve('hello), 1000)
    })

console.log(promise);

let result = await promise;

console.log(promise);
console.log(result);

}



