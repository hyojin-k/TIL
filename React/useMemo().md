# useMemo()
- 함수 컴포넌트 내부에서 발생하는 연산을 최적화 가능
- 렌더링하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고, 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 재사용하는 방식

>**useMemo(함수, 배열)**
- 두번째 파라미터인 배열의 값이 바뀔 때만 함수가 실행

#### 평균값 구하기
- list 배열의 내용이 바뀔 떄만 getAverage 함수 호출
```
import { useState, useMemo } from 'react';

const getAverege = numbers =>{
    console.log('평균값 계산 중);
    if( numbers.length === 0) return 0;
    const sum = numbers.reduce((a,b) => a + b);
    return sum / numbers.length;
}

const Average = () => {
    const [list, setList] = useState([]);
    const [number, setNumber] = useState('');

    const onChange = e =>{
        setNumber(e.target.value);
    }
    const onInsert = () =>{
        const nextList = list.concat(parseInt(number));
        setList(nextList);
        setNumber('');
    }

    const avg = useMemo(() => getAverage(list), [list]);

    return (
        <div>
            <input value={number} onChange={onChange} />
            <button onClick={onInsert}>등록</button>
            <ul>
                {list.map((value, index) => (
                    <li key={index}>{value}</li>
                ))}
            </ul>
            <p>평균값: {avg}</p>
        </div>
    )
}
```

#### 참고
리액트를 다루는 기술