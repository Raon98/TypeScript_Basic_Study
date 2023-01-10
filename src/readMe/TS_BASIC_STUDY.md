## TS BASIC STUDY

#### React를 이용한 TypeScript Study
***
- **타입추론**
<br>
 *`TS`는 `TYPE`을 명시해주는 `Script`* 
<br><em>  => Type을 문자열지정후 정수형을 넣을시 오류! </em>
```typescript
    let car:string = 'bmw';
      car = 3; //오류
```
`단! 굳이 명시를 하지않아도 타입이 확실한 경우에는 타입 생략!`
 ```typescript
     let car: string
     car = 'BMW';
 ```
 >이것을 `타입추론`이라 부름!
*** 
- **TS의 일반적인 타입**
1. `Number` | `String` | `Array` | `boolean`
```typescript
 let age:number =30 ; // number형 지정
 let isTrue:boolean = true; // Boolean형 지정
 let a:number[] = [1,2,3] // Number배열
 let a2:Array<number> = [1,2,3] //Array형 Number배열
 let week1:string[] = ['mon','tue','wed'] //String배열
 let week2:Array<string> = ['mon','tue','wed'] //Array형 String배열
```
`String으로 지정후 Number로 넣을시 오류`
```typescript
let week1:string[] = ['mon','tue','wed'] //String배열
 week1.push(3) // Argument of type 'number' is not assignable to parameter of type 'string'.
```
***
2. `tuple`
> `tuple`은 배열과 비슷한 모양! <br><em>= Index별로 서로 다른 타입의 데이터를 넣는 경우에 사용</em>
```typescript
 let b:[string,number];
    <!-- 데이터 대입 -->
    b = ['str',0] //정상
    b = [0 , 'str'] // 오류

    b[0].toLowerCase() //정상
    b[1].toLowerCase() // Number형이기때문에 사용불가X 오류
```
***
3. `void`
> `void는 함수에서 아무 것도 반환하지 않을때 주로 사용`
```typescript
function sayHello():void{
   console.log('hello')
   //return 반환값이 없음
}
```
***
4. `never`
> `에러를 반환하거나 영원히 끝나지 않는 함수의 타입으로 사용`
```typescript
function showError():never{
    throw new Error();
}

function infLoop():never {
    while (true){
        // 무한루프
    }
}
```
***
5 `enum`
> `비슷한 값들끼리 묶어서 숫자 형태로 쓰고싶을 때 사용`
```typescript
#TS
enum Os {
    windos,
    IOS,
    Android
}

#JAVASCIRT
'use strict';
let Os;
 (function (Os){
  Os[Os["window"] = 0] = "window"''
  Os[Os["IOS"] = 1] = "IOS";
  Os[Os["Android"] = 2] ="Android";
 })(Os || (Os = {}))
```
`1. Enum 데이터안에 수동으로 값을 주지않으면 자동으로 0부터 1까지 증가하면서 순서대로 값이 할당`
<br> `2. 수동으로 입력시 상위 아이템에 준 값부터 1씩 증가하면서 값이 할당`
```typescript
enum Os {
    windos = 3,
    IOS = 10, 
    Android
}
    Os[Os["Android"] = 11] = "Android"
```
`3. JS변환된값을 보면 양방향 매핑 되어있음`
```js
 console.log(Os[10]) = "IOS"
 console.log(Os["IOS"]) = 10
``` 
`4. 숫자가 아닌 문자열을 넣을 수도 있다`<br>`  - 양방향매핑X 단반향매핑O` 
```typescript
enum Os {
    windos = 'win',
    IOS = 'ios', 
    Android ='and'
}
```
` 5. Enum Type을 이용해 enum안에 있는 데이터를 사용할 수 있도록 만들어줄 수 있다.`
```typescript
   let myOs:Os;
   myOs = Os.Window
```
` 6. null 과 undefined`
```typescript
 let a:null = null;
 let b:undefined = undefined;
```
***
- **인터페이스**
  <br>
  *`INTERFACE`는 인터페이스 내에 선언된 프로퍼티 혹은 메서드의 구현을 강제하여 `일관성`을 유지할 수 있게 하는 장치*
