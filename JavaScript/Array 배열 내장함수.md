# Array 배열 내장함수

### .reduce()

- 배열에 있는 값들을 누적해서 연산

```
const array = [1.2.3.4];
const reducer = (누적된 값, 현재 값)=> 누적된 값 + 현재값 ;

console.log(Array). reduce(reducer);  // 10

<!-- 기본값(5)을 넣고 연산 -->
console.log(array.reduce(reducer, 5));  15
  ```
