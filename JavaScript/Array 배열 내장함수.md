# Array 배열 내장함수

### .map()
- 유사 반복문
- array 내의 모든 데이터에 똑같은 작업을 시켜주고 싶을 때

```
const array = [1,2,3];
const newArray = array.map(function (a){
  return a*2  // [2,4,6] 새로운 array 반환
})
```
- 반복문 사용하기
  - title에 들어있는 하나하나의 데이터를 돌면서 차례로 출력
  - i : 반복문이 돌 때 마다 0,1,2,3...으로 변하는 변수
  - map 반복문으로 돌린 HTML에는 kety={ } 필요
```
const[title, setTitle] = useState([A,B,C]) ;

{
  title.map((a,i) =>{
    return (
      <div key={i}>
        {a}
      </div>  // A,B,C 
    )
  })
}
```

### .reduce()

- 배열에 있는 값들을 누적해서 연산

```
const array = [1.2.3.4];
const reducer = (누적된 값, 현재 값)=> 누적된 값 + 현재값 ;

console.log(Array). reduce(reducer);  // 10

<!-- 기본값(5)을 넣고 연산 -->
console.log(array.reduce(reducer, 5));  // 15
  ```