> 인터페이스 안에 있는 프로퍼티에는 값이 아닌 타입이 들어가게됨
```typescript
   interface User {
      name : string;
      age : number;
  }
  
  let user : User = {
    name : 'xx',
    age : 30
  } 
  console.log(user.age) // 30
```
>`있어도 되고 없어도 되는 프로퍼티의 경우!` => `프로퍼티 이름뒤에 ? 표시`!!
```typescript
   interface User {
    name : string;
    age : number;
    gender? : string
    }
    
    let user : User = {
      name : 'cheol',
      age : 25
    }
    user.age = 26
    user.gender = 'men'

```
>`생성할 때 제외하고는 그 프로퍼티의 내용을 수정 불가능하게 하는 방법 : readonly 속성 부여`!!

```typescript
    interface User {
        name : string;
        age : number;
        readonly birth : string; 
    }

    let user : User = {
     name : 'cheol',
     age : 25,
     birth : '1998'
    }
    user.age = 26
    user.birth = '2000' //오류 

```
### INTERFACE 고급 사용법
```typescript
    interface User {
        name : string;
        age : number;
        gender? : string;
        readonly birthYear : number;
        1? : string;
        2? : string;
        3? : string;
        4? : string;
}
```
`이러한 방법으로 작성할수 있지만 더 스마트하게 작성할 수 있다.`
<br>**key:key속성 : value속성 형태**
```typescript
    interface User {
        name : string;
        age : number;
        gender? : string;
        readonly birthYear : number;
        [grade:number] : string
}

    let user : User = {
        name : 'xx',
        age : 30,
        birthYear : 2000,
        1 : 'A',
        2 : 'B'
    }
```
>이때 문자열로 올 수있는 경우가 너무많기때문에 `TYPE(키워드) [NAME] = 문자열 리턴 타입` 을 설정
```typescript
    type Score = 'A' | 'B' | 'C' | 'D'
    interface User {
        name : string;
        age : number;
        gender? : string;
        readonly birthYear : number;
        [grade:number] : Score
}

    let user : User = {
        name : 'xx',
        age : 30,
        birthYear : 2000,
        1 : 'g', // 오류
        2 : 'B'
    }

```

