# useRef()

- 함수 컴포넌트에서 ref를 쉽게 사용할 수 있게 해주는 Hook
- 컴포넌트에서 특정 DOM을 선택해야할 때 사용
- useRef를 사용하여 ref를 설정하면 useRef를 통해 만든 객체 안의 current 값이 실제 엘리먼트를 가리킴

```
import { useState, useMemo, useCallback, useRef } from 'react';

const getAverage= numbers => {
    console.log('평균값 계산 중');
    if (numbers.length === 0) return 0;
    const sum = numbers.reduce((a,b) => a + b);
    return sum / numbers.length;
}

const Average = () =>{
    const [list, setList] = useState([]);
    const [number, setNumber] = useState('');
    // Ref 객체 생성
    const inputEl = useRef(null);

    const onChange = useCallback(e => {
        setNumber(e.target.value);
    }, []);

    const onInsert = useCallback(() => {
        const nextList = list.concat(parseInt(number));
        setList(nextList);
        setNumber('');
        // Ref 객체의 .current 값은 설정한 DOM를 가르킴 
        inputEl.current.focus();
    }, [number, list])

    const avg = useMemo(() => getAverage(list), [list]);

    return (
        <div>
            // DOM에 ref 값으로 생성한 Ref 를 설정
            <input value={number} onChange={onChange} ref={inputEl} />
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

### 참고
리액트를 다루는 기술