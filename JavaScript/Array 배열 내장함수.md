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
  - map 반복문으로 돌린 HTML에는 key={ } 필요
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
const array = [1, 2, 3, 4];
const reducer = (누적된 값, 현재 값)=> 누적된 값 + 현재값 ;

console.log(Array). reduce(reducer);  // 10

<!-- 기본값(5)을 넣고 연산 -->
console.log(array.reduce(reducer, 5));  // 15
  ```

### .concat()
- 인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 추가로 새 배열을 반환
- 기존 배열은 그대로 유지하고 사본으로 새 배열 리턴

```
const num1 = [1, 2, 3];
const num2 = [4, 5, 6];
const text = ['a', 'b', 'c'];

const arr1 = num1.concat(num2);
const arr2 = num1.concat(num2, text);

console.log(arr1); // [1, 2, 3, 4, 5, 6];
console.log(arr2); // [1, 2, 3, 4, 5, 6, 'a', 'b', 'c'];
```

### .join()
- 배열의 모든 요소를 문자열로 변환 후 연결해 하나의 문자열로 반환
- 인자로 전달된 구분문자를 사용하여 문자열을 연결

```
const text = ['a', 'b', 'c'];

// 구분문자가 없으면 기본 값으로 , 사용 (띄어쓰기 x)
const join1 = text.join(); // 'a,b,c'

// 구분문자가 빈 문자열이면 하나의 문자열로 합칩
const join2 = text.join(''); // 'abc'

// 구분문자 사용
const join3 = text.join(', '); // 'a, b, c'
const join4 = text.join(' - '); // 'a - b - c'
```