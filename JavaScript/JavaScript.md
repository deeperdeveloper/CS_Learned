# 제대로 파는 자바 스크립트(JavaScript) - by 얄코

## 섹션 0. 인트로

html,css : 마크업 언어

* 뭘 배치하는 것밖에 못함.
  * 배치한 요소가 어떠한 동작을 하게끔 하려면, javascript를 활용해야 한다.



* 인터프리터 언어
  * 컴파일을 거치지 않음
* 동적 규칙
  * 자바 스크립트는 변수의 타입을 엄격하게 제어하지 않는다.
    * 이를 보완한 언어가 "타입스크립트"



Node.js

* 자바스크립트를 런타임 환경에서 실행하도록 하는 프로그램



## 섹션1. 자바스크립트의 기본적인 사용

### 콘솔 활용하기

//브라우저마다도 콘솔을 구현하는 방식이 다르다.

콘솔은, 사용자가 아니라 개발자를 위한 기능

=> 따라서, 사용자가 콘솔 창을 직접 열어보지 않는 이상, 콘솔에 어떤 명령어가 입력되었는지 잘 모른다.

=> 콘솔은, 소프트웨어 외적으로 영향을 미치지 않는다. 



종류

* console.log
* console.info
* console.warn
* console.error



### 주석과 세미콜론

좋은 코드는 주석을 많이 달지 않아도 알아볼 수 있어야 한다.



### 변수와 상수 - 데이터를 담는 주머니

** 요즘에는 var를 쓰지 않고, let과 const를 사용한다고 한다.



변수 variable

* let 사용

  * `let x;` 선언 시 메모리에서의 현상

  * `x=1` => undefined를 가리키는 주소값을, 1을 가리키는 주소값으로 바뀜

  * `let x = 1;` => 역시 위처럼, undefined를 먼저 가리킨 후, 1을 가리키는 주소값으로 바뀜.  (위의 2단계 매커니즘이 일어나는 것은 변함이 없다.)

  * ```javascript
    let x = 1;
    let y = x; //x가 가진 주소값을 y도 동일하게 가지게 된다.
    x=2; //x=2, y=1이다. 즉, 2가 데이터 영역에 새로 할당되며, x가 가리키는 주소값이 바뀌게 된다.
    ```

  * 위에서, 1이라는 같은 값을 x와 y가 가리킨다면, 데이터 영역에서 1이 두 곳에 존재하는 것이 아니다. 

    => 1은 데이터 영역 한 곳에서만 존재하며, x와 y는 같은 1을 가리킨다!

  * JavaScript는 자료형에 따라 할당되는 데이터 영역의 크기가 다르기 때문에,  어떠한 변수에 할당된 자료형이 달라진다면, 메모리상 가리키는 위치가 변경되는 방식으로 이루어진다.

    예) x=1 -> x= "Hello" 라면, x가 가리키는 데이터 영역의 메모리 주소가 달라진다.

  * x에다가 데이터를 재할당하는 것은 가능하지만, x를 다시 재선언하는 것은 불가능하다.

    * var의 경우는 위의 경우가 가능했었다. (=체계가 개판)

상수 const

* const 사용
  * 선언과 초기화가 동시에 일어나야 한다.
    * 선언만 먼저한 후, 초기화를 나중에 하는 것이 불가능하다.
  * 초기화 후, 값을 변경하지 못 한다.
    * 따라서, 값이 바뀔 일이 없는 데이터는 "상수"로 선언할 것.



여러 변수와 상수를 동시에 선언



//예외적으로, 브라우저 콘솔에서는 아래의 문법이 허용된다.

```javascript
let x=1;
let x=2; 
//엔터 (위 부분 허용x)


let x=1;
//엔터
let x=2;
//엔터

//(위 부분은 허용됨)

let x=1;
const x=2;
//엔터 (위 부분 허용x)
```



## 섹션2. 자료형과 연산자

### 자료형 - 데이터의 종류

typeof x => x의 자료형을 판단할 때 쓰임.

typeof x => 결국, 반환값 ('string', 'boolean', 'number') 은 String 형식이다.

* undefined 역시, "값이 부여되지 않은 상태" 를 나타냄

  => 뭔지 모를 값이 있음을 나타냄.

  => 엄연히 값이다!

  * 그리고, undefined는, 아무것도 반환하지 않은 구문에 대해서도 값으로서 나온다

    ```javascript
    //아래의 코드를 콘솔에 치게 되면, undefined를 반환받는다.
    let x = 1;
    ```

    

* null은, "값이 비어있음" 을 명시적으로 나타내는 "값" 이다.

  * Object 타입
    * 설계가 잘못되어서 null이 Object형의 결과가 됨. 그러나, 이를 못 고치고 있다.
    * 웹사이트에 사용된 언어가 있다보니, 묵시하고 넘어감.
    * 따라서, 그냥 객체와 null은 typeof로 구분이 불가능하다.
      * ===을 활용해서 비교할 예정

* 그 외 자료형
  * 숫자형은 정수와 실수의 구분이 없다.



undefined, null 구분 방법

* null은 주로 아래의 경우에 사용
  * 곧 들어올 객체의 자리임을 나타내거나
  * 반환이 잘못되서 객체 생성이 실패할 때 null을 반환



### 자료형과 정적, 동적 타입

** 정적 타입, 동적 타입

정작 타입의 경우, 컴파일 시점에 자료형이 정해져서 고정된다.

동적 타입은, 실행될 때 자료형을 해석한다.

* 따라서, 런타임시에 자료형 관련 오류에 취약하다.

  * 자바 같은 컴파일 언어는, 런타임 단계 전 컴파일 단계에서 자료형 관련 오류가 걸러진다

  * 반면, javaScript 와 같은 인터프리터 언어는, 런타임 단계가 되어서야 자료형 관련 오류를 알 수 있게 된다.

  * 예) 매개변수를 문자열로 받아, 대문자로 바꾸어 반환하는 함수 를 생각해보자

    => 매개변수를 숫자로 준다면, 해당 경우는 오류가 발생한다.

    => 자바의 경우, 컴파일 시점에서 바로 발견 가능하지만, JavaScript의 경우는 실행단계가 되어서야 발견이 가능하다.

  * ```javascript
    // 주어진 문자열을 대문자로 바꾸는 함수
    // 다른 자료형에 대한 예외처리 없음
    function getUpperCase(str) {
      return str.toUpperCase();
    }
    
    console.log(getUpperCase('hello'));
    
    // ⚠️ 오류 발생!
    console.log(getUpperCase(1));
    ```

    



### 문자열(string) - 텍스트 데이터

따옴표가 등장하면, 텍스트가 끝났다고 인식하므로, 이를 방지하려면 이스케이프 표현으로 처리해주면 된다.

```javascript
// ⭐️ 이스케이프 표현(escape sequence)
let word1 = '작은따옴표 안에 \'작은따옴표\' 사용';
let word2 = "큰따옴표 안에 \"큰따옴표\" 사용";
console.log(word1, word2);
```



* 이스케이프 표현

=> 긴 문자열을 소스코드 상에서, 잘라서 표현하되 실제 출력되는 결과물은 1줄로 나오게끔 할 수 있다.



* 백틱 표현으로도 쓸 수 있다.

=> 백틱 표현 내부에서는, 어떤 변수를 받아서 마치 하나의 문자열처럼 코드를 작성하는 것이 가능해진다.  

```javascript
const NAME = '홍길동';
let age = 20;
let married = false;

console.log(
`제 이름은 ${NAME}, 나이는 ${age}세구요, \
${married ? '기혼' : '미혼'}입니다.`
);

//백틱 표현을 쓰지 않으면 아래와 같이 써야 한다.
console.log('제 이름은 ' + NAME + ', 나이는 ' + age + '세구요, ' + (married ? '기혼':'미혼') + '입니다.');
```



### 문자열에 사용되는 연산자

== 과 === 의 차이를 보자

* 자바스크립트는, 암묵적으로 타입을 변환한다

  ```javascript
  '1' == 1 //true
  // 암묵적으로 문자를 숫자로 변환해서 비교한다.
  
  '1' === 1 //false
  // 값과 자료형까지 비교함
  ```

* 컴퓨터에서, 대문자는 소문자보다 앞에 온다.

  * 이를 확인할 수 있는 가장 직관적인 예는, 아래의 코드이다.

    ```
    console.log('ABC' < 'abc'); //true
    ```

    



문자열과 숫자를 같이 사용시, 문자열을 숫자로 변환해서 비교한다.

=> 그러나, 문자열과 숫자와 또 제3의 자료형(boolean 등)을 활용시, 모두 String으로 변환된다.

```javascript
//문자열과 숫자를 함께 활용한 경우
console.log('100' > 12); //true
console.log('100' > '12'); //false
console.log('100' + 12); //10012
```



```javascript
//문자열과 숫자, 그리고 제3의 자료형을 사용한 경우
let result = '안녕' + 1 + true;

console.log(result); //안녕1true
console.log(typeof result); //String

result += null;
result += undefined;

console.log(result); //안녕1truenullundefined
console.log(typeof result); //string
```



### 숫자와 관련 연산자

* 정수와 실수를 별도의 자료형으로 구분하지 않는다

* Infinity 또한 number 자료형이며, Infinity 자체가 예약어이기도 하다.

  * ```javascript
    let x = 1/0;
    console.log(x, typeof x); //Infinity, Number
    
    let z = Infinity;
    console.log(z, typeof z); //Infinity를 직접 할당해도 가능.
    ```

* NaN 또한 number 자료형이며, Not a number의 약자 (숫자가 아닌 값이 연산에 들어왔다는 의미)

  * 어떤 변수의 값이 NaN인지 판단하려면, == 이나 === 로는 불가능하며, 아래의 방법을 활용해야 한다.

    * boolean 타입은 숫자로 변환이 된다. 

    * isNaN() => 변환하기 전 숫자가 아니며, 변환 이후에도 숫자가 아니다 싶으면 true를 반환

      * (내가 따져보니, NaN의 정의에 입각하여, 매개변수의 식에서 숫자가 아닌 값이 피연산자로 들어 있다면, 값 자체가 NaN이 아니더라도 true를 반환한다고 이해하는게 제일 정확할 듯.)

    * Number.isNaN() => 숫자 자료형이면서, 숫자가 아니다 싶으면 true를 반환

      * NaN은 숫자 자료형이지만, 숫자가 아니므로 true를 반환
      * (나의 생각) 이외에는, 위의 isNaN()의 정의와 유사하다고 봄.
      * *<!--** isNaN() 과 Number.isNaN()은 지금은 100% 이해가 되지는 않지만, 추후 실전에서 맞닥뜨리면서 보완해보기-->*

    * ```javascript
      let x = 1 / 'abc';  //NaN
      
      console.log(
        x, 
        x == NaN, //false
        x === NaN, //false
        isNaN(x), // 숫자가 아닐 시 true
        Number.isNaN(x) // 보다 엄격한 버전 
      );
      ```

    * ```javascript
      //isNaN() 과 Number.isNaN() 의 차이
      
      console.log(
        typeof 'a', isNaN('a'), Number.isNaN('a')
      ); // string, true, false ⚠️ 특정 숫자로 변환 불가인 문자의 경우 차이 => 'a'는 변환했을 때에도 숫자 자료형이 아니므로, 'a'가 NaN임에도 불구하고 Number.isNaN('a')가 false를 반환한다.
      ```

    * ```javascript
      console.log(
        typeof '1', isNaN('1'), Number.isNaN('1')
      ); // string, false, false => 특정 숫자로 변환 가능한 문자
      
      console.log(
        typeof true, isNaN(true), Number.isNaN(true)
      ); // boolean, false, false => true는 1, false는 0으로 변환됨
      ```

    * ```JAVASCRIPT
      // 1/'a' 는 값 자체가 NaN이므로, 모두 true를 반환한다.
      // NaN 역시 숫자형임에 염두에 두면, Number.isNaN()의 메서드의 정의에 어긋나지 않는 결과를 가져옴을 알 수 있다.
      
      console.log(
        typeof (1/'a'), isNaN(1/'a'), Number.isNaN(1/'a')
      ); // NaN, true, true => NaN값인 경우
      ```

* 문자열을 숫자로 바꾸려면, 문자열 앞에 "+" 나"-"를 붙인다.

