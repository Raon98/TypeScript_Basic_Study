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

<br>
<br>
<br>

[참조 : 코딩악마](https://ssocoit.tistory.com/s205?category=974473)