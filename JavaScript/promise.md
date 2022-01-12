# Promise (프로미스)
- 콜백함수로 발생되는 콜백 헬을 해결하기 위해 도입됨
- 콜백함수 대신 비동기적인 작업을 하기 위해 사용되는 자바스크립트 내장 객체로, 비동기 처리 상태와 처리 결과를 알 수 있음
- **new 연산자**를 사용하여 Promise 객체 생성
- 새로운 promise가 만들어지면, 전달하는 콜백함수가 바로 실행됨
- 비동기 처리를 수행할 콜백 함수를 인수로 전달받는데, 이 콜백 함수는 resolve(성공 시 호출)와 reject(실패 시 호출) 함수를 인수로 전달 받음

```
const promise = new Promise((resolve, reject) => {
    if(true){
        /* 비동기 처리 성공 시 */
        resolve('result');
    } else { 
        /* 비동기 처리 실패 시*/
        reject('failure reason')
    }
})
```

## 프로미스의 상태값 (state)
- 작업이 실행되고 있는 중인지 / 작업이 끝나고 성공 혹은 실패 상태인지 알 수 있음
### pending 
- 아직 처리되지 않고 수행 중 => 프로미스가 생성된 직후 기본 상태
### fulfilled 
- 비동기 처리 **성공** => resolve 함수 호출
- then()을 이용하여 처리 결과 값 반환
### rejected 
- 비동기 처리 **실패** => reject 함수 호출
- catch()를 이용하여 처리 결과 값 반환
### settled 
- fulfilled or rejected 상태와 상관없이 pending이 아닌 상태

![promise](https://user-images.githubusercontent.com/50295043/149156896-31e2f069-ed63-4e11-9a52-d467bad5a045.png)


## 프로미스 후속처리 메소드

- 프로미스의 비동기 처리 상태가 변화하면 후속 처리 메소드에 인수로 전달한 콜백 함수가 선택적으로 호출
- 후속 처리 메소드의 콜백함수에 프로미스의 처리 결과가 인수로 전달
- 모든 후속 처리 메소드는 프로미스를 반환하며, 비동기로 동작함

### 프로미스 후속처리 메소드 종류
#### .then
- 두 개의 콜백 함수를 인수로 전달받으며, 첫 번째 콜백함수는 비동기 처리가 성공했을 때 호출되는 성공처리 콜백함수, 두번째 콜백함수는 비동기 처리가 실패 했을 때 호출되는 실패 처리 콜백함수

```
<!-- fulfilled -->
new Promise(resolve => resolve('filfilled'))
    . then(v => console.log(v), e => console.error(e));  // fulfilled

<!-- rejected -->
new Promise((_, reject) => reject(new Error('rejected')))
    . then(v => console.log(v), e => console.error(e));  // Error:rejected
```

#### .catch
- 한개의 콜백 함수를 인수로 전달받아 프로미스가 **rejected**인 경우에만 호출

```
<!-- rejected -->
new Promise((_, reject) => reject(new Error('rejected')))
    .catch(e => console.log(e));
```

#### .finally
- 프로미스의 성공, 실패와 상관없이 무조건 한 번 호출
- 성공, 실패 관계없이 어떠한 기능을 마지막으로 실행하고 싶을 때 사용

```
new Promise(() =>{})
    .finally(() => console.log('finally'))
```

### 프로미스로 콜백 헬을 해결하는 방식
- 후속처리 메소드는 언제나 콜백함수가 반환하는 프로미스를 반환하므로 연속적으로 호출 가능 => **프로미스 체이닝**

## 프로미스의 정적 메소드
### Promise.all([])
- 한꺼번에 실행되고, 모든 실행이 완료되면 그 값을 불러올 수 있음 (모든 작업이 완료될 때까지 기다림)
- 하나라도 에러가 뜨면 모든 값을 불러올 수 없음

### Promise.race([])
- 가장 먼저 완료된 값만 가져옴

**참고**

모던 자바스크립트 Deep Dive

[비동기, Promise, async, await 확실하게 이해하기](https://elvanov.com/2597)