* 그 외

  * ```javascript
    let y = 25;
    
    console.log(
      y **= 0.5, // 할당된 결과 반환
      y
    );
    
    // 5,5 가 출력된다.
    ```

  * ```javascript
    let x = '100';
    console.log(x++, x);
    //100, 101
    
    // 숫자로 변환될 수 없는 문자열
    // 첫 번째 값 주의 - 증가 이전에도 변환
    let z = 'abc';
    console.log(z++, z);
    //NaN, NaN 이 출력된다.
    ```



### 부동소수점과 관련 연산자

** number 자료형은 부동소수점이다. 실제 정수형은 아니다.

* 예) int 자료형(자바, 파이썬의 경우)

  * 32자리의 bit를 활용하며, 맨 앞 1자리 bit는 양수/음수를 나타내며, 나머지 31개의 bit로 수를 표현하며, 아래의 범위의 수를 표현 가능하다.
    $$
    -2^{31} \sim 2^{31} -1
    $$

* 소수의 경우

  * 예1) 9.625 => 1001.101₂ 로 표현이 가능하다.

  * 위의 소수를 고정 소숫점, 부동 소숫점 표현 방식으로 표현하자

    * 고정 소숫점

      * 말 그대로 32bit의 수를 "고정된 크기의" 정수 부분과 "고정된 크기의" 소수 부분으로 나눈다.

      * 맨 앞의 1bit => 부호 / 이후 15bit => 정수 부분 / 나머지 16bit => 소수 부분을 나타내게끔 하면 된다.

      * 위의 경우, 1 0000000 00001001 10100000 00000000 로 표현이 가능하다.

        => 그러나,  소숫점이 고정되어 있으므로 표현할 수 있는 수의 최댓값에 대한 한계가 존재하며, 정밀도 또한 높지 않다는 한계가 존재.

    * 부동 소숫점

      * 말 그대로, 소숫점을 움직여서 32bit의 수를 "유동적인 크기의" 정수 부분과 "유동적인 크기의" 소수 부분으로 나눈다.

        * 이를 위해, 어떤 소수를 2진수로 나타낸 후, 소숫점을 움직여서 정수 부분을 무조건 1로 만들어야 한다. 
        * 그리고, 움직인 소숫점의 칸 수를 기록한다.

      * 맨 앞의 1bit => 부호 / 이후 지수부 8bit / 나머지 가수부 23bit를 활용한다.

        * 지수부 8bit는, 소숫점을 n칸 움직일 필요가 있을 때, n과 127을 연산하여 나타내는 숫자이다.

          예)  소숫점을 3칸 왼쪽으로 움직일 때, 127 + 3 = 130을 위의 7bit에 할당한다.

          => 9.625의 경우, 1001.101₂ 로 나타내어 지며, 부동 소숫점 방식에 따라서, 소숫점을 왼쪽 3칸으로 움직이는 것이 필요하다

          => 따라서, 0 1000001 0/0011010 00000000 00000000 으로 나타내어 질 수 있다. (/이전까지의 수는, 130을 나타낸다.)

      * 이러한 원리를 64bit에 적용하며, 표준화한 방식을 "IEEE 754" 표준 방식이라고 하며, 다른 프로그래밍 언어(JAVA 등)에도 이러한 방식이 적용된다

        => 64bit인 경우, 자료형은 double형을 사용한다.



### 불리언(boolean)과 관련 연산자

```javascript
let x = true;
// x = false;

// ⭐️ &&, || 연산자는 값 자체를 반환
// &&나 || 연산을 통해 true, false 여부를 판별이 가능하면, 연산을 멈추고 현재 연산 대상인 데이터를 반환한다.
let y = x && 'abc';
let z = x || 123;

console.log(y, z);

//abc, true 가 출력된다.
```

=> 'abc'와 123은 true와 같이 인식되기 때문에, 위와 같이 출력이 된다. (truthy)

(&&나 ||는 값 자체를 반환한다.)



truthy => true로 평가되는 값들이지, true와 같다는 의미는 아니다. 

falsy => false로 평가되는 값들이지, false와 같다는 의미는 아니다. (다만, 몇몇 경우는false로 타입변환되기도 한다. - 자바스크립트의 종잡을 수 없는 특성 중 하나)

=> 0과 ''는, false로 타입변환됨을 아래의 결과를 통해 알 수 있다.

```javascript
//아래의 경우는, 모두 true를 반환
console.log(
  1.23 ? true : false,
  -999 ? true: false,
  '0' ? true : false,
  ' ' ? true : false,
  Infinity ? true : false,
  -Infinity ? true : false,
  {} ? true : false,
  [] ? true : false,
);

//위의 삼항 연산자 중, 조건문에 해당하는 데이터는 truthy일 뿐, true로 변환되지 않음을 보여준다. (모든 결과가 false)
// ⚠️ true와 `같다`는 의미는 아님
console.log(
  1.23 == true,
  ' ' == true,
  {} == true
);

//아래의 경우는 모두 false로 변환
console.log(
  0 ? true : false,
  -0 ? true : false,
  '' ? true : false,
  null ? true : false,
  undefined ? true : false,
  NaN ? true : false,
);

//위 값들은 모두 falsy이지만, 일부 데이터(0, '')는 false로 변환되기도 한다. (JavaScript의 특성)
// 💡 어떤 값들은 false로 타입변환됨
console.log(
  0 == false, //true
  0 === false, //false
  '' == false, //true
  '' === false //false
);

console.log(
  null == false, //false
  undefined == false, //false
  NaN == false, //false
);


```



어떤 자료형에 !를 붙이게 되면, 해당 자료형이 의미하는 boolean의 반대 의미로 변환되어 출력된다. 

(따라서, !!를 붙이면, 원래의 자료형이 의미하는 boolean으로 변환된다.)

```javascript
// 한 번 부정 (결과값은 boolean 값이다.)
console.log(
  !1, !-999, !'hello',
  !0, !'', !null
);
```

```javascript
// ⭐️ 두 번 부정하여 해당 boolean값으로
console.log(
  !!1, !!-999, !!'hello',
  !!0, !!'', !!null
);
```



### 연산자 마무리

?? 병합 연산자

* null과 undefined을 대체할 때 사용하는 연산자
  * 즉, || 연산자보다 엄격하게 적용됨을 알 수 있다.
  * 예를 들어, let x = a || b에서, a의 값이 falsy이면 (즉, null 또는 undefined 이외에 0이나 '' 등) b의 값을 x에 할당하는 방식보다 엄격하다고 할 수 있다.

```javascript
let a = false;
let b = 0;
let c = '';
let d = null;
let e;

//false, 0, '', 기본값, 기본값
console.log(
  a ?? '기본값',
  b ?? '기본값',
  c ?? '기본값',
  d ?? '기본값',
  e ?? '기본값',
);

//기본값, 기본값, 기본값, 기본값, 기본값
console.log(
  a || '기본값',
  b || '기본값',
  c || '기본값',
  d || '기본값',
  e || '기본값',
);


let baby1 = '홍길동';
let baby2; // 아직 이름을 짓지 못함

const nameTag1 = baby1 ?? '1번 아기';
const nameTag2 = baby2 ?? '2번 아기';

console.log(nameTag1, nameTag2); //홍길동, 2번 아기
//nameTag2의 경우, baby2 변수의 데이터가 undefined이기 때문에, ?? 연산자의에 의해 '2번 아기' 로 대체가 되었다 
```



병합 할당 연산자들 예시

```javascript
let x = 0;
let y = '';
let z = null;

x ||= 100;
y &&= '있어야 바뀜';
z ??= '기본값';

console.log(x, y, z); //100, '', 기본값
```



 쉼표 연산자

```javascript
let x = 1, y = 2, z = 3;
console.log(x, y, z);

// 마지막으로 실행한 것 반환
//12가 반환된다.
console.log(
  (++x, y += x, z *= y)
);

//아래의 결과는 2,4,12가 반환된다.
let x = 1, y = 2, z = 3;
console.log(x, y, z);

// 마지막으로 실행한 것 반환
//12가 반환된다.
console.log(
  (++x, y += x, z *= y)
);
```



### 객체와 배열 미리 보기

원시타입이 아닌 모든 데이터는 근본적으로 "객체"



객체의 정의

* 복합적인 정보를, 프로퍼티로 저장하는 자료형

  * 즉, key-value 조합으로 저장하는 자료형이다.

    ```javascript
    const person1 = {
      name: '김철수',
      age: 25,
      married: false
    };
    
    console.log(typeof person1); // object
    console.log(person1); // {name: '김철수', age: 25, married: false}
    ```

    

* const로 선언한 객체 역시, 프로퍼티를 수정할 수는 있다.

  * 왜냐하면, 프로퍼티를 수정하더라도, 결국 객체의 메모리 주소는 동일하기 때문이다.
    * (내 생각 - 확인 요망) 정확히는, 객체의 메모리 시작 주소를 저장하기 때문에(이 사실을 확인해야 함), 객체에 프로퍼티를 추가하는 것 역시 가능한 것 같다.

  * 다만, 아예 새로운 객체로 재선언은 불가.

* 특정 키가 객체에 포함되어있는지 확인할 수 있다.

  * 해당 키가 존재하지 않으면, undefined를 반환한다.

```javascript
const person1 = {
  name: '김철수',
  age: 25,
  married: false
};

//김철수, 25, false
console.log(
  person1.name,
  person1.age,
  person1.married
);

//위의 log의 결과물과 완전히 일치한다. (김철수, 25, false)
//아래의 프로퍼티 접근법은, key가 숫자일 때에도 가능하다.
console.log(
  person1['name'], // 속성명을 string으로
  person1['age'],
  person1['married'],
);

//아래의 결과물은 undefined가 출력된다.
console.log(person1.birthdate);
console.log(person1['job']);

// 특정 프로퍼티의 값 변경
person1.age = 26;
person1['married'] = true

console.log(person1);

//프로퍼티 값 수정
// 특정 프로퍼티의 값 변경
person1.age = 26;
person1['married'] = true

console.log(person1);

// 새 프로퍼티 추가
person1.job = 'developer';
person1['bloodtype'] = 'AB'

//{name: '김철수', age: 26, married: true, job: 'developer', bloodtype: 'AB'}
console.log(person1);
```





배열의 정의

* 객체의 일종이다
  * length 프로퍼티와, index 프로퍼티로 이루어져 있는 특수한 객체이다.
    * 따라서, index 프로퍼티로 접근한 값 역시 원칙적으로 모든 자료형이 가능하므로, 배열 내부에는 각기 다른 자료형의 요소로 선언이 가능한 것이다.

  * 키가 숫자로 되어있다면, winners.0이 아닌, winners[0] 으로 접근한다.
    * 왜냐하면, 식별자 규칙에 어긋나는 키이기 때문.

* 역시, const로 선언한 배열도, 아예 다른 배열로 재선언하는 것은 불가능
  * 그러나, 해당 배열 내부의 특정 요소를 수정하거나, 추가하는 것은 가능
* 배열 범주 너머로 접근 시 undefined 반환
  * (내 생각) 이는 추후, 배열의 길이를 늘렸을 때 메모리 할당이 가능함을 나타내기 위해서 null이나 empty가 아닌 undefined가 반환된다고 생각함!

* 일반적인 프로그래밍 언어에서의 배열의 정의와는 달리, HashTable로 구현되어 있으며 이로 인해 탐색, 추가, 삭제 등에서 일반적인 의미의 배열과 성능 차이가 발생한다.

```javascript
const winners = [12, 592, 7, 48];
const weekdays = ['월', '화', '수', '목', '금', '토', '일'];

// 자료형에 관계없이 한 배열에 넣을 수 있음
const randoms = ['홍길동', -24, true, null, undefined];

console.log(typeof winners); //object
console.log(winners, weekdays, randoms); //12, '일', null
```

```javascript
const numbers = [1, 2, 3];

// 특정 위치의 값 수정
numbers[2] = 5;

console.log(numbers); //[1,2,5]

// 맨 끝에 값 추가
numbers.push(10);

console.log(numbers); //[1,2,5,10]

//배열의 범주를 넘어서면 undefined를 반환
const winners = [12, 592, 7, 48];
console.log(winners[winners.length]); //undefined

//배열은 모든 자료형을 요소로 가질 수 있으므로, 아래의 형태 또한 허용된다.
const groups = [[1, 2], [3, 4, 5], [6, 7, 8, 9]];

const weapons = [
  { name: '롱소드', damage: 30, design: ['화룡검', '뇌신검'] },
  { name: '활', damage: 12 },
  { name: '워해머', damage: 48 },
];

console.log(groups[1][2]);
console.log(weapons[2].damage);
console.log(weapons[0].design[0]);

//객체 내부에 value의 자료형으로서 배열, 객체로 오는 것도 가능하다.
const person2 = {
  name: '김달순',
  age: 23,
  languages: ['Korean', 'English', 'French'],
  education: {
    school: '한국대',
    major: ['컴퓨터공학', '전자공학'],
    graduated: true,
  }
};

console.log(person2.languages[2]);
console.log(person2.education.graduated);
```





