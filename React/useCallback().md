# useCallback()

- 렌더링 성능을 최적화
- 함수를 새로 만들지 않고 재사용하고 싶을 때 사용
- 컴포넌트의 렌더링이 자주 발생하거나 렌더링해야 할 컴포넌트의 개수가 많아지면 최적화 해주는 것이 좋음

>**useCallback(생성하고 싶은 함수, 배열)**
- 배열에는 어떤 값이 바뀌었을 때 함수를 새로 생성해야하는지 명시
- 함수 내부에서 상태 값에 의존해야 할 때는 그 값을 반드시 두번째 파라미터 안에 포함시켜주어야 함
- [] 
    - 컴포넌트가 렌더링될 때 만들었던 함수를 계속해서 재사용
    - 기존의 값을 조회하지 않고 바로 설정만 하기 때문에 배열이 비어있어도 됨
- [number] 
    - input 내용이 바뀌거나 새로운 항목이 추가될 때 새로 만들어진 함수 사용
    - 기존의 number를 조회해서 새로운 것을 생성하기 때문에 배열안에 넣어주어야 함

```
import { useState, useMemo, useCallback } from 'react';

const getAverage= numbers => {
    console.log('평균값 계산 중');
    if (numbers.length === 0) return 0;
    const sum = numbers.reduce((a,b) => a + b);
    return sum / numbers.length;
}

const Average = () =>{
    const [list, setList] = useState([]);
    const [number, setNumber] = useState('');

    // 컴포넌트가 처음 랜더링될 때만 함수 생성
    const onChange = useCallback(e => {
        setNumber(e.target.value);
    }, []);

    // number나 list가 바뀌었을 때만 함수 생성
    const onInsert = useCallback(() => {
        const nextList = list.concat(parseInt(number));
        setList(nextList);
        setNumber('');
    }, [number, list])

    const avg = useMemo(() => getAverage(list), [list]);

    return (
        <div>
            <input value={number} onChange={onChange} />
            <button onClick={onInsert}>등록</button>

            <ul>>
                {list.map((value, index) => (
                    <li key={index}>{value}</li>
                ))}
            </ul>
            <p>평균값:{avg}</p>
        </div>
    )
}

export default Average;
```

#### useMemo vs useCallback
- useMemo : 특정 결과값을 재사용 할 때 사용
- useCallback : 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용 

#### 참고
리액트를 다루는 기술