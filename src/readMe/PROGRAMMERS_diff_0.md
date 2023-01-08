## 시간날때 푸는 Programmers 
####프로그래머스 최빈값구하기 난이도 0
>최빈값은 주어진 값 중에서 가장 자주 나오는 값을 의미합니다. 정수 배열 array가 매개변수로 주어질 때, 최빈값을 return 하도록 solution 함수를 완성해보세요. 최빈값이 여러 개면 -1을 return 합니다.

>-  입출력 예 #1
> <br> [1, 2, 3, 3, 3, 4]에서 1은 1개 2는 1개 3은 3개 4는 1개로 최빈값은 3입니다.
>-  입출력 예 #2
> <br> [1, 1, 2, 2]에서 1은 2개 2는 2개로 최빈값이 1, 2입니다. 최빈값이 여러 개이므로 -1을 return 합니다.
>-  입출력 예 #3
> <br> [1]에는 1만 있으므로 최빈값은 1입니다.
```javascript
    function solution(array) {
        let m = new Map();
        for (let n of array){
                m.set(n, (m.get(n) || 0)+1);
        }
        
        m = [...m].sort((a,b)=>b[1]-a[1]);
        
        return m.length === 1 || m[0][1] > m[1][1] ? m[0][0] : -1;
    }
```
***
#### 새로알게된 스킬
***
- **result[x] = (result[x] || 0) + 1;**
```javascript
    if(result[x])	{
        result[x] = result[x] + 1;
    }else {
        result[x] = 0 + 1;
    }
 ```
>`대괄호 표기법(square bracket notation)`
>>1. 처음에 배열의 첫번째 값 'a'가 들어오면,result[x], 즉, result.a는 undefined 입니다.
result.a가 undefined이므로 result에 a 속성을 추가하고, 0+1, 즉, 1을 세팅합니다.<br>
>>2. 배열의 두번째 값 'b'가 들어와도 마찬가지로 result에 b 속성을 추가하고, 1을 세팅합니다.<br>
>>3. 배열의 세번째 값 'a'가 들어오면, 이번에는 result.a의 값이 1로 세팅되어 있으므로
result.a의 값을 result.a + 1, 즉, 1+1, 2로 세팅합니다.

[참조 : 네이버블로그](https://hianna.tistory.com/459)

***
**arr.REDUCE 함수**
>arr.reduce((누적값, 현잿값, 인덱스, 요소) => { return 결과 }, 초깃값);
```javascript
array.reduce((acc,cur) => ({ ...acc,
        [cur]: (acc[cur] || 0) + 1
    }), {})
```
> arr.reduce 이용해 배열 만들기 //초기값 배열로설정
```javascript
    result = oneTwoThree.reduce((acc, cur) => {
      acc.push(cur % 2 ? '홀수' : '짝수');
      return acc;
    }, []);
    result; // ['홀수', '짝수', '홀수']

```
***

**왼쪽&오른쪽 시프트 연산자**
> 비트연산자 [ << ,  >> ]
```javascript
    const b5 = 4 << 2;
    console.log(b5); //16
    //4를 2비트 왼쪽으로 이동한다.
    //0000 0100 4
    //0000 1000 8(1비트 이동)
    //0001 0000 16(2비트 이동)
```
