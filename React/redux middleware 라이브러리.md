# redux middleware 라이브러리
- 리덕스를 쉽게 쓸 수 있도록 도와주는 역할을 하는 라이브러리 
- 액션이 스토어에서 상태값을 바꾸기 전에 특정 작업들을 수행하도록 함
- store의 state를 변경하기 위해서는 dispatch를 이용해서 action으로 **객체만** 변경가능

![middleware](https://user-images.githubusercontent.com/50295043/149663794-d2c8181b-9488-4d9e-881e-8b34b7a83279.png)


## redux-thunk
- 비동기 작업을 처리 할 때 사용
- 객체 대신 **함수**를 생성하는 액션 생성함수를 작성할 수 있도록 함
- 비동기 작업 함수를 만들어 필요한 시점에 불러와 액션을 디스패치
- dispatch와 getState를 파라미터로 받아옴
- redux-saga에 비해 로직이 간단하고, 빠르고 간단한 서비스에 용이

## redux-saga
- 비동기 작업을 처리할 때 사용
- 액션을 모니터링 하고 있다가 특정 액션이 발생했을 때 미리 정해둔 로직에 따라 작업이 이루어지는 방식
- **Generator** 문법 사용
- **순수 함수**로 이루어져 side-effect가 적고 테스트 코드를 작성하기 용이
- redux-thunk에 비해 많은 기능 수행할 수 있으며, 사이즈가 크고 복잡한 서비스에 사용

## redux-logger
- Redux DevTools와 같은 역할
- 액션을 콘솔에 출력하여 리듀서가 실행되기 전과 실행된 후를 쉽게 비교할 수 있도록 함

```
import { createStore, applyMiddleware } from 'redux';
import { createLogger } from 'redux-logger';
import reducers from './reducers';

const logger = createLogger();

const store = createStore(reducers, applyMiddleware(logger));
```

## redux-actions
- createAction을 사용하여 액션 생성함수를 간단하게 작성
```
<!-- createAction 사용 x -->
const ADD_USER = 'ADD_USER';

export const add_user = user => ({type: ADD_USER, user});

<!-- createAction 사용 o -->
import {createAction} from 'redux-actions'; 
const ADD_USER = 'ADD_USER';

export const add_user = createAction(ADD_USER, user => user);
```

- 리듀서를 switch문이 아닌 handleActions 함수를 사용하여 작성할 수 있음
```
<!-- handleActions 사용 x -->
const reducer = (state = initialState, action) =>{
    switch (action.type){
        case ADD_USER:
            return {...state, user: action.user}
    }
}

<!-- handleActions 사용 o -->
import {handleActions} from 'redux-actions';
const reducer = handleActions({
    [ADD_USER]: (state, action) => ({...state, user: action.user})
})
```


**참고**

[벨로퍼트와 함께하는 모던 리액트](https://react.vlpt.us/redux-middleware/10-redux-saga.html)