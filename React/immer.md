# immer (불변성 유지)

- 구조가 복잡한 객체의 불변성을 유지하면서 업데이트할 수 있도록 하는 라이브러리
- 불변성에 신경 쓰지 않는 것처럼 코드를 작성하되 불변성 관리는 제대로 하는 것이 목적

- produce(state, draft => { })
    - 첫번째 파라미터 : 수정하고 싶은 상태
    - 두번째 파라미터 : 상태를 어떻게 업데이트할지 정의하는 함수
    - 두번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면, produce 함수가 불변성 유지를 대신해주면서 새로운 상태를 생성

```
import produce from 'immer';

const state = [
    {
        id:1,
        todo: '리액트',
        checked: true,
    },
    {
        id:2,
        todo: '자바스크립트',
        checked: false,
    }
]

const nextState = produce(state, draft =>{
    // id가 2인 todo의 checked 값 수정
    const todo = draft.find(t => t.id ===2);
    todo.checked = true;

    // 새로운 데이터 추가
    draft.push({
        id:3,
        todo: '타입스크립트',
        checked: false,
    });

    // id가 1인 항목 제거
    draft.splice(draft.findIndex(t => t.id ===1), 1);
})

```

### useState의 함수형 업데이트와 immer 함께 쓰기
- produce 함수를 호출할 때, 첫 번째 파라미터가 함수 형태이면 업데이트 함수를 반환

```
const update = produce(draft =>{
    draft.value = 2;
})

const state = {
    value: 1,
    foo: 'bar',
}
const nextState = update(state);
console.log(nextState) // {value:2, foo: 'bar}
```

### 불변성 유지 비교 예시 코드

```
  const onChange = useCallback(
    e =>{
      const {name, value} = e.target;
       
      <!-- immer를 사용하지 않고 불변성 유지  -->
      setForm({
        ...form,
        [name] : [value]
      });

      <!-- immer 사용 -->
      setForm(
        produce(form, draft => {
          draft[name] = value;
        })
      )

      <!-- useState 함수형 업데이트 + immer -->
      setForm(
        produce(draft =>{
          draft[name] = value;
        })
      )
    },
    [form]
  )
```


#### 참고
리액트를 다루는 기술