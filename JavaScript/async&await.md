# async & await
- 프로미스를 좀 더 간결하게 사용하고 동기적으로 실행되는 것처럼 보이게 함
- 프로미스의 후속 처리 메서드(then, catch, finally) 없이 마치 동기 처리처럼 프로미스가 처리 결과를 반환하도록 구현할 수 있음

```
async function 함수명() {
    await 비동기처리메서드();
}
```

## async 
- 함수 앞에 async를 붙이면 코드블록이 프로미스로 바뀌면서 항상 프로미스를 반환(프로미스를 만들지 않아도 프로미스 상태값 반환)
- **어떤 함수에서도 Promise 반환**

## await
- async 없이 사용 x (async 함수 안에서만 동작)
- 프로미스 앞에 사용
- 프로미스가 처리 될 때 까지 기다렸다가(fulfilled 혹은 rejected) 처리 결과를 반환하고 다음 동작을 처리

```
<!-- 프로미스 객체를 반환하는 함수 -->
function fetchItems() {
    return new Promise(function(resolve, reject){
        var items = [1,2,3];
        resolve(items)
    })
}

<!-- async/await 사용 -->
async function logItems() {
    var resultItems = await fetchItems();
    console.log(resultItems); // [1,2,3]
}
```

## 에러 처리
- try...catch문을 사용하여 에러처리

```
async function logTodoTitle() {
    try{
        var user = await fetchUser();
        if (user.id === 1){
            var todo = await fetchTodo();
            console.log(todo.title);
        }
    } catch(error){
        console.log(error);
    }
}
```

**참고**

모던 자바스크립트 Deep Dive

[비동기, Promise, async, await 확실하게 이해하기](https://elvanov.com/2597)

[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)