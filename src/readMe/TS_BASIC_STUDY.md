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
***
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
### 인터페이스로 함수만들기
```typescript
    interface Add {
    (num1:number, num2:number): number;
    }
    
    const add : Add = (x,y) => {
      return x+y;
    }
    add(10,20)
```
### 인터페이스로 클래스 만들기

```typescript
        interface Car {
        color: string;
        wheels: number;
    
        start(): void;
    }

    class Bmw implements Car {
        color = 'red';
        wheels = 4;
    
        start() {
            console.log('go!')
        }
    
        // 생성자 함수도 동일하지만 인터페이스에 선언한 프로퍼티들은 다들어가야됨
        constructor(c:string) {
            this.color = c
        }
    }
    
    const b = new Bmw('green')
    console.log(b)
```
### 인터페이스의 확장
```typescript
    interface Car {
        color: string;
        wheels: number;
        start(): void;
    }
    interface price {
        money : number
    }
    interface Benz extends Car , price {  //,로 여러개 상속도 가능
        stop(): void;
        door: number;
    }
    
    const banz : Benz = {
        door : 5,
        stop() {
            console.log('Stop!')
        }
    } // 오류 : 인터페이스 Car의 선언된 프로퍼티들도 다 정의해야됨
```
- **함수**

0.1 기본 사용법
    - TypeScript에서 함수는 Type 지정말고는 동일

```typescript
    function add (num1:number, num2:number) : void {
        console.log(num1 + num2)
    }
    //리턴할 값이 없으면 void 사용
```

0.2  Optional Parameter
 - 인터페이스와 동일하게 ?(Optional Parameter)를 이용해서 __선택적__ 으로 매개변수를 받을 수 있다.
```typescript
    // 기본형
    function hello(name? : string){
        return `Hello, ${name || 'world'}`;
    }
    const result1 = hello(); // hello world
    const result2 = hello('Missa') // hello Missa
    const result3 = hello(123) // 오류
    
    //미리지정을 해줘도됨
    function hello2(name = "world"){
        return `Hello ${name}`;
    }
```
  Optional Parameter를 사용할 시 주의할점!
  `해당 매개변수는 필수 매개변수 뒷편으로 해놔야됨 - 그렇지않으면 1개만 받았을때 어느 매개변수인지 알지 못함`

```typescript
    //오류
    function hello(age?:number,name:string):string{
        if(name !== undefined){
            return `hello ${name}. You age ${age}`
        }
    }
    //대체법
    function hello(age :number | undefined ,name:string):string{
        if(name !== undefined){
            return `hello ${name}. You age ${age}`
        }
    }
```
0.3  전개 구문
```typescript
    function add(...num: number[]) {
        return num.reduce((result,num) => result + num,0)
    }
    add(1,2,3) // 6
```

1. 인터페이스와 함수
```typescript
    interface User {
        name : string
    }
    const Sam: User = {name : 'Sam'}

    function showName() {
        console.log(this.name); //  this가 어떤 타입인지 알수없기 떄문에 밀줄
    }
    const a = showName().bind(Sam);
    a();
```
this의 타입을 정의해주기 위해서는 `첫 번쨰 매개변수로 this의 타입을 정의`해주면된다.
```typescript
    function showName(this:User) {
        console.log(this.name); //  this가 어떤 타입인지 알수없기 떄문에 밀줄
    }
```
만약 다른 매개변수를 받더라도 맨앞에 this를 정의 할 수도있다.
매개변수를 받더라도 this가 아닌 그 다음 요소가 받아진다.
```typescript
    function showName(this:User, age:number, gender:'m'|'f') {
        console.log(this.name ,age , gender); //  this가 어떤 타입인지 알수없기 떄문에 밀줄
    }
```
1.0 함수 오버로딩
- 매개변수로 number 타입을 요소로 받는지, String 타입을 요소로 받는지에따라 다른 결과값 반환

##### TYPESCRIPT는 함수가 작동하기 전부터 발생할 수 있는 에러를 체크할수있다는 장점
```typescript
    interface User {
        name: string;
        age: number;
    }
    
    function join(name:string,age: string) : string 
    function join(name:string, age:number) : User

    function join(name: string, age: number | string): User | string {
        if(typeof age === "number"){
            return {
                name,
                age
            };
        }else{
            return "나이는 숫자로 입력해주세요!"
        }
    }
    const sam: User  =join('Sam',30);
    const jong: String = join('jong','20');
```
위 처럼 리턴 타입을 정확히 명시 해줘야 오류메세지 X


<br> 
<br>
<br>

[[참조] : 코딩악마](https://ssocoit.tistory.com/s205?category=974473) 