***
##알고리즘 기초
####var | let | const 차이
#####먼저 변수란 ? 
>변수(variable)는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙이 이름
```javascript
    const myNumber = 23
    // 변수명(식별자): myNumber
    // 해당 값의 위치(메모리 주소): 0012CCGWH80
    // 변수 값(저장된 값): 23
```
변수에 값을 저장하는 것을 `할당(assignment, 대입, 저장)`이라 하며 변수에 저장된 값을 읽어 들이는 것을 `참조(reference)`라 한다. 그리고 변수명을 자바스크립트 엔진에 알리는 것을 `선언(declaration)`이라 한다.`
######변수선언
- 선언 단계: 변수명을 등록하여 자바스크립트 엔진에 변수의 존재를 알린다.
- 초기화 단계: 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화한다.
######변수할당
- 변수 선언과 할당은 하나의 문(statement)으로 단축 표현할 수 있지만, 두 개의 실행 시점이 다르다. 변수 선언이 호이스팅되어 런타임 이전에 실행되지만, 값의 할당은 소스코드가 순차적으로 실행되는 런타임에 실행

여기서 호이스팅이란 ? <br>
> 코드가 실행하기 전 변수선언/함수선언 이 해당 스코프의 최상단으로 끌어 올려진 것 같은 현상

여기서 스코프 란 ?
<br>
`var의 경우는 함수레벨 스코프` <br>
 - `함수 레벨 스코프 란 : 오로지 함수의 코드 블록만을 지역 스코프로 인정`

`let, const의 경우는 블록레벨 스코프` <br>
 - `모두 코드 블록(ex. 함수, if, for, while, try/catch 문 등)을 지역 스코프로 인정`

1. var
    - ES6 이전 사용하던 변수
    - 함수 레벨 스코프
    - 문제점 
      - 변수 중복 선언 가능하여, 예기치 못한 값을 반환할 수 있다.
      - 함수 레벨 스코프로 인해 함수 외부에서 선언한 변수는 모두 전역 변수로 된다.
      - 변수 선언문 이전에 변수를 참조하면 언제나 undefined를 반환

2. let
    - 변수 중복 선언이 불가능하지만, 재할당은 가능하다
   ```javascript
    let name = 'kmj'
    console.log(name) // output: kmj
    
    let name = 'howdy' // output: Uncaught SyntaxError: Identifier 'name' has already been declared 
    name = 'howdy'
    console.log(name) // output: howdy
   ```
   - 블록 레벨 스코프
   - 선언 단계와 초기화 단계가 분리되어 진행 [호이스팅]
     - 런타임 이전에 자바스크립트 엔진에 의해 선언 단계가 먼저 실행되지만, 초기화 단계가 실행되지 않았을 때 해당 변수에 접근하려고 하면 참조 에러
     - 스코프의 시작 지점부터 초기화 단계 시작 지점까지 변수를 참조할 수 없는 일시적 사각지대(Temporal Dead Zone: TDZ) 구간에 존재

3. const
    - 변수 중복 선언X, 재할당 X
    - 반드시 선언과 초기화를 동시에 진행되어야 한다.
    ```javascript
   // 원시값의 재할당
    const name = 'kmj'
    name = 'howdy' // output: Uncaught TypeError: Assignment to constant variable.
    
    // 객체의 재할당
    const name = {
    eng: 'kmj',
    }
    name.eng = 'howdy'
    
    console.log(name) // output: { eng: "howdy" }
   ``` 
   - 블록 레벨 스코프
   - 선언 단계와 초기화 단계가 분리되어 진행 [호이스팅]
     - 선언과 초기화가 동시에 이루어져야 하지만 런타임 이전에는 실행될 수 없다.
***
####화살표함수(Arrow) 와 일반 함수 차이
1. This
   - 일반 함수 <Br> `일반함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되는 것이 아니고,
   함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정된다.`

   - 화살표 함수 <br>
   `화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.
   화살표 함수의 this 언제나 상위 스코프의 this를 가리킨다.(Lexical this)
   또한 call, apply, bind 메소드를 사용하여 this를 변경할 수 없다.`

```javascript
    function fun() {
      this.name = "하이";
      return {
        name: "바이",
        speak: function () {
          console.log(this.name);
        },
      };
    }
    
    function arrFun() {
      this.name = "하이";
      return {
        name: "바이",
        speak: () => {
          console.log(this.name);
        },
      };
    }
    
    const fun1 = new fun();
    fun1.speak(); // 바이
    
    const fun2 = new arrFun();
    fun2.speak(); // 하이
```
>일반 함수는 자신이 종속된 객체를 this로 가리키고 화살표 함수는 자신이 종속된 인스턴스를 가리킨다.

 2. 생성자 함수로 사용 가능 여부
 <br> - 일반 함수는 생성자 함수 O
 <br> - 화살표 함수는 생성자 함수 X
```javascript
    function fun() {
      this.num = 1234;
    }
    const arrFun = () => {
      this.num = 1234;
    };
    
    const funA = new fun();
    console.log(funA.num); // 1234
    
    const funB = new arrFun(); // Error
```
3. arguments 사용 가능 여부 <br>
`arguments란, 함수에 전달되는 인수들을 배열 형태로 나타낸 객체`
    - 일반 함수 에서는 함수가 실행 될때 암묵적으로 arguments 변수가 전달되어 사용할 수 있다.
   ```javascript
    function fun() {
        console.log(arguments); // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    }
            
    fun(1, 2, 3);
   ```
    - 화살표 함수에서는 arguments 변수가 전달되지 않는다.
   ```javascript
   const arrFun = () => {
    console.log(arguments); // Uncaught ReferenceError: arguments is not defined
    };
    
    arrFun(1, 2, 3);
   ```
   

<br>
<br>
<br>

[[참조] : 코딩악마](https://ssocoit.tistory.com/s205?category=974473)
<br>[[참조] : 코딩하는 경제학도](https://ssocoit.tistory.com/207?category=974473)
<br>[[참조] : 혜미의 개발 블로그 ➪ 화살표함수](https://hhyemi.github.io/2021/06/09/arrow.html)
<br>[[참조] : 김민정 블로그 ➪ var/let/const 차이](https://www.howdy-mj.me/javascript/var-let-const) 