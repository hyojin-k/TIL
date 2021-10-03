
# Promise

## Promise (프로미스)
- 콜백함수로 발생되는 콜백 헬을 해결하기 위해 도입됨
- 비동기 처리가 종료된 이후에 결과를 알기 위해 사용하는 객체
- 작업이 성공했는지 실패했는지 프로미스의 선택값으로 알 수 있음

```
const promise = new Promise((resolve, reject) => {
    if(/* 비동기 처리 성공 시 */){
        resolve('result');
    } else { /* 비동기 처리 실패 시*/
        reject('failure reason')
    }
})

```

## 프로미스의 상태값
- pending : 아직 처리되지 않음 => 프로미스가 생성된 직후 기본 상태
- fulfilled : 성공 => resolve 함수 호출
- rejected : 실패 => reject 함수 호출
- settled : fulfilled or rejected 상태와 상관없이 pending이 아닌 상태

## 프로미스 후속처리 메소드

- 프로미스의 비동기 처리 상태가 변화하면 후속 처리 메소드에 인수로 전달한  콜백 함수가 선택적으로 호출
- 후속 처리 메소드의 콜백함수에 프로미스으 처리 결과가 인수로 전달

#### 프로미스 후속처리 메소드 종류
- .then
     - 두 개의 콜백 함수를 인수로 전달받으며, 첫 번째 콜백함수는 비동기 처리가 성공했을 때 호출되는 성공처리 콜백함수, 두번째 콜백함수는 비동기 처리가 실패 했을 때 호출되는 실패 처리 콜백함수

```
<!-- fulfilled -->
new Promise(resolve => resolve('filfilled))
    . then(v => console.log(v), e => console.error(e));  // fulfilled

<!-- rejected -->
new Promise((_, reject) => reject(new Error('rejected')))
    . then(v => console.log(v), e => console.error(e));  // Error:rejected
```

- .catch
    - 한개의 콜백 함수를 인수로 전달받아 프로미스가 rejected인 경우에만 호출

```
<!-- rejected -->
new Promise((_, reject => reject(new Error('rejected))))
    .catch(e => console.log(e));
```

- .finally
    - 프로미스의 성공, 실패와 상관없이 무조건 한 번 호출

```
new Promise(() =>{})
    .finally(() => console.log('finally'))
```

## 프로미스로 콜백 헬을 해결하는 방식
- 후속처리 메소드는 언제나 프로미스를 반환하므로 연속적으로 호출 가능
- 후속처리 메소드는 콜백 함수가 반환한 프로미스를 반환

