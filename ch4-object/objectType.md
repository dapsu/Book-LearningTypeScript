# 객체 타입
```typescript
const poet = {
  born: 1935,
  name: "Mary Oliver",
};

poet["born"];  // type: number
poet.name;  // type: string
poet.end;  // Error: Property 'end' does not exist on type
```
null과 undefined를 제외한 모든 값은 그 값에 대한 실제 타입의 멤버 집합을 가지므로 타입스크립트는 모든 값의 타입을 확인하기 위해 객체 타입을 이해해야 한다.

## 별칭 객체 타입
```typescript
type Poet = {
  born: number;
  name: string;
};

let poetLater: Poet;
poetLater = {
  born: 1935,
  name: "Sara",
;}
```

# 구조적 타이핑
타입스크립트의 시스템은 구조적으로 타입화되어 있기 때문에 타입을 충족하는 모든 값을 해당 타입의 값으로 사용할 수 있다.
```typescript
type WithFirstName = {
  firstName: string;
};

type WithLastName = {
  lastName: string;
};

const hasBoth = {
  firstName: "Lionel",
  lastName: "Messi",
};

let withFirstName: WithFirstName = hasBoth;  // OK: hasBoth는 string타입의 firstName 포함
let withLastName: WithLastName = hasBoth;  // OK: hasBoth는 string타입의 lastName 포함
```

## 사용 검사
```typescript
type FirstAndLastName = {
  firstName: string;
  lastName: string;
};

// OK
const hasBoth: FirstAndLastName = {
  firstName: "Lionel",
  lastName: "Messi",
};

// Error: Property 'lastName' is missing ...
const hasOnlyOne: FirstAndLastName = {
  firstName: "Naldo",
};
```

## 초과 속성 검사
```typescript
type Poet = {
  born: number;
  name: string;
};

// Error: Type ... is not assignable to type 'Poet' ...
const extraProperty: Poet = {
  activity: "walking",
  born: 1935,
  name: "Mary",
};

// Ok
const extraObject = {
  activity: "walking",
  born: 1935,
  name: "Mary",
};

const extraPropertyButOk: Poet = extraObject;
```
`extraPropertyButOk`는 왜 가능? 초과 속성 검사는 객체 타입으로 선언된 위치에서 생성되는 객체 리터럴에 대해서만 일어나기 때문

## 중첩된 객체 타입
```typescript
type Author = {
  firstName: string;
  lastName: string;
};
type Poem = {
  author: Author;
  name: string;
}
```

## 선택적 옵션
타입의 속성 애너테이션에서 : 앞에 ?를 추가하면 선택적 속성(옵션)으로 사용할 수 있다.
```typescript
type Bookt = {
  author?: string;
  pages: number;
}
```

# 교차 타입
```typescript
type ShortPoem = { author: string } & (
  | { kigo: string; type: "haiku"; }
  | { meter: number; type: "villanelle"; }
);

// OK
const morningGlory: shortPoem = {
  author: "Fukuda Chiyo-ni",
  kigo: "Morning Glory",
  type: "haiku",
};

// Error
const oneArt: shortPoem = {
  author: "Elizabeth",
  type: "villanelle",
};
```

## 교체 타입의 위험성
교체 타입은 유용하지만 컴파일러를 혼동시키는 방식으로 사용되기 쉽다. 교차 타입을 이용할 때에는 가능한 코드를 간결하게 작성하자.

#### 긴 할당 가능성 오류
복잡한 교차 타입을 만들게 되면 타입 검사기의 메시지도 이해하기 어려워진다.

#### never
원시 타입의 값은 동시에 여러 타입이 될 수 없기 때문에 교차 타입의 구성 요소로 함께 결합할 수 없다. 두 개의 원시타입을 함께 시도하면 never 키워드로 표시된다.
```typescript
type NotPossible = number & string;  // type: never
```