<u>** 생각해 볼 사안</u>

* <u>일반 프로그래밍 언어에서의 배열의 정의와 javaScript에서의 배열의 정의 차이</u>
* <u>배열을 추가할 때에도</u> 
* <u>undefined가 언제 반환되는지, 그리고 null과 empty와의 차이점.</u>



### 원시 타입 vs 참조 타입

primitive 타입은, 값에 의한 복사이다. (copy by value)

=> 따라서, 데이터 영역에는 값 그 자체가 저장되며, 사용자가 특정 변수의 값을 바꿀 때, 데이터 영역의 다른 곳에 바꾼 값이 할당되며 해당 데이터를 가리키게 된다.

```javascript
let number1 = 1;
let string1 = 'ABC';
let bool1 = true;

let number2 = number1; //number2에도 1이 저장이 되나, number1에 할당된 값을 2로 바꾼다고 해서 number2가 영향을 받지는 않는다.
let string2 = string1;
let bool2 = bool1;

number2 = 2;
string2 = '가나다';
bool2 = false;

console.log('~1:', number1, string1, bool1); //1, ABC, true
console.log('~2:', number2, string2, bool2); //2, 가나다, false
```



반면 reference 타입은, 데이터 영역에 주소값을 저장한다.

=> 해당 주소값에 해당하는 객체의 각 요소는, "힙 영역"에 저장된다.

=> 각 요소에 해당하는 실제 데이터(primitive type이라고 가정)은 "데이터 영역"에 저장된다.

(만약 실제 데이터가 reference type이라고 하면, 데이터 영역에는 주소값이 저장될 것이며 위의 메커니즘과 동일할 것이다.)

```javascript
const obj1 = {
  num: 1, str: 'ABC', bool: true
};
const obj2 = obj1;
// obj2 = {}; // ⚠️ 오류

console.log('obj1:', obj1); // {num: 1, str: 'ABC', bool: true}
console.log('obj2:', obj2); // {num: 1, str: 'ABC', bool: true}

// ⭐️ const임에도 내부 값은 변경 가능함 주목
// 내부 변경 방지는 이후 배울 Object.freeze 함수로
obj2.num = 2;
obj2.str = '가나다';
obj2.bool = false;

console.log('obj1:', obj1); // {num: 2, str: '가나다', bool: false}
console.log('obj2:', obj2); // {num: 2, str: '가나다', bool: false}
```



<u>의문) 힙 영역에서의, "각 요소의 변수들은", 변수 영역에 저장되는 것이 아니라, 별도의 영역(힙 영역)에 저장된다고 보는 것이 맞는지?</u>



## 섹션3. 제어문

### 블록문과 스코프

블록 내부 또다른 블록에서, 동명의 변수를 선언할 수 있다.

=> 선언해서 사용 시, 해당 변수가 우선적으로 적용됨

(또한, 블록 바깥의 변수의 값을 바꾸는 역할 또한 할 수 있음)

```javascript
{
  const x = 'Hello';
  let y = 'world!';
  console.log(x, y);
}

//아래의 결과는 에러가 발생
console.log(x);
console.log(y);

const xx = 0;
let yy = 'Hello!';
let zz = 300;
console.log(xx, yy, zz); //0, 'Hello!', 300

{
  const xx = 1; // 💡 블록 안에서는 바깥의 const 재선언 가능
  let yy = '안녕하세요~';
  zz = 400;	
    
  console.log(xx, yy, zz); //1, '안녕하세요~', 400
  // ⚠️ const, let을 빼먹으면 재선언이 아니라 바깥것의 값을(변수면) 바꿈!
}

//블록을 벗어났으므로, xx와 yy는 원래 블록 바깥에 정의된 값을 갖게 된다.
// => 이를 scope chain이라고 한다.
console.log(xx, yy, zz); //0, 'Hello', 400
```



스코프 체인과 메모리에서의 관점

```javascript
//스코프 체인 예시
let a = 0;
let b = 1;
let c = 2;
console.log('시점 1:', a, b, c);

{
  let a = 'A';
  let b = 'B'
  console.log('시점 2:', a, b, c);

  {
    let a = '가'
    console.log('시점 3:', a, b, c);
  }

  console.log('시점 4:', a, b, c);
}

console.log('시점 5:', a, b, c);
```

위 현상을 메모리에서 풀어보자면, 전역 변수(데이터 영역)과 지역 변수(스택 영역)의 관점으로 바라볼 수 있게 된다.

* 동일한 변수가 데이터 영역과 스택 영역에 동시에 선언이 된다면, (해당 스코프 내라면) 스택 영역 내의 변수가 우선적으로 활용된다

* 되도록이면, 스택 영역에 변수와 상수를 선언해서 메모리를 절약하는 것이 권장된다.



### if/else

if ~ else 형식으로 특정 조건에 맞는 데이터면 그에 따른 코드가 적용되도록 작성할 수 있다

=> return을 사용해도 된다.

```javascript
// if~else 문 예시
const x = 22;

if (x % 4) {
  if (x % 2) {
    console.log('홀수입니다.');
  } else {
    console.log('짝수입니다.');
  }
} else {
  console.log('4의 배수입니다.');
}
```

```javascript
//return과 function을 활용한 if~else 문 예시
function evalNum () {
  const x = 21;

  if (x % 2) {
    console.log('홀수입니다.');
    return;
  }

  if (x % 4) {
    console.log('짝수입니다.');
    return;
  }

  console.log('4의 배수입니다.');
}

evalNum();
console.log('블록문 바깥');
```



### switch

특정 변수에 대한 조건이 여러개일 때 유용하다.

```javascript
// 💡 참고: 객체를 사용한 방법
const direction = 'north'

//??를 활용하여, direction에 지정된 데이터 외의 값이 들어오게 되는 경우, directionKor을 '무효' 로 출력한다.
const directionKor = {
  north: '북',
  south: '남',
  east: '동',
  west: '서'
}[direction] ?? '무효'

console.log(directionKor);
```

```javascript
const month = 1;
let season = '';

switch (month) {
  case 1: case 2: case 3:
    season = '1분기'; break;

  case 4: case 5: case 6:
    season = '2분기'; break;

  case 7: case 8: case 9:
    season = '3분기'; break;

  case 10: case 11: case 12:
    season = '4분기'; break;

  default: 
    season = '잘못된 월입니다.';
}

console.log(season);
```



### for 루프

```javascript
//백틱 표현 활용

for (let i = 1; i <= 9; i++) {
  for (let j = 1; j <= 9; j++) {
    console.log(`${i} * ${j} = ${i * j}`);
  }
}

// 1 * 1 = 1 
// 1 * 2 = 2
// ....
// 9 * 9 = 81 
```

```javascript
//무한 루프
let x = 0;

for (;;) {
  console.log(x);
}

console.log('출력 안됨');
```

```javascript
//for문 응용
for (
  let x = true, y = 0, z = 0;
  y * z < 10;
  x = !x, x ? y++ : z++
) {
  console.log(y, z);
}

// 0 0
// 0 1
// 1 1
// 1 2
// ...
// 3 3
```

```javascript
//객체에 대해 요소들을 모두 출력하는 코드.
//객체에 대해 for문을 적용 시, 객체 각 요소의 key값들을 호출하게 된다.
const lunch = {
  name: '라면',
  taste: '매운맛',
  kilocalories: 500,
  cold: false
}

for (const key in lunch) { // 💡 변할 것이 아니므로 const 사용
  console.log(key, ':', lunch[key])
}

// name: '라면',
// taste: '매운맛',
// kilocalories: 500,
// cold: false
```

for~of 구문 => iterable 객체에 대해 사용되며, 해당 객체의 요소를 모두 꺼낸다.

```javascript
const list = [1, '가나다', false, null];

for (const item of list) {
  console.log(item);
}
for (const el of list) {
  console.log(el);
}

// 문자열 역시 이터러블이므로 사용 가능
for (const letter of '안녕하세요~') {
  console.log(letter);
}
```

```javascript
const numbers1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const numbers2 = [];

for (let num of numbers1) {
  num++; // ⚠️ 복사된 값. let 사용 주목
  numbers2.push(num + 1);
}
console.log(numbers1, numbers2);

// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
// [3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```

continue와 break 활용

```javascript
for (let i = 1; i <= 10; i++) {
  if (i % 3 === 0) continue;
  console.log(i);
}

console.log('for 루프 종료');
```

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) break;
  console.log(i);
}

console.log('for 루프 종료');
```



### while과 do while

do while => 일단 do 구문을 무조건 시행한 후, while 조건문을 따져서 do구문을 반복 실행할지 여부를 결정

```javascript
let x = 12;

do {
  console.log(x++);
} while (x < 10);

//12
```



## 섹션4. 함수

### 함수의 의미와 사용법

function의 반환값이 명시되어 있지 않다면, undefined를 반환한다.



호이스팅 

* 변수, 상수는 호이스팅이 되지 않음

* 함수는 "선언 방법에 따라 "호이스팅이 가능

  * 왜냐하면, js가 실행될 때, 함수부터 먼저 쭉 찾아서 변수들로 등록하기 때문

  * ```javascript
    // 함수는 실행문보다 나중에 정의하는 것이 가능
    // 변수나 상수는 불가능! (var 제외)
    console.log(add(2, 7));
    
    function add (x, y) {
      return x + y;
    }
    ```

  * 함수도 값이고, 객체이기 때문에 아래와 같이 선언할 수 있다.

    ```javascript
    const subt = function (x, y) {
      return x - y;
    }
    
    console.log(subt(7, 2));
    ```

  * 기존 함수 재정의

  * ```javascript
    function add (x, y) {
      return x + y;
    }
    
    console.log(add(2, 7));
    ```

  * ```javascript
    // 💡 기존의 함수를 재정의하는것도 가능
    add = function (x, y) {
      console.log(`${x}와 ${y}를 더합니다.`);
      console.log(`결과는 ${x + y}입니다.`);
      return x + y;
    }
    
    console.log(add(2, 7));
    ```

  * 화살표 함수로도 정의 가능

    ```javascript
    // 인자가 하나일 때는 괄호 없이 선언 가능
    const pow = x => x ** 2;
    console.log(pow(3));
    ```

* 호이스팅은 "함수 선언" 형태로 정의된 것만 가능하다.

  * 왜냐하면, 위 방법으로 인한 함수 생성의 시점은, 엔진 코드 실행 이전에 미리 생성되기 때문이다.


* <u>*(나의 개인적인 의문)*</u>

  * <u>*함수가 왜 "1급 객체" 여야만 하는지를 파악하기 위해서 구글링을 해 보았는데, 이는 프로토타입을 알아야 제대로 파악이 가능할 것 같다.*</u>

    => 



### 일급 객체

js의 함수는 "변수"와 같이 다루는 개념이 존재한다.

=> 1급 객체로서 다룬다.

* 따라서, 상수나 변수에 할당될 수 있다.

  ```javascript
  function isOddNum (number) {
    console.log(
      (number % 2 ? '홀' : '짝')
      + '수입니다.'
    );
    return number % 2 ? true : false;
  };
  
  const checkIfOdd = isOddNum; // 뒤에 괄호 없음 유의
  
  console.log(checkIfOdd(23));
  
  // 홀수입니다.
  // true
  ```

* 다른 함수의 인자로서도 전달될 수 있다.

* 다른 함수의 결과값으로서 반환될 수 있다.

* 심지어, 어떤 객체의 키에 상응하는 value로도 받을 수 있다.

  * ```javascript
    let person = {
      name: '홍길동',
      age: 30,
      married: true,
      introduce: function (formal) {
        return formal
        ? '안녕하십니까. 홍길동 대리라고 합니다.'
        : '안녕하세요, 홍길동이라고 해요.';
      }
    };
    
    console.log(person.introduce(true));
    console.log(person.introduce(false));
    ```

  * 객체의 다른 프로퍼티에 접근할 때, this를 사용

    ```javascript
    let person = {
      name: '홍길동',
      age: 30,
      married: true,
      introduce: function () {
        return `저는 ${this.name}, ${this.age}살이고 `
        + `${this.married ? '기혼' : '미혼'}입니다.`;
      }
    }
    
    console.log(person.introduce());
    ```

    참고로 아래의 경우에는 this 참조를 활용할 수 없다.

    (할 수 있기는 한데, name과 age와 married 프로퍼티를 읽어들이지 못한다.)

    ```javascript
    let person = {
      name: '홍길동',
      age: 30,
      married: true,
      introduce: () => {
        return `저는 ${this.name}, ${this.age}살이고 `
        + `${this.married ? '기혼' : '미혼'}입니다.`;
      }
    }
    
    console.log(person.introduce());
    ```

    => (내 생각) 이 경우에는 메서드가 먼저 메모리에 실리고 아니고의 차이일 거 같은데... 음...

  * 배열의 요소로도 받을 수 있다.

  * ```javascript
    let arithmetics = [
      (a, b) => a + b,
      (a, b) => a - b,
      (a, b) => a * b,
      (a, b) => a / b
    ];
    
    for (arm of arithmetics) {
      console.log(arm(5, 3));
    }
    ```



고차함수, 콜백함수

```javascript
let list = [1, 2, 3, 4, 5];

