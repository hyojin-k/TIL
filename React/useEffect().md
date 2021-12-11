# useEffect()

- 컴포넌트가 랜더링 될 때마다 특정 작업을 실행할 수 있도록 하는 훅 (Hooks)
- 클래스형 컴포넌트의 componentDidmout와 componentDidUpdate를 합친 형태로 볼 수 있음
- 컴포넌트가 mount, update, unmount 될 때 특정 작업 처리
- 랜더링되고 난 직후마다 실행되며, 두 번째 파라미터 배열에 무엇을 넣는지에 따라 실행되는 조건이 달라짐

>**useEffect( 수행하고자하는 작업, 검사하고자하는 특정 배열 or 빈배열)**

```
import { useState, useEffect } from 'react ;

const Info = () =>{
    const [name, setName] = useState('');
    const [nkckname, setNickname] = useState('');
    useEffect(() =>{
        console.log('랜더링 완료);
        console.log({
            name,
            nickname
        })
    })

    ...
}

export default Info;
```

### mount
- useEffect에서 설졍한 함수를 컴포넌트가 화면에 첫 랜더링 될 때 한 번 실행 (업데이트 될때는 실행 x)
- 두 번째 파라미터로 빈 배열 []

```
useEffect(() =>{
    console.log('mount')
}, [])
```

### update
- 특정 값이 변경될 때만 호출하고 싶을 때
- 두 번째 파라미터로 배열 안에 검사하고 싶은 값을 넣기

```
useEffect(() =>{
    console.log(name');
},[name])
```

### cleanup
- 컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떤 작업을 수행하고 싶으면  cleanup 함수를 반환해 주어야 함

**랜더링 될 때 마다 cleanup 실행**
- cleanup 함수가 호출될 때는 업데이트되기 직전의 값을 보여줌

```
useEffect(() =>{
    console.log('effect');
    console.log(name);
    return () =>{
        console.log('cleanup');
        console.log(name);
    };
},[name]);
```

**언마운트 될 때만  cleanup 실행**
- 두 번째 파라미터에 빈 배열
```
useEffect(() =>{
    console.log('effect');
    return() =>{
        console.log('unmount);
    };
},[]);
```

#### 참고
리액트를 다루는 기술