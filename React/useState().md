# useState()

## state(상태)
- 컴포넌트에서 동적인 값
- 변수 대신 쓰이는 리액트의 데이터 저장 공간
- useState()를 이용해 만들어야 함

## useState()

- 리액트 훅(Hooks) 함수 중 하나
- 함수형 컴포넌트에서 상태 관리 가능
----

**const [상태 값 저장 변수, 상태 값 갱신 함수] = useState(상태 초기 값)**

```
// 상태의 기본값을 파라미터로 넣어서 호출
const [number, setNumber] = useState(0);
```
- number - 현재 상태 값 변수
- setNumber - 상태값을 갱신해주는 Setter 함수
- useState(0) - 상태의 초기 값 (string, number, Object, array 전부 담을 수 있음)

**전체 코드**

```
// 리액트에 있는 내장함수를 가져다 쓸 것
import React, {useState} from 'react';

function App(){
    const [abc,setAbc] = useState(['a','b','c'])  => 변수에 담음

    function changeWord(){
        <!-- setTitle(['A','b','c']) //state를 아예 대체해주는 함수 -->

        <!-- state의 복사본 생성(deep copy) - 값 공유를 하지 않고 완전히 새로운 배열 복사 (spread 사용) -->
        let newArray = [...abc]; 
        newArray[0] = 'A';
        setAbc(newArray)

    return (
        <div>
            <p>{abc[0]}</p>   // a

            <!-- changeWord() 바로 호출 시키면 안됨 -->
            <!-- 클릭하면 a에서 A로 바뀜 -->
            <p onClick={()=>{changeWord}}><span>{abc[0]}</span></p>
        </div>
    )
}

export default App;
```
---

#### state에 데이터 저장하는 이유
- state는 변경되면 HTML이 자동으로 재랜더링이 됨
- 새로고침 없이 재렌더링 되도록 하기 위해
- 자주 바뀌는 중요한 데이터를 변수 대신 state 로 저장해서 쓰면 좋음