function doInArray (array, func) {
  for (item of array) {
    func(item);
  }
}

// console.log - console이란 객체에서 log란 키에 할당된 함수

// doInArray => "고차함수" (전달받는 함수)
// console.log => "콜백함수" (전달하는 함수)
doInArray(list, console.log);
```

```javascript
function doNTimes (func, repeat, x, y) {
  let result = x;
  for (i = 0; i < repeat; i++) {
    result = func(result, y);
  }
  return result;
}

console.log(
  doNTimes((x, y) => x * y, 3, 5, 2),
  doNTimes((x, y) => x / y, 3, 5, 2),
);
```

```javascript
// calculate
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;
const multiply = (a, b) => a * b;

// evaluate
const isOdd = (number) => !!(number % 2);
const isPositive = (number) => number > 0;

//아래의 "인자로 전달된 함수"인 calc와 eval은, 상수나 변수에 할당된 함수가 아니기 때문에, "익명 함수" 라고 불리운다.
function calcAndEval (calc, eval, x, y) {
  return eval(calc(x, y));
}

console.log(
  calcAndEval(add, isOdd, 5, 7),
  calcAndEval(subtract, isPositive, 5, 7),
  calcAndEval(multiply, isOdd, 5, 7)
);
```



결과값으로서 함수를 반환받는 경우 역시 존재

```javascript
function getIntroFunc (name, formal) {
  return formal
  ? function () {
    console.log(`안녕하십니까, ${name}입니다.`);
  } : function () {
    console.log(`안녕하세요~ ${name}이라고 해요.`);
  }
}

const hongIntro = getIntroFunc('홍길동', true);
const jeonIntro = getIntroFunc('전우치', false);
```

```javascript
// hongIntro와 jeonIntro 에 "함수"가 할당되었음을 인지하자
hongIntro();
jeonIntro();
```



커링

* 어떤 함수에서 필요한 인자보다 적은 수의 인자를 받으면, 나머지 인자를, 인자로 받는 다른 함수를 반환

  * 그러고 나서 추후에 나머지 인자를 받으면, 반환받은 함수에다가 인자를 넣으면 될 것이다.

  ```javascript
  // 기존의 코드
  function addMultSubt (a, b, c, d) {
    return (a + b) * c - d;
  }
  
  const addMultSubt2 = (a, b, c, d) => (a + b) * c - d;
  
  console.log(
    addMultSubt(2, 3, 4, 5),
    addMultSubt2(2, 3, 4, 5),
  );
  ```

  ```javascript
  // ⭐ 커링으로 작성된 함수
  function curryAddMultSubt (a) {
    return function (b) {
      return function (c) {
        return function (d) {
          return (a + b) * c - d;
        }
      }
    }
  }
  
  const curryAddMultSubt2 = a => b => c => d => (a + b) * c - d;
  ```

  ```javascript
  const curryAddMultSubtFrom2 = curryAddMultSubt(2);
  const curryMultSubtFrom5 = curryAddMultSubt(2)(3);
  const currySubtFrom20 = curryAddMultSubt(2)(3)(4);
  ```



### 매개변수

* 매개변수 갯수를 넘어가는 인수를 받을 때, 오류가 나지 않고 넘어가는 인수에 대해서는 무시한다.

  * 매개변수 자체에 대해서, default 값을 설정할 수도 있다.

  * 나의 의문) 아래의 출력 결과를 볼 때, console.log()의 매개변수를 모두 실행 후, 매개변수에 해당하는 값을 console에 출력하는 것으로 보임.

    ```javascript
    function add(a = 2, b = 4) {
      console.log(`${a} + ${b}`);
      return a + b;
    }
    
    console.log(
      add(),
      add(1),
      add(1, 3)
    );
    
    // 2+4
    // 1+4
    // 1+3
    // 6 5 4 (console.log의 결과물)
    
    ```

* 함수 호출 시 전달된 모든 인수들은 "배열" 처럼 동작한다. (매개변수 갯수를 넘어가는 인수가 전달되어도, 모두 "배열" 처럼 동작한다.)

  * ```javascript
    //함수 호출 시, 전달된 모든 인수들은 arguments 라는 벼ㅕㄴ수로 받는다.
    function add(a, b) {
      console.log('1.', arguments);
      console.log('2.', arguments[0]);
      console.log('3.', typeof arguments);
      return a + b;
    }
    
    console.log(
      '4.', add(1, 3, 5, 7)
    );
    
    // 1. Arguments(4) [100, 3, 5, 7, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    // 2. 1
    // 3. object
    // 4. 4
    ```

  * ```javascript
    //arguments 가 iterable 하므로, 아래의 식도 가능하다.
    //2개를 초과해서 4개의 인자를 받아도, 일단 arguments는 4개의 인자를 모두 담는다. 
    function add(a, b) {
      for (const arg of arguments) {
        console.log(arg);
      }
      return a + b;
    }
    
    console.log(
      add(1, 3, 5, 7)
    );
    
    //1
    //3
    //5
    //7
    //4
    ```

  전달받은 모든 인수를, 평균값을 내기 (숫자만 filtering 해서!)

  ```javascript
  //function을 정의할 때에는 인자가 없어도 된다고 정의하여도, arguments를 통해 인자를 전달받을 수 있다.
  function getAverage() {
    let result = 0;
    for (const num of arguments) {
      result += num;
    }
    return result / arguments.length;
  }
  
  console.log(
    getAverage(1, 4, 7),
    getAverage(24, 31, 52, 80)
  );
  
  // 4
  // 46.75
  ```

  ```javascript
  // 💡 타입에 안전한 버전
  // 전달받은 인자 중, 숫자인 인자에 대해서만 자동으로 계산하게 해 줌
  function getAverage() {
    let result = 0, count = 0;
    for (const num of arguments) {
      if (typeof num !== 'number') continue;
      result += num;
      count++;
    }
    return result / count;
  }
  
  console.log(
    getAverage(2, '가', 8, true, 5)
  );
  ```

  

(내 생각) 함수를 선언한 경우에만, 넘겨받은 인수에 대해서 arguments로 받을 수 있는 것처럼 보임.

=> 일단, 화살표로 정의된 함수에 대해서는, arguments를 사용할 수 없다.

```javascript
// ♻️ 새로고침 후 실행
// 아마, 화살표로 정의된 함수는, 넘겨받은 인자를 arguments에 바인딩되지 않는다는 점을 활용한 거 같다. (아직까지는 내 생각)
const add = (a, b) => a + b;
const sub = (a, b) => a - b;
const mul = (a, b) => a * b;
const div = (a, b) => a / b;

function combineArms () {
  return (x, y) => {
    let result = x;
    //combineArms()에 넘겨받은 인자들에 대해서 반복문 적용
    for (const arm of arguments) {
      if (typeof arm !== 'function') continue;
      result = arm(result, y);
    }
    return result;
  }
}

const add_mul = combineArms(add, mul, 1, true);
const add_mul_sub = combineArms(add, mul, sub);
const add_mul_sub_div = combineArms(add, mul, sub, div);

// 💡 익명 함수 사용됨
const add_mul_sub_div_pow
  = combineArms(add, mul, sub, div, (x, y) => x ** y);
```

```javascript
console.log(
  add_mul(8, 3),
  add_mul_sub(8, 3),
  add_mul_sub_div(8, 3),
  add_mul_sub_div_pow(8, 3)
);

// 33
// 30
// 10
// 1000
```



rest parameters

* 매개변수의 맨 마지막 인자로만 사용이 가능하며, "수가 정해지지 않은" 매개변수들을 받을 떄 활용

  * rest parameters는 실제 배열 타입이다.

* ```javascript
  console.log(
    '3.',
    classIntro(3, '김민지', '영희', '철수', '보라')
  ); // 호이스팅
  
  function classIntro (classNo, teacher, ...children) {
    console.log('1.', children);
    console.log('2.', arguments);
  
    let childrenStr = '';
    for (const child of children) {
      if (childrenStr) childrenStr += ', ';
      childrenStr += child;
    }
    return `${classNo}반의 선생님은 ${teacher}, `
      + `학생들은 ${childrenStr}입니다.`
  }
  
  // 1. (3) ['영희', '철수', '보라']
  // 2. Arguments(5) [3, '김민지', '영희', '철수', '보라', callee: (...), Symbol(Symbol.iterator): ƒ]
  // 3. 3반의 선생님은 김민지, 학생들은 영희, 철수, 보라입니다.
  
  ```

* ```javascript
  // 사칙연산을 적용하는 코드
  
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  
  function doMultiArms (x, y, ...arms) {
    let result = x;
    for (const arm of arms) {
      if (typeof arm !== 'function') continue;
      result = arm(result, y);
    }
    return result;
  }
  
  console.log(
    doMultiArms(8, 3, add, mul, 1, true),
    doMultiArms(8, 3, add, mul, sub),
    doMultiArms(8, 3, add, mul, sub, div),
    doMultiArms(8, 3, add, mul, sub, div, (x, y) => x ** y)
  );
  ```



<u>개인적으로 내가 가졌던 궁금한 사항</u>

* <u>왜 화살표 함수는 arguments를 활용할 수 없을까?</u>

  => 아주 정확한 이유는 아직 모르지만, 일반함수로 정의했을 때는 Arguments가 null이나, 화살표로 함수를 정의 시, Arguments에 접근이 불가능함을 알 수 있다.

  => 블로그의 설명대로 따르면, 화살표로 정의된 함수는, 넘겨받은 인자들을 Arguments에 바인딩하지 않는다고 한다.

  * 출처 : https://velog.io/@ansrjsdn/%EC%99%9C-%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98%EC%97%90%EB%8A%94-arguments%EA%B0%80-%EC%97%86%EC%9D%84%EA%B9%8C



### 함수 더 알아보기

outer 함수 내부에서만 또다른 함수가 쓰일 때, 중첩 함수를 정의할 수 있다.

```javascript
function outer () {
  const name = '바깥쪽'
  console.log(name, '함수');

  function inner () {
    const name = '안쪽'
    console.log(name, '함수');
  }
  inner();
}

outer();
```



** <u>내가 가졌던 의문</u>

* 위처럼 중첩해서 함수를 정의하는 것과, 중첩하지 않고 정의하는 것의 차이점이 있을까? (즉, outer() 와 inner() 를 별도의 함수로서 동일한 스코프에서 정의한다면?)

  => 클린코드적 관점이랑, 성능적 관점에서 생각해볼 수 있다.

  * 클린코드적 관점

    * 중첩해서 함수를 정의한다면, inner()는 outer()가 호출될 때에만 쓰임을 명시적으로 드러내므로, 중첩하지 않고 정의할 때보다 코드의 질이 올라간다

  * 성능적 관점

    * 함수 역시 "값" 임에 초점을 두자

      * 그렇다면, 위의 경우처럼 중첩을 한다면, inner() 함수 객체는 outer()가 호출될때마다 생성되고, 호출이 끝나면 파괴된다.
      * 반면, 중첩을 하지 않고 동일한 스코프에서 inner() 와 outer()를 정의한다면, outer() 함수 객체는 단 1번 생성되며 해당 객체가 계속 사용된다.

    * 따라서, 이론적으로는 중첩하지 않고, 동일한 스코프에서 별도의 함수로 선언하는 것이 성능 상 더 좋을 수 있다

      => 오래전에는 그러했으나, 요즘에는 자바스크립트 엔진 내부적으로 중첩된 함수에 대해 최적화 로직이 적용되어 있다고 한다.

      => 따라서, 중첩하지 않았을 경우랑 성능 상 별 차이가 없다고 한다.

  * 출처 : https://siyoon210.tistory.com/162



재귀 함수

```javascript
function upto5 (x) {
  console.log(x);
  if (x < 5) {
    upto5(x + 1);
  } else {
    console.log('- - -');
  };
}

