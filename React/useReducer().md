# useReducer()

- useState보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트 해주고 싶을 때 사용하는 Hook
- 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리 가능

### reducer
- 현재 상태와 업데이트를 위해 필요한 정보를 담은 action 값을 파라미터로 전달받아 새로운 상태를 반환하는 함수
- 리듀서 함수에서 새로운 상태를 만들 때 반드시 '불변성'을 지켜주어야 함

>**const [state, dispatch] = useReducer(reducer, initialState)**
- state: 컴포넌트에서 사용할 수 있는 상태
- dispatch: 액션을 발생시키는 함수, 함수 안에 파라미터로 액션 값을 넣으면 리듀서 함수가 호출 됨
 ``` 
  dispatch({ type: 'INCREMENT' })
  ```
- 첫 번째 파라미터: reducer 함수
- 두 번째 파라미터: 초기 값 

#### 기존 코드 (useReducer 적용 전)
```
import React, { useState } from 'react';

function Counter() {
    const [number, setNumber] = useState(0);

    const onIncrease = () =>{
        setNumber(prevNumber => prevNumber + 1);
    };
    const onDecrease = () =>{
        setNumber(prevNumber => prevNumber - 1);
    };

    return (
        <div>
            <h1>{number}</h1>
            <button onClick={onIncrease}> +1 </button>
            <button onClick={onDecrease}> -1 </button>  
        </div>
    );
}

export default Counter;
```

#### useReducer 적용

>#### Counter.js

```
import React, { useReducer } from 'react';

function reducer(state, action) {
    // action.type에 따라 다른 작업 수행
    switch (action.type) {
        case 'INCREMENT':
            return { value: state.value +1 };
        case 'DECREMENT':
            return { value: state.value -1 };

        //아무것도 해당되지 않을 때 기존 state 반환
        default:
            return state;
    }
}

const Counter = () =>{
    // 첫번째 파라미터 - 리듀서 함수
    // 두번째 파라미터 - 리듀서의 기본 값
    const [state, dispatch] = useReducer(reducer, { value:0 });

    return (
        <div>
            <p>현재 카운터 {state.value}</p>
            <button onClick={() => dispatch({type:'INCREMENT'})}>+1</button>
            <button onClick={() => dispatch({type:'DECREMENT'})}>-1</button>
        </div>
    );
};

export default Counter;
```

>#### Info.js
- input 상태관리
- 이벤트 객체가 지니고 있는 e.target 값 자체를 액션 값으로 사용
- 불변성을 지키기 위해 spread 연산자(...) 사용
```
import React, ( useReducer ) from 'react';

function reducer(state, action){
    return{
        ...state,
        [action.name]: action.value
    };
};

const Info = () =>{
    const [state, dispatch] = useReducer(reducer,{
        name:''.
        nickname: ''
    });
    const { name, nickname } = state;
    const onChange = e =>{
        dispatch(e.target);
    };

    return (
        <div>
            <input name='name' value={name} onChange={onChange} />
            <input name='nickname' value={nickname} onChange={onChange} />
            <div>
                <p>이름: {name}</p>
                <p>닉네임: {nickname}</p>
            </div>
        </div>
    )
}

export default Info;
```

### useReducer vs useState
- useState : 컴포넌트에서 관리하는 값이 하나이고, 그 값이 단순한 숫자, 문자열, boolean 값일 때
- useReducer : 컴포넌트에서 관리하는 값이 여러개이고 상태의 구조가 복잡할 때

#### 참고
[벨로퍼트와 함께하는 모던 리액트](https://react.vlpt.us/basic/20-useReducer.html)
리액트를 다루는 기술