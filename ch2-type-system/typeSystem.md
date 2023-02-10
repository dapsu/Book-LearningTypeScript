# 타입의 종류

## 원시 타입
> 타입스크립트의 가장 기본적인 타입은 자바스크립트와 동일
```
- null
- undefined
- boolean
- string
- number
- bigint
- symbol
```

- 자바스크립트에서의 Boolean, Number와 같은 객체는 원싯값을 감싸는 객채
- 반면에 타입스크립트에서는 boolean, number처럼 소문자로 참조하는 것이 모범 사례

## 타입 시스템
타입스크립트의 타입 시스템은 다음과 같이 작동
1. 코드를 읽고 존재하는 모든 타입과 값을 이해한다.
2. 각 값이 초기 선언에서 가질 수 있는 타입을 확인한다.
3. 각 값이 추후 코드에서 어떻게 사용될 수 있는지 모든 방법을 확인한다.
4. 값의 사용법이 타입과 일치하지 않으면 사용자에게 오류를 표시한다.

## 오류 종류
- 구문 오류: 타입스크립트가 자바스크립트로 변환되는 것을 차단
- 타입 오류: 타입 검사기에 따라 일치하지 않는 것 감지

# 할당 가능성
> 타입스크립트에서 함수 호출이나 변수에 값을 제공할 수 있는지 여부를 확인하는 것을 할당 가능성이라고 한다.

```typescript
let myName = "dapsu";
myName = "hansomeBoy"; // --> 쌉가능
```

```typescript
let myName = "dapsu";
myName = false;
// Error: type 'boolean' is not assignable to type 'string'.
```

# 타입 애너테이션
초기 타입을 유추할 수 없는 변수는 **진화하는 any**라고 부른다. 
```typescript
let dapsu;  // type: any
dapsu = "handsomeBoy";  // type: string
dapsu.toUpperCase();  // 쌉가능

dapsu = 31;  // type: number
dapsu.toUpperCase();  // Error. 타입 number임 ㅅㄱ
```

위 예시로 보면 진화하는 any변수인 dapsu에 처음에는 문자열이 할당되는데, 그 다음에 number로 진화되는 것을 확인할 수 있다.
하지만 이런 방식의 any타입으로 진화하는 것을 허용하게 되면 타입스크립트의 타입 검사 목적이 쓸모 없어진다.

타입스크립트는 초깃값을 할당하지 않고도 변수의 타입을 선언할 수 있는 구문인 **타입 애너테이션**을 제공한다. 타입 애너테이션은 타입스크립트에만 존재하며 런타임 코드에 영향을 주지 않는다.
```typescript
let dapsu: string;
dapsu = "hansomeBoy";

// 출련된 js파일
let dapsu;
dapsu = "hansomeBoy";

// 불필요한 타입 애너테이션
let dapsu: string = "hansomeBoy";
```