upto5(1);
upto5(3);
upto5(7);

// 1
// 2 
// 3
// 4
// 5 
// ---
// 3
// 4
// 5
// ---
// 7
// ---
```



팩토리얼 재귀 함수

```javascript
function fact(x) {
  return x === 0 ? 1 : x * fact(x - 1);
}

console.log(
  fact(1),
  fact(2),
  fact(3),
  fact(4)
)

//1 2 6 24
```

** 자바스크립트에서는, tail recursion을 활용해서 내부적으로 for문을 돌려서 stack frame이 쌓이는 거를 방지하는 기술은 적용되어 있지 않다고 한다.



IIFE

* 일회용 함수 개념(함수 이름은 익명임)

  * 함수를 정의함과 동시에 즉시 시행할 때 활용

  ```javascript
  (function () {
    console.log('IIFE');
  })();
  ```

  

* 아래의 경우 사용된다.

  * function의 경우, 1회성으로 사용되므로 아래와 같이 정의했다.

  ```javascript
  const initialMessage = (function () {
    // ⚠️ var를 사용함에 주목
    var month = 8;
    var day = 15;
    var temps = [28, 27, 27, 30, 32, 32, 30, 28];
    var avgTemp = 0;
    for (const temp of temps) {
      avgTemp += temp
    }
    avgTemp /= temps.length;
  
    return `${month}월 ${day}일 평균기온은 섭씨 ${avgTemp}도입니다.`;
  })();
  
  console.log(initialMessage);
  console.log(month); //month를 var로 선언하였기에, 출력이 된다.
  ```

  => month는 블록 바깥에서 활용되지 않는다. (* 아래의 경우는, var로 선언 시, 블록 바깥에서도 해당 변수가 사용이 가능하다는 문제점이 있다.)



아래의 코드는 블록 내부에서, var로 선언 시 블록 바깥에서 활용 가능하다. (const나 let으로 선언한 경우는 스코프 내에서만 활용이 가능)

```javascript
let initialMessage;

{
  const month = 8;
  const day = 15;
  const temps = [28, 27, 27, 30, 32, 32, 30, 28];
  let avgTemp = 0;
  for (const temp of temps) {
    avgTemp += temp
  }
  avgTemp /= temps.length;

  initialMessage = `${month}월 ${day}일 평균기온은 섭씨 ${avgTemp}도입니다.`;
};

console.log(initialMessage);
console.log(month); // 에러 발생한다. 새로고침 후 const를 var로 바꾸고 실행해볼 것.
```

위처럼 var는 블록 외에서도 사용될 수 있었다는 문제점 때문에, var 사용 시 예전에 불편하게 IIFE를 만들어서 사용했다.

=> 이제는 const와 let을 활용해서 그냥 블록문을 실행하면 된다.



## 섹션5. 객체와 클래스

### 객체의 기본 사용법들

객체의 프로퍼티 접근 시, 식별자 명명 규칙에 벗어난 키라면, [] 로만 접근해야 한다.

```JAVASCRIPT
const obj = {
  1: '하나', // 숫자도 객체의 키로는 사용 가능
  'ab-cd': 'ABCD', // 문자 포함 시 키도 따옴표로 감싸야 함
  's p a c e': 'Space'
}

// 아래의 index는, 대괄호 프로퍼티 접근 연산자로만 가능
console.log(
  obj[1],
  obj['ab-cd'],
  obj['s p a c e']
);

// ⚠️ 오류 발생
// console.log(
//   obj.1,
//   obj.ab-cd,
//   obj.s p a c e
// );
```



키는 표현식으로도 정의할 수 있다.

 ```javascript
let idx = 0;
const  obj = {
  ['key-' + ++idx]: `value-${idx}`,
  ['key-' + ++idx]: `value-${idx}`,
  ['key-' + ++idx]: `value-${idx}`,
  [idx ** idx]: 'POWER'
}

console.log(obj);
// {27: 'POWER', key-1: 'value-1', key-2: 'value-2', key-3: 'value-3'}
 ```



★ 키는, 객체나 배열을 쓸 떄는 주의를 요한다

* 키를 객체로 쓸 경우, (객체의 값에 관계없이) [Object object] 를 키값으로 가진다.

  * 따라서, 아무 객체나 키값으로 지정해도 데이터가 호출이 된다.

* 배열을 객체로 쓸 경우, 내부 요소를 문자열로 치환한 값을 키값으로 가진다.

  * 해당 문자열을 키값으로 하여, value를 조회하면 같은 결과가 나온다.

  (아래의 각 단락은 모두 같은 결과를 나타낸다.)

```javascript
const objKey = { x: 1, y: 2 };
const arrKey = [1, 2, 3];

const obj = {
  [objKey]: '객체를 키값으로',
  [arrKey]: '배열을 키값으로'
}
```

```javascript
console.log(
  obj[objKey],
  obj[arrKey]
);

// 객체를 키값으로 배열을 키값으로
```

```javascript
// ⚠️ ???????
console.log(
  obj[{ a: 1, b: 2, c: 3 }], // 내용이 다른 객체
  obj['1,2,3'], // 문자열
  obj['1,2,3,4'] // 접근이 되지 않는다.
);

// 객체를 키값으로 배열을 키값으로 undefined
```

```javascript
console.log(
  obj['[object Object]']
);

//객체를 키값으로
```

```javascript
//obj를 console로 찍으면, 위 현상의 원인을 파악할 수 있다.
console.log(obj);

//{[object Object]: '객체를 키값으로', 1,2,3: '배열을 키값으로'}
```



delete 프로퍼티는, 없는 프로퍼티를 삭제하려고 해도 오류가 발생하지 않는다.



동적으로 키를 할당할 때는, 반드시 대괄호로 접근해야만 한다.

(obj.key로 접근 시, key 필드로 접근하겠다는 의미이기 때문.)

```javascript
const product1 = {
  name: '노트북',
  color: 'gray',
  price: 800000
}

function addModifyProperty (obj, key, value) {
  // obj.key = value; // ⚠️ 의도와 다른 작업 수행
  obj[key] = value;
}

function deleteProperty (obj, key) {
  // delete obj.key // ⚠️ 의도와 다른 작업 수행
  delete obj[key];
}
```

```javascript
addModifyProperty (product1, 'inch', 16);
console.log(product1);

// {name: '노트북', color: 'gray', price: 800000, inch: 16}
```

```javascript
addModifyProperty (product1, 'price', 750000);
console.log(product1);

// {name: '노트북', color: 'gray', price: 750000, inch: 16}
```

```javascript
deleteProperty(product1, 'color');
console.log(product1);

// {name: '노트북', price: 750000, inch: 16}
```



ES6 추가 문법

```javascript
function createProduct (name, price, quantity) {
  return { name, price, quantity }; //key가 name이고 value도 name에 할당된 데이터를 받아옴
}

const product1 = createProduct('선풍기', 50000, 50);
const product2 = createProduct('청소기', 125000, 32);

console.log(product1, product2);
```

 => 객체 프로퍼티로서, "함수 프로퍼티"를 쓸 때, 축약해서 쓸 수 있다.

=> 그리고 이렇게 객체의 축약 표현으로 정의된 함수 프로퍼티를, "메서드" 라고 부른다.

```javascript
// 일반 함수 프로퍼티 정의
const person = {
  name: '홍길동',

  salutate: function (formal) {
    return formal
    ? `안녕하십니까, ${this.name}입니다.`
    : `안녕하세요, ${this.name}이에요.`;
  }
}
console.log(person.salutate(true));
```

```javascript
// ⭐️ 메서드 정의
const person = {
  name: '홍길동',
  
  salutate (formal) {
    return formal
    ? `안녕하십니까, ${this.name}입니다.`
    : `안녕하세요, ${this.name}이에요.`;
  }
}
console.log(person.salutate(true));
```

=> 모두 같은 코드이다.



### 생성자 함수

어떤 함수가 대문자로 시작하면, 이는 관례적으로 "생성자 함수" 이다.

* 생성자 함수는 암묵적으로 this를 반환한다. (new 연산자를 활용했을 경우에 한해서이다!)
* 생성자 함수 내에서는, 또다른 메서드를 정의할 수 없다. 오직 프로퍼티로서만 정의가 가능
  * 객체가 아니라 함수이기 때문
    * (나의 의문) 약간 이유가 애매하기는 하지만, 일단은 애매하게 이해했음을 인지하고 넘어가기.
* 해당 함수의 this는, 해당 (생성자) 메서드 실행 결과로 인해 곧 생성될 인스턴스를 의미한다.
  * 참고) 함수를 메서드로서 호출하는지, 일반 함수로서 호출하는지, 생성자 함수로서 호출하는지에 따라 this의 역할이 달라진다
  * 출처 : https://jeongwle.tistory.com/19 



생성자 함수도 기본적으로 함수이기 때문에, 원하는 결과를 얻고 싶으면 new를 붙여서 호출해야 한다.

* 그렇지 않으면, return이 보통 지정되어 있지 않으므로 undefined가 반환된다.
* 또한, 어떠한 함수를 생성자 함수로 활용하려고 하면, return을 쓰면 안 된다.
  * return을 쓰게 된다면, 해당 함수는 일반 함수로 작동하게 된다. 이는 생성자 함수로서의 의미를 훼손하게 된다.





프로토타입

* 클래스 전에 프로토타입이 나왔고, 다른 언어에서 이후 클래스로 대체되었다.
* js는 "프로토타입" 기반이다.
  * 생성자 함수로 인스턴스를 생성하더라도, prototype을 통해서 유기적으로 연결되어 있음
    * 반드시 생성자 함수로 인스턴스를 생성하여야, prototype과 유기적으로 연결된다.
    * new 연산자를 통해 생성된 객체는, `__proto__` 프로퍼티를 내부적으로 가지며, 이 프로퍼티는, 생성자 함수의 prototype 프로퍼티 값(=객체)를 가리키게 된다.
  * prototype을 통해 추가한 메서드는 [Prototype] : Object 에 보면 확인할 수 있다.

```javascript
function YalcoChicken (name, no) {
  this.name = name;
  this.no = no;
  this.introduce = function () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
}

const chain1 = new YalcoChicken('판교', 3);
console.log(chain1);
```

```javascript
// 본사에서 새 업무를 추가
// 프로토타입: 본사에서 배포하는 메뉴얼이라고 이해
YalcoChicken.prototype.introEng = function () {
  return `Welcome to Yalco Chicken at ${this.name}!`;
};
//이후 YalcoChicken 생성자 함수를 이용하여, new 연산자를 통해 만들어진 객체의 __proto__ 프로퍼티는, YalcoChicken.prototype 의 값(=객체)를 가리키게 된다.
```

```javascript
console.log(chain1.introEng());
console.log(new YalcoChicken('강남', 17).introEng());
```

=> YalcoChicken.introEng 라고 하게 되면, YalcoChicken 객체 자체에다가 introEng 프로퍼티를 정의하는 것이다.

​	=> 이는 YalcoChicken.prototype.introEng와 완전 다른 개념!

=> 여튼, 프로토타입으로 계속 넘어와서, new YalcoChicken()으로 새로운 객체를 만들게 되면, 해당 객체는 YalcoChicken.prototype의 값(객체)을 가리키게 된다.

=> 이는, `new YalcoChicken().__proto__` 가 가리키는 값과 동일하다.





생성자를 만드는 방식(객체 리터럴, 객체 반환 함수, 생성자 함수) 비교

* 생성자 함수를 통해 만들어진 객체는 prototype을 통해 사후관리가 가능하다
  * 위의 경우, prototype을 통해 추가한 메서드라고 할 수 있다.
  * 반면, 객체를 직접 반환하거나 객체 리터럴을 통한 객체 생성은 사후 관리가 되지 않는다.
    * 이는, 생성자 함수에 new 연산자를 적용하여 생성된 객체는, 내부적으로 생성자 함수의 prototype 프로퍼티의 값(=객체)을 가리키게끔 로직이 적용되기 때문이다.  
* prototype에서, 생성자 함수로 만들어진 객체는 instanceof 연산을 적용할 수 있다.

```javascript
function YalcoChicken (name, no) {
  this.name = name;
  this.no = no;
  this.introduce = function () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
}

