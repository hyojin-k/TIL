# Intersection types (교차타입)

- 여러타입을 합쳐서 사용
- 해당하는 모든 속성을 입력해야함

```
interface Car {
    name: string;
    start(): void;
}

interface Toy {
    name: string;
    color: string;
    price: number;
}

<!-- 필요한 모든 기능을 가진 하나의 타입 생성 -->
const toyCar: Toy & Car = {
    name: 'toycar',
    start(){},
    color: 'blue',
    price: 1000
}
```
