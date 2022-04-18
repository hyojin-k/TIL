# Literal (리터럴)

## 문자열 리터럴 타입

- 정해진 string 값을 가짐

```
<!-- const : 정해진 문자만 사용 가능 -->
const user1 = 'hyo'; // const user1: 'hyo'

<!-- let : 정해진 타입만 사용 가능 -->
let user2 = 'jin'; // let user2: string
let user3: string | number = 'zoe';

user2 = 2; // 불가능
user3 = 3; // 가능
```

### type 사용

```
type Word = 'A' | 'B' | 'C' ;

interface User {
    name: string;
    word: Word;
}

const user: User = {
    name: 'hyo',
    word: 'D' // 불가능 (type Word에서 지정한 값들만 사용 가능)
}
```

## 숫자형 리터럴 타입

- 정해진 숫자만 사용 가능

```
interface Student {
    name: string;
    grade: 1 | 2 | 3; // union 사용
}
```