function createYalcoChicken (name, no) {
  return {
    name, no,
    introduce () {
      return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
    }
  }
}

// 객체 리터럴
const chain1 = {
  name: '판교', no: 3,
  introduce: function () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
};

// 객체 반환 함수
const chain2 = createYalcoChicken('강남', 17);

// 생성자 함수
const chain3 = new YalcoChicken('제주', 24);
```

```javascript
console.log(chain1, chain1 instanceof YalcoChicken); //false
console.log(chain2, chain2 instanceof YalcoChicken); //false
console.log(chain3, chain3 instanceof YalcoChicken); //true
```

```javascript
//아래의 경우를 본다면, prototype이 어떤 것인지 좀 더 명확해질 것이다.
console.log(chain2.__proto__); // {constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}

console.log(chain3.__proto__); // {constructor: ƒ}
console.log(chain3.__proto__.__proto__); // chain2.__proto__와 동일

//즉, chain2는, 기본적인 prototype 객체가 생성됨을 확인할 수 있고, chain3는 new 연산자를 통해 생성되었으므로,  YalcoChicken.prototype이 가리키는 값(객체)이 chain3.__proto__에 할당됨을 알 수 있다
	//=> 또한, chain3.__proto__ 역시 객체이므로, 이 객체의 __proto__ 프로퍼티는 기본적인 prototype 객체임을 확인할 수 있다.
```



함수도 객체이므로, 아래의 기능이 가능하다.

* 인스턴스를 생성하지 않고, 함수 자체에 대해 필드와 함수를 추가할 수 있다. 
  * 이는, 치킨을 관리하는 방법에 이슈가 있을 시, 가맹점(인스턴스)가 아닌 본사에 전화를 하는 것과 같다.

```javascript
function YalcoChicken (name, no) {
  this.name = name;
  this.no = no;
  this.introduce = function () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
}

// 본사의 정보와 업무
YalcoChicken.brand = '얄코치킨';
YalcoChicken.contact = function () {
  return `${this.brand}입니다. 무엇을 도와드릴까요?`;
};

const chain1 = new YalcoChicken('판교', 3);

console.log(YalcoChicken.contact());
console.log(chain1.contact()); //에러 발생
```



new 연산자를 실수로 빠뜨린 경우, 아래의 코드로 보완이 가능하다.

```javascript
function YalcoChicken (name, no) {
  this.name = name;
  this.no = no;
  this.introduce = function () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }

  if (!new.target) { // 이 부분을 지우고 다시 해 볼 것
    return new YalcoChicken(name, no);
  }
}

const chain1 = new YalcoChicken('판교', 3);
const chain2 = YalcoChicken('강남', 17);

console.log(chain1, chain2);
```



참고 사항

* 프로토타입의 정의와 내용

  * (생성자) 함수의 프로토타입과, 해당 생성자 함수를 통해 (new 연산자 이용하여) 생성된 객체와의 연관성
  * 출처 : https://ko.javascript.info/function-prototype

* new.target에 대한 내용

  * 출처 : https://ko.javascript.info/constructor-new

* hoisting의 원리 (요약)

  * javascript는 Execution Context 객체를 생성하여 변수 관리를 하게 된다.

    * Execution Context의 종류에는, Global Execution Context와 Functional Execution Context가 있다

      * 그리고, 각 Execution Context는 Lexical Environment와 Variable Environment로 나누어져 있다.

        * 코드가 실행되기 전인 Creation Phase와, 실행되는 중인 Execution Phase로 나뉘게 된다.

          * 각각의 Environment는, key가 식별자(변수명, class 명 등)이며 value가 각 변수에 할당된 값이 된다.

          * 이 때, 코드가 실행되기 전, JS는 선언된 변수와 class명을 스캔하여 각 Environment에 저장한다

            * var로 선언된 변수는 Variable Environment에 저장되며, 이는 해당 Execution Context의 스코프 및 내부 스코프에 var로 선언된 변수가 저장이 된다.
            * 이 때, 초깃값은 undefined로 설정된다.

          * let, const로 선언된 변수는 Lexical Environment에 저장되며, 이는 해당 Execution Context의 스코프에 선언된 변수만 저장이된다.

            * 이 때, 초깃값은 역시 undefined로 설정된다.

              => 이러한 원리에 의해, 

            * 따라서, 해당 Execution Context의 스코프 내부에 또다른 스코프가 있는 경우, 그 내부 스코프에 let / const로 선언된 변수는 현재의 Lexical Environment에 저장되지 않는다.(★)

              => 즉, 내부 스코프의 Creation Phase 단계 전까지는, 내부 스코프의 let/const로 선언된 변수 자체가 Lexical Environment에 저장되지 않는다. 

        * 코드가 실행되고 나서, 각 변수에 값을 할당하는 코드가 실행되고 나서야 각 Environement에 선언된 변수가 초기화된다.

        * 함수의 경우, Creation Phase 단계에서 Variable Environment에 저장이 되기 때문에 hoisting이 되는 것이다.

        * 이외에 hoisting이 되면서 값으로 초기화가 되는 대상은 아래와 같다

          * var로 선언된 변수 => undefined로 초기화됨
          * function

        * 반면, hoisting은 되나, uninitialized로 초기화가 되어서 error를 발생시키는 대상은 아래와 같다

          * let,const로 선언된 변수
          * class

        * hoisting이 되지 않는 대상은 아래와 같다.

          * 함수 표현식
          * 클래스 표현식

  * 출처 

    * https://blinders.tistory.com/90
    * https://dkje.github.io/2020/08/30/ExecutionContext/



### 클래스

엄밀히 얘기하면, 생성자 함수나 프로토 타입은 타 언어 문법과 차이가 있으므로, 타 언어 문법과 비슷한 "클래스"로 포장한 것임. (Syntactic sugar)

* 생성자 함수와의 차이점

  * 클래스는 호이스팅이 불가능하다.
  * 클래스를 활용하여 인스턴스 생성 시, new 연산자가 반드시 필요하다.

  ```javascript
  // 차이 1. 클래스는 호이스팅되지 않음 (정확히는 되지만...)
  const chain1 = new YalcoChicken('판교', 3);
  
  class YalcoChicken {
    constructor (name, no) {
      this.name = name;
      this.no = no;
    }
    //프로토타입의 메서드로 간주된다.
    introduce () {
      return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
    }
  }
  ```

  ```javascript
  // 차이 2. 클래스는 new 없이 사용하면 오류
  // (생성자 함수는 오류 없이 undefined 반환)
  //const chain2 = YalcoChicken('강남', 17); //error
  
  const chain3 = new YalcoChicken('판교', 33);
  console.log(chain3); // YalcoChicken {name: '판교', no: 33}
  console.log(YalcoChicken.prototype); // {constructor: ƒ, introduce: ƒ}
  ```

* constructor 메서드

  ```javascript
  class Person {
    constructor (name, age, married = false) {
      this.name = name;
      this.age = age;
      this.married = married;
    }
  }
  
  const person1 = new Person('박영희', 30, true);
  const person2 = new Person('오동수', 18);
  console.log(person1, person2);
  ```

* 클래스로 만든 인스턴스와 메서드로 만든 인스턴스의 차이점

  * 아래의 예시에서, 클래스로 만든 인스턴스는, 프로토타입의 속성으로 bark 메서드를 가진다

  * 또한, constructor로 "class Xxx" 로 나타내어진다.

    ```javascript
    class Dog {
      //bark() 함수는 프로토타입으로 들어간다.
      bark () {
        return '멍멍';
      }
    }
    const badugi = new Dog();
    console.log(badugi, badugi.bark());
    
    //Dog {} [[Prototype]]: Object  bark: ƒ bark()  constructor: class Dog  [[Prototype]]: Object
    ```

  * 반면, 메서드로 만든 인스턴스는, key-value 형식으로 가진다.

    ```javascript
    function Dog2 () {
      //Dog2() 생성자 함수와 new 연선자를 활용하여 만든 객체의, 함수 프로퍼티로 들어간다.
      this.bark = function () {
        return '멍멍';
      }
    }
    const badugi = new Dog2();
    console.log(badugi, badugi.bark());
    ```

    

    



클래스 필드

=> 아래와 같이 정의 가능하다.

```javascript
class YalcoChicken {
  //no와 menu, name 프로퍼티는 각각의 인스턴스의 프로퍼티로 정의된다.
  //초기화가 필요없으면, constructor()를 명시하지 않아도 된다.
  no = 0;
  menu = { '후라이드': 10000, '양념치킨': 12000 };

  constructor (name, no) {
    this.name = name;
    if (no) this.no = no;
  }
    
  //introduce() 와 order() 함수는 YalcoChicken의 프로토타입(=> 객체의 __proto__ 프로퍼티가 참조)에 속하게 된다.
  introduce () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
  order (name) {
    return `${this.menu[name]}원입니다.`
  }
}

console.log(new YalcoChicken('aa11'));
// YalcoChicken {no: 0, menu: {…}, name: 'aa11'}
```

=> no, menu, name 프로퍼티 // 프로토타입에 constructor, 메서드가 정의되어 있다.





클래스의 static 필드와 static 메서드는 오직 클래스 차원에서만 호출이 가능하다.

````javascript
class YalcoChicken {

  // 정적 변수와 메서드
  // YalcoChicken이 생성자 함수일 때, 마치 YalcoChicken.brand = '얄코치킨' 이렇게 지정하는 것과 동일 (즉, 인스턴스의 프로퍼티와 함수와는 관련이 없다.)
  // 따라서, new YalcoChicken().brand 나 new YalcoChicken().contact() 는 불가능하다.
  static brand = '얄코치킨';
  static contact () {
    return `${this.brand}입니다. 무엇을 도와드릴까요?`; //이 this는 YalcoChicken이다. 따라서, 정적 메서드에서는, 정적 필드만 호출이 가능하다. (당연히...)
  }

  constructor (name, no) {
    this.name = name;
    this.no = no;
  } 
  introduce () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
}

console.log(YalcoChicken);
console.log(YalcoChicken.contact());
````

=> 인스턴스가 brand 프로퍼티를 호출할 수 없다.



클래스는 함수이다. 따라서, 아래와 같이 쓸 수 있다.

```javascript
class Dog {
  bark () {
    return '멍멍';
  }
}

console.log(typeof Dog); //function
```

```javascript
const 개 = Dog; // 할당될 수 있는 일급 객체
const 바둑이 = new 개();

console.log(바둑이); // 💡 콘솔에 나타난 타입 확인
```



### 접근자 프로퍼티와 은닉

접근자 프로퍼티

=> getter, setter 함수라고도 불리운다.

=> 함수처럼 지정되었지만, 프로퍼티처럼 사용된다!

=> **앞에서 배운 프로퍼티는, "데이터" 프로퍼티 라고 부른다.

=> 객체 리터럴 및 클래스에서 사용이 가능하다.

```javascript
//객체 리터럴에서 사용하는 경우

const person1 = {
  age: 17, //데이터 프로퍼티

  get koreanAge () {
    return this.age + 1;
  },

  set koreanAge (krAge) {
    this.age = krAge - 1;
  }
}
```

```javascript
console.log(person1, person1.koreanAge);
//{age: 17} 18

person1.koreanAge = 20; //setter 호출
console.log(person1, person1.koreanAge); //getter 호출

//{age: 19} 20
```



클래스에서도 마찬가지로 

```javascript
class YalcoChicken {
  constructor (name, no) {
    this.name = name;
    this.no = no;
  }
  get chainTitle() {
    return `${this.no}호 ${this.name}점`;
  }
  set chainNo(chainNo) {
    if (typeof chainNo !== 'number') return;
    if (chainNo <= 0) return;
    this.no = chainNo;
  }
}
```

```javascript
const chain1 = new YalcoChicken('판교', 3);
console.log(chain1.chainTitle); //"3호 판교점"

console.log(chain1);

//chain1을 log로 찍어보면, chainTitle이 데이터 프로퍼티로 저장되어 있음을 확인할 수 있다.

