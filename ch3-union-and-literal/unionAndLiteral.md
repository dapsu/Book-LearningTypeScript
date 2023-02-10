# 유니언 타입
```
두 가지 핵신 개념
- 유니언: 값에 허용된 타입을 두 개 이상의 가능한 타입으로 확장하는 것
- 내로잉: 값에 허용된 타입이 하나 이상의 가능한 타입이 되지 않도록 좁히는 것
```

## 내로잉
> 타입가드: 타입을 좁히는 데 사용할 수 있는 논리적 검사

```typescript
let admiral: number | string;
admiral = "Hopper";
admiral.toUpperCase();  // Ok: string
admiral.toFixed();  // Error: toFIxed does not exist on 'string'
```

처음에는 유니언 타입으로 선언되었지만 초깃값이 주어질 때 할당 내로잉이 작동하여 string으로 좁혀졌다는 것을 알 수 있다.

# 리터럴 타입
> 원시 타입 값 중 어떤 것이 아닌 특정 원싯값으로 알려진 타입

```typescript
let admiral: "Hopper";
admiral = "Hopper";
```

- 유니언 타입으로 리터럴과 원시 타입을 섞어서 사용할 수 있다.
- 엄격한 null 검사를 활성해햐만 코드가 null 또는 undefined 값으로 인한 오류로부터 안전한지 여부를 쉽게 파악할 수 있다.

# 타입 별칭
> 재사용하는 타입에 더 쉬운 이름 할당

```typescript
type RawData = boolean | number | string | null | undefined ;  // 타입 별칭은 파스칼 케이스로 지정

let firstData: RawData;
let secondData: RawData;
let thirdData: RawData;
```

- 타입 별칭은 자바스크립트가 아니다. 즉 타입 별칭은 순전히 '개발 시'에만 존재한다.
