# Union (유니온)

## 식별 가능한 Union 타입

- 여러 타입 중 하나가 될 수 있는 값으로, | 를 사용하여 타입을 구분함
- 유니온에 있는 모든 타입에 공통인 멤버들에만 접근 가능

```
interface Car {
  name: 'car';
  color: string;
  start(): void;
}

interface Mobile {
  name: 'mobile';
  color: string;
  call(): void;
}

function getGift(gift: Car | Mobile) {
  console.log(gift.color);
  gift.start(); // start는 Car에만 존재하므로 error

  <!-- 타입을 다르게 줘서 interface 구분 (항목이 많아지면 switch문 사용) -->
  if(gift.name === 'car'){
    gift.start();
  }else{
    gift.call();
  }
}
```