//YalcoChicken {name: '판교', no: 3}
//name: "판교"
//no: 3
//chainTitle: "3호 판교점"
//[[Prototype]]: Object
//	chainTitle: "3호 판교점"
//	constructor: class YalcoChicken
//	set chainNo: ƒ chainNo(chainNo)
//	get chainTitle: ƒ chainTitle()
//	[[Prototype]]: Object
```

```javascript
chain1.chainNo = '4'; //setter에서 정한 제약조건 때문에 설정되지 않는다.
console.log(chain1);

//YalcoChicken {name: '판교', no: 3}
```

```javascript
chain1.chainNo = 4;
console.log(chain1);

//YalcoChicken {name: '판교', no: 6}
```



필드 이름과 setter의 이름이 같다면, this.no = no; 는, 결국 setter 함수를 호출하는 꼴이다.

```javascript
class YalcoChicken {
  constructor (name, no) {
    this.name = name;
    this.no = no; //set no(no) 호출
  }
  get no () { 
    return this.no + '호점'; 
  }
  set no (no) {
    this.no = no; //set no(no) 호출. 무한히 호출하므로, StackOverflow 에러가 발생.
  }
}
const chain1 = new YalcoChicken('판교', 3); // ⚠️ 오류 발생!
```

this.no => setter 함수를 호출할 가능성이 있다.

=> 따라서, this._no 를 활용하여, _no 필드를 별도로 setter 함수 내에 정의함 (알아서 해석함)

```javascript
class YalcoChicken {
  constructor (name, no) {
    this.name = name;
    this.no = no;
  }
  get no () { 
    return this._no + '호점'; 
  }
  set no (no) { 
    this._no = no;
  }
}

const chain1 = new YalcoChicken('판교', 3);
```



이제, this._no 에 직접 접근할 수 없게끔 해야 한다. (그래야 setter 함수를 사용하는 의미가 있으므로)

=> 따라서, 접근제어자 private 등장. (#을 프로퍼티 명 앞에 붙인다.)

** 의문) #을 붙여도... 접근이 되는데요????



```javascript
class Employee {
  #name = '';
  #age = 0;
  constructor (name, age) {
    this.#name = name;
    this.#age = age;
  }
  get name () {
    // [n]: n + 1 번째 글자를 반환
    return this.#name[0] + '모씨';
  }
  get age () {
    return this.#age - (this.#age % 10) + '대';
  }
  set age (age) {
    if (typeof age === 'number' && age > 0) {
      this.#age = age;
    };
  }
  getOlder(years) { this.#age += years; }
}

const emp1 = new Employee('김복동', 22);
```

```javascript
console.log(emp1.name, emp1.age)
```



=> 이로 인해, 클라이언트가 key를 알더라도, key에 해당하는 값을 알 수 없게 된다. (물론, 클라는 서버 내부의 코드를 볼 수 없다.)



### 상속

클래스의 상속 문법

=> 결국, JS에서는 프로토타입을 활용해서 상속을 구현함을 알 수 있다.

```javascript
class Bird {
  wings = 2;
}
class Eagle extends Bird {
  claws = 2;
}
class Penguin extends Bird {
  swim () { console.log('수영중...'); }
}
class EmperorPenguin extends Penguin {
  size = 'XXXL';
}

const birdy = new Bird();
const eaglee = new Eagle();
const pengu = new Penguin();
const pengdol = new EmperorPenguin();

console.log(birdy, eaglee, pengu, pengdol);

//어떤 객체의 __proto__ 프로퍼티의 값(=객체, =Function.prototype)의 타입은, 부모 클래스의 타입이라고 말할 수 있다.
// 예) eaglee 객체의 __proto__ 프로퍼티의 값의 타입은, Bird 타입이다.
//

//birdy
// Bird {wings: 2}
// wings: 2
// [[Prototype]]: Object
//		constructor: class Bird
//  	[[Prototype]]: Object

//eaglee
//Eagle {wings: 2, claws: 2}
//claws: 2
//wings: 2
//[[Prototype]]: Bird
//	constructor: class Eagle
//	[[Prototype]]: Object
// 		constructor: class Bird
//		[[Prototype]]: Object


//pengu
//Penguin {wings: 2}
//wings: 2
//[[Prototype]]: Bird
//	constructor: class Penguin
//	swim: ƒ swim()
//	[[Prototype]]: Object
//	constructor: class Bird
//	[[Prototype]]: Object

//pengdol
//EmperorPenguin {wings: 2, size: 'XXXL'}
//size: "XXXL"
//wings: 2
//[[Prototype]]: Penguin
//	constructor: class EmperorPenguin
//  [[Prototype]]: Bird
//		constructor: class Penguin
//		swim: ƒ swim()
//		[[Prototype]]: Object
//			constructor: class Bird
//			[[Prototype]]: Object
```

* 위의 예에서 알 수 있는 주요한 특징

  * 어떤 객체의 `__proto__ `프로퍼티의 값(=객체, =Function.prototype)의 타입은, 부모 클래스의 타입이라고 말할 수 있다.
    예) eaglee 객체의 `__proto__ `프로퍼티의 값의 타입은, Bird 타입이다.

  * 부모 객체와 자식 객체가 있다고 하자
    * 부모 객체의 프로퍼티의 값이 함수가 아니라면, (즉, 값이거나 객체라면), 해당 프로퍼티는 모두 자식의 프로퍼티로 간주된다.
    * 예) 위에서, eaglee 객체는 상위 클래스(Bird)에 정의된 "값 프로퍼티 wings" 프로퍼티를 가지게 된다.
    * => 내 생각) 이렇게 되어야 아래의 사유에서 합당하다고 생각
      * => this가 자식 객체를 나타내는 상황이라고 하자. 이 때, 부모 클래스의 함수를 호출할 때에는 `__proto__` 프로퍼티에 정의된 객체의 함수를 호출할 것이며, 이는 암묵적으로 this.(부모 클래스의 함수) 로서 호출을 한다.
      * => 이 때, 부모 클래스의 함수 내에서는, 부모 클래스의 프로퍼티를 활용하여 정의가 되어 있으며, 코드로서는 this.(부모 클래스 프로퍼티) 로서 작성되어 있을 것이다.
      * => 그런데 지금 상황에서는, this는 "자식 객체" 이므로, 위의 코드가 정상적으로 동작하려면 "자식 객체" 내에 "부모 클래스 값(객체) 프로퍼티" 가 정의되어야 할  것이다.
        * 함수는 일반적으로 Function.prototype에 정의되어 있으므로, 자식 객체인 this 입장에서  부모 클래스의 prototype에 정의된 함수를 활용하려면 this에다가 부모 클래스의 값(객체) 프로퍼티가 정의되어야 하는 것이 타당할 것이다.





```javascript
class YalcoChicken {
  no = 0;
  menu = { '후라이드': 10000, '양념치킨': 12000 };

  constructor (name, no) {
    this.name = name;
    if (no) this.no = no;
  }
  introduce () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
  order (name) {
    return `${this.menu[name]}원입니다.`
  }
}
```

```javascript
class YalcoChickenAndCafe extends YalcoChicken {
  cafeMenu = { '아메리카노': 4000, '라떼': 4500 };
  cafeOrder (name) {
    return `${this.cafeMenu[name]}원입니다.`
  }
}

const chain1 = new YalcoChickenAndCafe('서면', 2)
```

```javascript
console.log(chain1);

//YalcoChickenAndCafe {no: 2, menu: {…}, name: '서면', cafeMenu: {…}}
//cafeMenu: {아메리카노: 4000, 라떼: 4500}
//menu: {후라이드: 10000, 양념치킨: 12000}
//name: "서면"
//no: 2
//[[Prototype]]: YalcoChicken
//	cafeOrder: ƒ cafeOrder(name)
//	constructor: class YalcoChickenAndCafe
//	[[Prototype]]: Object
//		constructor: class YalcoChicken
//		introduce: ƒ introduce()
//		order: ƒ order(name)
//		[[Prototype]]: Object
```



오버라이딩

* 아래의 코드를 통해 내가 알아낸 사실
  * 부모 클래스와 자식 클래스에 travel()이 다 정의가 되어 있지만, `__proto__` 속성을 타고 올라가서 발견한 맨 첫번째의 travel() 메서드를 적용하는 것으로 보임 ( = 자식 클래스의 travel() 로 override가 된다고 말할 수 있다!)

```javascript
class Bird {
  wings = 2;
  canFly = true;
  travel () { console.log('비행중...') }
}
class Eagle extends Bird {
  claws = 2;
}
class Penguin extends Bird {
  canFly = false;
  travel () { console.log('수영중...') }
}
```

```javascript
const eaglee = new Eagle();
const pengu = new Penguin();

console.log(eaglee);
eaglee.travel();

console.log(pengu);
pengu.travel();
```

* 아래의 경우를 통해서, 상속의 특징을 알 수 있다.

  * YalcoChicken에 정의된 함수는 자식 객체가 호출할 수 있으며, 이 경우 this는 자식 객체가 된다.

    => 따라서, 부모 클래스에 정의된 프로퍼티가 자식 객체(this)가 직접 가지는 것이 타당할 것이다.

```javascript
class YalcoChicken {
  no = 0;
  menu = { '후라이드': 10000, '양념치킨': 12000 };

  constructor (name, no) {
    this.name = name;
    if (no) this.no = no;
  }
  introduce () {
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
  order (name) {
    return `${this.menu[name]}원입니다.`
  }
}

class YorkNannyYalcoChicken extends YalcoChicken {
  introduce () {
    return `또 뭐 쳐먹으러 기어들어왔어.`;
  }
  order (name) {
    return `${this.menu[name]}원이여.`
  }
}

const chain1 = new YorkNannyYalcoChicken ('종로', 48);

console.log(chain1.introduce()); //또 뭐 쳐먹으러 기어들어왔어.
console.log(chain1.order('양념치킨')); //12000원이여.
```



super 키워드

```javascript
class YalcoChicken {
  no = 0;
  menu = { '후라이드': 10000, '양념치킨': 12000 };

  constructor (name, no) {
    this.name = name;
    if (no) this.no = no;
  }
  introduce () {
      console.log("==");
      console.log(this);
      console.log("==");
    return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
  }
  order (name) {
    return `${this.menu[name]}원입니다.`
  }
}

class ConceptYalcoChicken extends YalcoChicken {
  #word = '';
  constructor (name, no, word) {
    super(name, no);
    this.#word = word;
  }
  introWithConcept () {
    return super.introduce() + ' ' + this.#word;
  }
  order (name) {
    return super.order(name) + ' ' + this.#word;
  }
}

const pikaChain = new ConceptYalcoChicken('도봉', 50, '피카피카~');
```

```javascript
console.log(pikaChain);
console.log(pikaChain.introWithConcept());
console.log(pikaChain.order('후라이드'));

//첫번째 줄 결과
//ConceptYalcoChicken {no: 50, menu: {…}, name: '도봉', #word: '피카피카~'}
//menu: {후라이드: 10000, 양념치킨: 12000}
//name: "도봉"
//no: 50
//#word: "피카피카~"
//[[Prototype]]: YalcoChicken
//	constructor: class ConceptYalcoChicken
//	introWithConcept: ƒ introWithConcept()
//	order: ƒ order(name)
//	[[Prototype]]: Object
//		constructor: class YalcoChicken
//		introduce: ƒ introduce()
//		order: ƒ order(name)
//      [[Prototype]]: Object

//두번째 줄 결과
//==
//ConceptYalcoChicken {no: 50, menu: {…}, name: '도봉', #word: '피카피카~'}
//==
    
//세번째 줄 결과
//안녕하세요, 50호 도봉점입니다! 피카피카~
//10000원입니다. 피카피카~
```

=> super는 크게 2가지 용도로 활용됨을 알 수 있다.

* 자식 클래스의 constructor 내부에서 사용 시 -> 부모 클래스의 constructor를 가리킴
* 자식 클래스의 method 내부에서 사용 시 -> 부모 클래스를 가리킴



정적 메서드와 정적 프로퍼티에서도 동일한 방식으로 상속이 적용된다.

```javascript
class YalcoChicken {
  static brand = '얄코치킨';
  static contact () {
    console.log(`${this.brand}입니다. 무엇을 도와드릴까요?`);
  }
}

class ConceptYalcoChicken extends YalcoChicken {
  static contact () {
    super.contact(); //현재 this는 ConceptYalcoChicken 클래스이며, __proto__ 속성의 값(객체)는 YalcoChicken 클래스 그 자체를 가리키므로, YalcoChicken 클래스 객체의 contact() 가 호출된다.
    console.log('컨셉 가맹문의는 홈페이지를 참조하세요.');
  }
}

ConceptYalcoChicken.contact();
//얄코치킨입니다. 무엇을 도와드릴까요?
//컨셉 가맹문의는 홈페이지를 참조하세요.
```

* (내가 느끼기에) 관심있게 파악한 사항

  * 위 코드에서 ConceptYalcoChicken의 contact() 함수 내부에서, super.contact() 를 호출하면, 궁극적으로 아래의 과정이 펼쳐진다.

    * YalcoChicken의 contact() 함수 호출

      * 이 때, 이 contact() 함수 내부에서의 this는 "ConceptYalcoChicken 클래스 그 자체의 객체"를 가리킨다.

      * 그런데 ConceptYalcoChicken 클래스를 console.dir() 로 파악하면, brand 프로퍼티가 존재하지 않는다.

        * 더 정확히는, `ConceptYalcoChicken.__proto__ ` 속성에 brand 프로퍼티가 존재하며 이는 `ConceptYalcoChicken.__proto__.brand` 로 접근이 가능.

          => 이는 ConceptYalcoChicken.brand 로도 접근이 가능

  * 위의 과정을 통해서 아래의 결론을 도출하였다.

    * 클래스의 상속 과정은, new 연산자를 만든 객체에서의 상속과 다르게, 부모 클래스의 값 프로퍼티를 자식 클래스로 당겨오는 과정이 존재하지 않는다

      => (내 생각) 객체에서는, 부모 객체를 만들지 않고 자식 객체만으로 부모 객체의 프로퍼티를 활용해야 했기에 부모 객체의 값 프로퍼티를 다 가져오는 과정이 포함된다고 생각함

      => 반면, 클래스에서는, 이미 부모 클래스와 자식 클래스가 모두 메모리 상에 존재하기 때문에, 굳이 위의 과정이 필요하지 않다고 생각함.

      => 자식 클래스에서 부모 클래스의 property를 조회하기를 원할 때, 자식 객체의 `__proto__`를 통해서 (암묵적으로도) 조회가 가능하다는 사실은, 위의 생각을 뒷받침한다.



### 객체의 스프레드와 디스트럭쳐링

스프레드

```javascript
const class1 = {
  x: 1, y: 'A', z: true
};

const class2 = { ...class1 };

// 아래의 참조복사 코드와 다름!
// const class2 = class1;

console.log(class2);
```

=> class1과 class2는 다른 객체이다.



스프레드는, 특정 객체의 프로퍼티를 포함하는 다른 객체 생성에도 유용하다.

```javascript
const class1 = {
  a: 1, b: 'A', c: true
};
const class2 = {
  d: { x: 10, y: 100 }, e: [1, 2, 3]
};
const class3 = {
  ...class1, z: 0
}
const class4 = {
  ...class2, ...class3, ...class2.d
}

console.log(class4);
//{d: {…}, e: Array(3), a: 1, b: 'A', c: true, …}
//	a: 1
//	b: "A"
//	c: true
//	d: {x: 10, y: 100}
//	e: (3) [1, 2, 3]
//	x: 10
//	y: 100
//	z: 0
//	[[Prototype]]: Object
```



중복되는 프로퍼티는, 뒤의 것으로 덮어씌워진다.

```javascript
const class1 = {
  ...{ a: 1, b: 2 },
  ...{ b: 3, c: 4, d: 5 },
  ...{ c: 6, d: 7, e: 8 }
}

console.log(class1);
```



(스프레드 활용 시) 기본적으로 shallow copy가 일어난다.

```javascript
const class1 = {
  x: 1,
  y: { a: 2 },
  z: [3, 4]
};

const class2 = { ...class1 };
class1.x++;
class1.y.a++;
class1.z[0]++;
```

=> class1과 class2 객체는, 객체 프로퍼티에 대해서는 동시에 변경된다. (shallow copy이기 때문)





디스트럭쳐링

=> 식별자에 해당하는 값을 가져온다.

=> 객체에서, 모든 (또는 특정한) 프로퍼티의 값을 받아올 때 활용한다.



아래의 코드는 모두 같은 코드이다.

```javascript
const obj1 = {
  x: 1, y: 2, z: 3
};

const x = obj1.x;
const y = obj1.y;
const z = obj1.z;

console.log(x, y, z);
```

```javascript
const obj1 = {
  x: 1, y: 2, z: 3
};

const {x, y, z} = obj1;

console.log(x, y, z);
```

아래의 경우는 일부만 가져오는 기능이다.

```javascript
const obj1 = {
  x: 1, y: 2, z: 3
};

const {x, z} = obj1;

console.log(x, z);
```

함수에서도 디스트럭쳐링이 활용될 수 있다.

```javascript
// 디스트럭쳐링 (적절히 활용)
function introduce({age, married, job, name}) {
  // 순서 무관
  // 이 프로퍼티들을 갖는 객체를 인자로 받겠다는 의도 드러냄

  console.log(`제 이름은 ${name}, `
    + `나이는 ${age}세구요. `
    + `직업은 ${job}, `
    + `${married ? '기혼' : '미혼'}입니다.`
  )
}

const person1 = {
  job: '개발자',
  age: 28,
  married: false,
  name: '김철수',
  blood: 'O'
};

introduce(person1);
```

** 그리고 배열에서, length 프로퍼티는 기본적으로 존재



## 섹션6. 주요 빌트인 객체

### 전역 객체와 표준 빌트인 객체

전역 객체

* 전역 범위에 항상 존재하는 객체

  * 브라우저에서는, console.log(this)를 쳐 보면 알 수 있다.
  * 브라우저의 것이랑, node.js의 것이 다르다.
  * console.log(this)를 콘솔에서 쳐 보고, node.js 터미널(REPL)에서 쳐보고, node.js에서 문서로 실행해보면 다른 결과가 나타난다.

* 표준 빌트인 객체

  * 환경에 관계없이 제공해야만 하는 것들

* 호스트 객체

  * 각 환경에서 제공하는 기타 객체들

    => 브라우저의 Web API, Node.js API 등등에서 제공하는 객체들. 

* (브라우저 한정) 전역으로 설정한 var 변수와 전역 함수

  * globalThis.(const변수) => 읽어낼 수 없다.
  * (내  생각) - 이는 hoisting 시, variable Environment에 저장되는 변수/함수 만 다루겠다는 의미와 관련될 거 같다는 생각. 

  ```javascript
  var myGlobalVar = 1;
  const myGlobalConst = 1;
  
  function myGlobalFunc () {};
  
  console.log(
    globalThis.myGlobalVar, //1이 출력되며, myGlobalVar 프로퍼티가 전역객체의 프로퍼티로서도 추가된다.
    globalThis.myGlobalConst, //undefined로 나타난다.
    globalThis.myGlobalFunc //myGlobalFunc 프로퍼티가 전역객체의 프로퍼티로서 추가된다.
  );
  ```





참고할 만한 사항

* node.js에서 console.log(global);을 실행 시, 표준 빌트인 객체는 안 나오고 node.js에서 제공하는 API만 출력됨을 확인할 수 있다.
  * 하지만, console.log(globalThis.isNaN) 을 입력 시, Function으로서 isNaN 프로퍼티가 존재함을 확인할 수 있다.
  * => 객체를 조회해서 프로퍼티가 조회되지 않고, 실제 프로퍼티를 직접 조회해야 확인이 되는 점은 좀 의아하기는 하다. (내 생각)



표준 빌트인 객체

* ECMAScript 사양에 정의된 객체들

* boolean, Infinity, isNaN 등은 표준 빌트인 객체이므로, 그냥 가져다 쓸 수 있었던 거임

  ```javascript
  // 그러나 요소들로 갖고 있는 것은 확인 가능
  console.log(globalThis.Infinity);
  console.log(globalThis.isNaN);
  console.log(globalThis.Object);
  ```

  => globalThis를 생략해도 된다.



래퍼 객체 

원시 값이 프로퍼티를 활용할 수 있는 이유는, 프로퍼티를 호출할 때 일시적으로 wrapper 객체로서 작동을 하며, 호출이 끝나고 나면 다시 원시 타입으로 돌리기 때문이다. (메모리 절약!)

```javascript
const str = 'abcde';
console.log(
  str.length,
  str.toUpperCase(),
  str[0]
);
```

```javascript
const num = 123.4567;
console.log(
  typeof num.toString(), //string
  num.toFixed(2)
);
```

비교를 위해 아래의 코드를 실행

```javascript
const str = new String('abcde'); //Object
const num = new Number(123.4567); //Object
const bool = new Boolean(true); //Object

console.log(str.valueOf()); //abcde
console.log(num.valueOf()); //123.4567
console.log(bool.valueOf()); //true
```



### 빌트인 전역 프로퍼티와 함수

eval은 쓰지 말 것.

(eval은 문자를 받아서 js로 해석하는 과정이다. 이는, 실제로 코드로서 실행하는 과정을 생략하는 등 최적화 과정이 없으므로 속도가 떨어지게 된다.)

```javascript
//아래의 과정은, 이제는 엣지 브라우저 기준에서 에러가 뜬다. (eval 함수를 허용하지 않음)

const x = eval('1 + 2 + 3');

// 객체나 함수의 리터럴은 괄호로 감싸야 함
const obj = eval('({a: 1, b: 2})');

console.log(x, obj);
```

```javascript
//아래의 과정은, 이제는 엣지 브라우저 기준에서 에러가 뜬다. (eval 함수를 허용하지 않음)

const code = `
  let x = 1;
  console.log(x++, x);
`;

eval(code);
```



isFinite() 기능

```javascript
//true
console.log(
  isFinite(1),
  isFinite(0),
  isFinite('1'),
  isFinite(null)
);
```

```javascript
//false
console.log(
  isFinite(1/0),
  isFinite(Infinity),
  isFinite(-Infinity),
  isFinite(NaN),
  isFinite('abc')
);
```



parseFloat() => 인자로 받은 값을 실수로 변환. + 숫자로 시작하면 읽을 수 있는 부분까지 반환

=> 그 외의 경우는 NaN을 반환

```javascript
console.log(
  parseFloat(123.4567),
  parseFloat('123.4567'),
  parseFloat(' 123.4567 ')
);

//123.4567
//123.4567
//123.4567
```

```javascript
console.log(
  parseFloat('123.0'),
  parseFloat('123'),
  parseFloat(' 123ABC '),
  parseFloat([123, 456, 789])
);

//123
//123
//123    //문자열의 앞뒤 공백 무시
//123	 //배열의 맨 첫번째 요소의 숫자
```

```javascript
//NaN
console.log(
  parseFloat('ABC123'),
  parseFloat({x: 1}),
  parseFloat([]),
  parseFloat(['a', 1, true])
);
```



parseInt() => 인자로 받은 값을 정수(type은 Number)로 반환 + 2번째 인자로 숫자 n을 받으면, n진법으로 해석해서 10진법의 결과물로 반환해준다.

```javascript
console.log(
  parseInt('11'),
  parseInt('11', 2),
  parseInt('11', 8),
  parseInt('11', 16),
  parseInt('11', 32),

  parseInt('11', 37),
  parseInt('11', 'A'),
);
```

```javascript
console.log(
  parseInt('abc'),
  parseInt('{}'),
  parseInt('[]')
);
```



encodeURI(), encodeURIComponent()

* encodeURI() 는 전체 URI를 받을 것을 기대(가정)하고 인코딩 수행
  * ?, =, & (특정 기능 수행)을 인코딩하지 않는다. 
* 반면, encodeURIComponent()는 요소를 인코딩한다. 
  * 아래의 경우는, "얄코"만 인자로 넘겨야 한다.
  * ?=얄코를 통째로 넘기면, `?` 와 `=` 도 인코딩이 된다. (encodeURI() 함수와의 차이.)

```javascript
const searchURI = 'https://www.google.com/search?q=얄코';
const encodedURI = encodeURI(searchURI);

console.log(encodedURI);

//https://www.google.com/search?q=%EC%96%84%EC%BD%94

//즉, URI를 아래의 규칙으로 인코딩한다.
//	=> 아스키 문자는 그대로, 그리고 아스키가 아닌 문자와 "일부" 특수문자는 아스키 코드로 인코딩한다  
```

```javascript
const keyword = '얄코';
const encodedKeyword = encodeURIComponent(keyword);

console.log(encodedKeyword);
//%EC%96%84%EC%BD%94

const searchURI = `https://www.google.com/search?q=${encodedKeyword}`;
console.log(searchURI);
//https://www.google.com/search?q=%EC%96%84%EC%BD%94
```

