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



### String 객체

```javascript
const fromNum = new String(123);
const fromBool = new String(true);
const fromArr = new String([1, 'A', false]);
const fromObj = new String({a: 1});

console.log(typeof fromNum, fromNum);
console.log(typeof fromBool, fromBool);
console.log(typeof fromArr, fromArr);
console.log(typeof fromObj, fromObj);

//object String {'123'}
//		0: "1"
//		1: "2"
//		2: "3"
//		length: 3
//      [[Prototype]]: String
//      [[PrimitiveValue]]: "123"
//object String {'true'}
//object String {'1,A,false'}
//object String {'[object Object]'}
```

```javascript
//원시값으로 반환
//따라서, 아래의 타입은 모두 'string'이다.
console.log(fromNum.toString());
console.log(fromBool.toString());
console.log(fromArr.toString());
console.log(fromObj.toString());
```

=> 인자로 받은 값을 감싸서 String 객체로 반환

** new 없이 객체를 생성 시, 타입이 다름을 확인할 수 있다. (문자열 그 자체로 반환된다.)

```javascript
const str1 = String('Hello World!');
const str2 = String(123);
const str3 = String(true);
const str4 = String({x: 1, y: 2}); // 💡 [object Object]
const str5 = String([1, 2, 3]); // 💡 1,2,3

console.log(typeof str1, str1);
console.log(typeof str2, str2);
console.log(typeof str3, str3);
console.log(typeof str4, str4);
console.log(typeof str5, str5);

//string Hello World!
//string 123
//string true
//string [object Object]
//string 1,2,3

```



유사 배열 객체

=> 내용을 바꿀 수 없다는 점 외에는, 배열의 기능을 대동소이하게 수행한다.

=> String은 원시값이므로, [] 접근이나 인스턴스 메서드로 특정 글자만 수정하는 것이 불가능하다. (조금 더 깊게 파헤쳐보고 싶음) 

<u>=> (내 생각) primitive 값은 그 자체로 저장이 되기 때문에, 해당 값의 일부분을 변경하려고 하면 메모리 상의 아예 다른 곳에 변경 이후의 primitive 값이 저장되지 않나 싶다.</u>

```javascript
let myStr = '안녕하세요!';

console.log(
  myStr.length,
  myStr[0],
  myStr[myStr.length - 1]
);
```

```javascript
myStr[myStr.length - 1] = '?';
console.log(myStr); // 💡 배열과 달리 그대로 //'안녕하세요!'
```



주요 인스턴스 메서드

toUpperCase, toLowerCase, charAt, at, indexOf, lastIndexOf, includes, startsWith, endsWith, search, substring, slice, split, trim, repeat, replaceAll

* at은 음수로 뒤에서부터 접근 가능 (-1부터)

  * splitted.at(-1) 로도 쓸 수 있다.

* 정규식을 활용한 search 메서드의 예

  ```javascript
  console.log(
    '하루가 7번 지나면 1주일이 되는 거야.'.search(/[0-9]/),
    '하루가 일곱 번 지나면 일주일이 되는 거야.'.search(/[0-9]/)
  );
  
  //4
  //1
  ```

  

* split 주목

  ```javascript
  console.log(
    '010-1234-5678'.split('-'),
    'ABC1DEF2GHI3JKL'.split(/[0-9]/)
  )
  
  //['010', '1234', '5678']
  //['ABC', 'DEF', 'GHI', 'JKL']
  
  // 인자로 빈 문자열을 넣거나 인자 생략시
  const word = '안녕하세요';
  
  console.log(
    word.split(''),
    word.split()
  );
  
  //['안', '녕', '하', '세', '요']
  //['안녕하세요']
  ```

  두번째 인자로 split() 함수의 return 결과물의 출력하고싶은 길이를 받을 수 있다.

  ```javascript
  const word = '하나 하면 할머니가 지팡이 짚고서 잘잘잘';
  
  console.log(
    word.split(' ', 2),
    word.split(' ', 4)
  );
  
  //['하나', '하면']
  //['하나', '하면', '할머니가', '지팡이']
  ```

* replace, replaceAll 주목

  * replaceAll은 정규표현식으로 인자를 넘기지 않아도, 마치 정규표현식을 인자로 받은 것처럼 실행되는 것이 replace와의 차이점

    ```javascript
    const word = '밥 좀 먹자, 밥. 응? 야, 밥 좀 먹자고 밥, 밥!';
    
    console.log(word.replace('밥', '라면'));
    console.log(word.replace(/밥/g, '라면'));
    
    //라면 좀 먹자, 밥. 응? 야, 밥 좀 먹자고 밥, 밥!   
    //	=> 즉, 첫번째 부분의 밥만 치환된다.
    
    //라면 좀 먹자, 라면. 응? 야, 라면 좀 먹자고 라면, 라면!
    //	=> 모든 부분의 밥이 치환되며, 이 때 정규식을 활용한다.
    ```

    ```javascript
    console.log(word.replaceAll('밥', '라면'));
    console.log(word.replaceAll(/밥/g, '라면'));
    
    //라면 좀 먹자, 라면. 응? 야, 라면 좀 먹자고 라면, 라면!
    //라면 좀 먹자, 라면. 응? 야, 라면 좀 먹자고 라면, 라면!
    
    //	=> 즉, replaceAll() 함수를 쓰게 되면, 인자로 문자열을 넘겨받아도 마치 정규식을 넘겨받은 것처럼 동작한다
    ```

    정규표현식으로 써야, 모든 "밥"이 "라면" 으로 치환된다. (단, replaceAll() 을 쓸 경우, 정규표현식을 쓰지 않아도 된다.)



메서드 체이닝

* 메서드 체이닝을 안 쓴다면, 코드가 굉장히 지저분해진다.

  ```javascript
  const word = ' 모두 HELLO! ';
  const rpFrom = 'hello';
  const rpTo = 'bye';
  
  console.log(
    word
    .trimStart()                // '모두 HELLO! '
    .toLowerCase()              // '모두 hello! '
    .replaceAll(rpFrom, rpTo)   // '모두 bye! '
    .toUpperCase()              // '모두 BYE! '
    .repeat(3)                  // '모두 BYE! 모두 BYE! 모두 BYE! '
    .trimEnd()                  // '모두 BYE! 모두 BYE! 모두 BYE!'
  );
  ```



### Number 객체

```javascript
// 특정 숫자값으로 인식되는 것
console.log(
  new Number('-123.4567'), // Number {-123.4567}
  new Number('Infinity'),  // Number {Infinity}
  new Number(true),		   // Number {1}
  new Number(false)		   // Number {0}
);

// Number {NaN} 으로 반환된다.
console.log(
  new Number('1/2'),
  new Number('123ABC'),
  new Number('ABC'),
  new Number('{a: 1, b: 2}'),
  new Number([1, 2, 3])
);

const num1 = Number('123');
const num2 = Number('-123.45');
const num3 = Number(true);
const num4 = Number(false);
const num5 = Number(null);


console.log(typeof num1, num1); //number 123
console.log(typeof num2, num2); //number -123.45
console.log(typeof num3, num3); //number 1
console.log(typeof num4, num4); //number 0
console.log(typeof num5, num5); //number 0
```



정적 프로퍼티

* EPSILON
  * 정의 : Number 형으로 표현 가능한 1보다 큰 수 중, 가장 작은 수 - 1
    * 즉, 부동소숫점 계산의 오차를 해결하기 위해서 사용된다.


```javascript
console.log((0.1 + 0.2) - 0.3 < Number.EPSILON) //true
```

* 그외 기능들
  * `Number.MAX_SAFE_INTEGER` 과 `Number.MIN_SAFE_INTEGER` 는 부동 소숫점 체계에서 "안정적으로"나타낼 수 있는 가장 큰 수와 작은 수를 의미한다고 한다. 


```javascript
console.log(Number.MAX_VALUE);
console.log(Number.MIN_VALUE);

console.log(Number.MAX_SAFE_INTEGER);
console.log(Number.MIN_SAFE_INTEGER);

console.log(Number.POSITIVE_INFINITY);
console.log(Number.NEGATIVE_INFINITY);

console.log(Number.NaN);
```



정적 메서드

```javascript
//2개의 메서드 차이는, 타입 변환을 암묵적으로 하냐 안 하냐의 차이

console.log(
  isFinite(null), //true // null을 0으로 변환 //전역 객체 메서드
  Number.isFinite(null) //false
);

console.log(
  isNaN('abc'), //true // 숫자타입의 NaN으로 변환 //전역 객체 메서드
  Number.isNaN('abc') //false // 숫자타입 자체가 아니므로 false
);

```

이외 수많은 정적 메서드



인스턴스 메서드

* toExponential()
  * 어떠한 실수를 a * 10^n 꼴로 나타낸다.

```javascript
const numInExp = (123.456789).toExponential();
console.log(
  typeof(numInExp), numInExp
);
//string 1.23456789e+2

// 인자로 자릿수 제한
console.log(
  (123.456789).toExponential(2),
  (123.456789).toExponential(4),
  (123.456789).toExponential(6)
);
//1.23e+2 1.2346e+2 1.234568e+2

console.log(
  // 인자가 없으면 0을 받은 것과 같음
  (111.234567).toFixed(),
  (111.234567).toFixed(0),
  (111.234567).toFixed(1)
);
//111 111 111.2

console.log(
  // 인자가 없으면 toString처럼 그대로 문자열로 반환
  (1234.56789).toPrecision()
);
//1234.56789

// 인자가 정수부 자릿수보다 적으면 지수로
console.log(
  (1234.56789).toPrecision(1),
  (1234.56789).toPrecision(2),
  (1234.56789).toPrecision(3),
  (1234.56789).toPrecision(6)
);
//1e+3 1.2e+3 1.23e+3 1234.57

// 반올림
console.log(
  (1234.56789).toPrecision(4),
  (1234.56789).toPrecision(6),
  (1234.56789).toPrecision(8)
);
//1235 1234.57 1234.5679

//10진법의 수를 n진법으로 바꾸어서 문자열로 출력
console.log(
  (11).toString(),
  (11).toString(2),
  (11).toString(8),
  (11).toString(16)
);
//11 1011 13 b
```



//부동소숫점을 다룰 때, 실전에서는, 라이브러리를 사용

//toFixed()를 적용했을 때, Number 형태로 받고 싶다면 Number()로 감싸거나, Object 형태로 받고 싶다면 new Number() 로 감싸기.



* 그 외 의문사항들

  * 컴퓨터 내부에서 +와 *의 원리가 다르게 적용되는 듯 하다.

    * 단적인 예로, 아래의 코드를 보자

      ```javascript
      console.log(0.3+0.3+0.3+0.3+0.3+0.3+0.3+0.3+0.3+0.3 == 3); //false
      console.log(0.3*10 == 3); //true
      ```

    * 아래 사이트가 그 해답이 되지 않을까 싶다

      * 곱하기와 더하기의 원리가 미세하게 차이나서? 그러지 않을까 생각한다
      * 출처 : https://beramodo.tistory.com/1



### Math 객체

생성자 함수로 작동하지 않음. 

Number 타입만 지원하며, BigInt는 사용 불가



//난수 생성 시, 보다 더 엄격한 메서드를 쓸 것을 권함.



```javascript
for (let i = 0; i < 10; i++) {
  console.log(Math.random());
}
```



### Date 객체

```javascript
const now = new Date();

console.log(typeof now); //object
console.log(now); //Mon Oct 09 2023 17:54:03 GMT+0900 (한국 표준시)
```

의문사항 

* Date 함수는 인자를 여러 개 받을 수 있던데, 원리가 어떻게 될까

  * 우선 Date 함수는 아래와 같이 여러 개의 인자를 받을 수 있다.

    ```javascript
    new Date();
    new Date(value);
    new Date(dateString);
    
    new Date(year, monthIndex);
    new Date(year, monthIndex, day);
    new Date(year, monthIndex, day, hours);
    new Date(year, monthIndex, day, hours, minutes);
    new Date(year, monthIndex, day, hours, minutes, seconds);
    new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds);
    ```

    * 출처 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/Date

  * 하지만 콘솔창에 Date 객체를 찍어보면, 아래와 같이 인자를 받지 않은 함수임을 알 수 있다.

    ```javascript
    console.log(Date);
    //ƒ Date() { [native code] }
    ```

    => native 코드로 이루어져 있어서, 해당 부분까지 파악하기에는 너무 깊은 level이라고 판단함.

    => 그러나, 코드 내부적으로 인자를 여러개 받았을 때 무언가.... 대처하는 코드가 있지 않을까 싶다.

    

핵심은, 현재 시간을 UTC 방식이나 한국식 방식으로 표현 시, 어떤 차이가 있는지에 관한 것이다. 

```JAVASCRIPT
console.log(Date.now()); //현재의 시스템 시간(한국 시간)이 나온다.
```

```JAVASCRIPT
//첫번째 코드는 UTC시간을 형성한다.
////따라서, Date.parse('January 1, 1970 00:00:00 UTC') 입력시 0이 나온다.
console.log(
  Date.parse('August 20, 2022 00:00:00 UTC')
);

//두번째 코드는 한국시간을 형성하므로, UTC시간으로 변환시 -9시간 이 적용된다.
//따라서, Date.parse('January 1, 1970 00:00:00') 입력시 0이 아니라 시차만큼(ms) 나온다.
console.log(
  // 💡 시스템(실행 컴퓨터) 시간이 한국이면 시차 9시간 적용
  Date.parse('August 20, 2022 09:00:00')
);

//아래의 코드는, 정확히 UTC 시간대를 형성하므로, Date.UTC(1970,0,0,0,0,0) 을 입력하면 결과값이 0이 된다.
console.log(
  // ⭐️ 월은 0부터 시작
  Date.UTC(2022, 7, 20, 0, 0, 0)
);

//밀리초는 화면상으로는 나타내지 않는다.
```



인스턴스 메서드

```javascript
const now = new Date();

console.log(
  now.toString()
); //시스템 언어 설정대로, 날짜와 시간이 문자열 형식으로 출력된다.
// 결과 : Thu Jun 22 2023 13:03:09 GMT+0900 (한국 표준시)
```

```javascript
//날짜를 언어 형식에 따라 다르게 나타내기
//현재 웹브라우저에서는, 한국에서 사용하는 날짜와 시간 방식을 기본으로 채택하므로, toLocaleString() 에 아무 인자도 넘기지 않아도 된다.

console.log(
  now.toLocaleString()
);

console.log(
  now.toLocaleString('ko-KR')
);

console.log(
  now.toLocaleString('en-US')
);

//2023. 10. 9. 오후 9:40:13
//2023. 10. 9. 오후 9:40:13
//10/9/2023, 9:40:13 PM
```



그리고, Date 객체를 활용해서 년,월,일,시간 정보를 조회/수정할 수 있다. (getter, setter 메서드 활용)

```javascript
const now = new Date();

const year = now.getFullYear();
const month = now.getMonth() + 1;
const date = now.getDate();
const day = '일월화수목금토'[now.getDay()];

console.log(
  `오늘은 ${year}년 ${month}월 ${date}일, ${day}요일입니다.`
);
```



또한, getTime과 setTime을 이용하여 밀리초 숫자값을 얻을 수 있다.

```javascript
const date1 = new Date(2020, 7, 20);
const date1value = date1.getTime();

console.log(date1.toString());
console.log(date1value);
```

```javascript
const date2 = new Date();

console.log(date2.toString());
```

```javascript
date2.setTime(date1value);

console.log(date2.toString());
```



그리고 UTC 시간과 시스템의 시간대에 대한 차이를 getTimezoneOffset() 으로 획득하고, 이를 이용하여 UTC 기준의 시간을 시스템 시간대로 바꿔보자

```JAVASCRIPT
const now = new Date();
const timezoneOffset = now.getTimezoneOffset() * 60 * 1000; //밀리세컨 반환

const isoStr = new Date(now.getTime() - timezoneOffset).toISOString(); //시스템 시간대로 변환


console.log(isoStr); //시스템 시간(한국시간대)로 변환 //2023-10-09T21:40:13.596Z
console.log(now.toString()); // Mon Oct 09 2023 21:40:13 GMT+0900 (한국 표준시)

//isoStr.split('T'); 를 활용해서 날짜 parsing을 할 수 있다.
```



## 섹션 7. 배열

### 자바스크립트 배열의 특징과 생성

자바 스크립트의 배열은 아래의 "특별한" 특징이 있다.

* 연속 나열이 아닌 편이다. (엔진에 따라 다를 수 있음 ) 
  * 해쉬 테이블로 구현되어 있다.
  * 특정 배열은 그렇기도 하지만 다루지 않겠음

* 한 배열에 다양한 자료형의 데이터가 들어갈 수 있다.
* 접근이 느림. but, 중간 요소의 추가나 제거는 빠름



배열을 생성할 때는 아래의 과정을 거친다.

* 배열 리터럴, 생성자 함수

* 출처
  * [Array() 생성자 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Array)



배열 리터럴

```javascript
const arr1 = []; // 빈 배열
const arr2 = [1, 2, 3];
const arr3 = [1, , 2, , 3] // 빈 요소(undefined) 표함 배열 생성

console.log(arr1.length, arr1);
console.log(arr2.length, arr2);
console.log(arr3.length, arr3);

// 0 []
// 3 (3) [1, 2, 3]
// 5 (5) [1, 비어 있음, 2, 비어 있음, 3]

console.log(arr3[1]); 
//undefined          => 빈 요소를 조회할 때 발생
```



생성자 함수

* 확인해보니, Array 또한 native code이다.

```javascript
const arr = new Array();

console.log(arr);
console.log(arr.length);

//[]
//0
```

```javascript
//숫자 1개짜리 인자를 전달받으면, 아래와 같이 빈 배열이 만들어진다

const arr = new Array(3); //길이 3짜리 빈 배열이 만들어짐.

console.log(arr);
console.log(arr.length);

// [빈 ×3]
// 3
```



```javascript
//인자가 2개 이상이거나, 숫자가 아닌 인자를 전달받는 경우

const arr1 = new Array(1, 2, 3);
const arr2 = new Array('ABC');
const arr3 = new Array(true);

console.log(arr1); //길이 3짜리 배열이 만들어짐
console.log(arr2); //길이 1짜리 배열이 만들어짐
console.log(arr3); //길이 1짜리 배열이 만들어짐

//(3) [1, 2, 3]
// ['ABC'] 
// [true]
```



정적 메서드 of

* Array.of() 를 활용해서도 새로운 Array 객체를 생성할 수 있다.
  * 생성자 함수 Array를 통해 Array 객체를 생성하는 것과의 "유일한" 차이는, 인자로 하나의 숫자만 받는 경우이다.

```javascript
// 인자가 하나의 숫자라도 이를 요소로 갖는 배열 생성
const arr1 = Array.of(3);

const arr2 = Array.of(1, 2, 3);
const arr3 = Array.of('ABC', true, null);

console.log(arr1);
console.log(arr2);
console.log(arr3);

// [3]
// [1,2,3]
// ['ABC', true, null]
```



정적 메서드 from

* 인자로서 배열, 유사배열, 이터러블 객체를 받아서 shallow copy한 객체를 반환

  * 또한, 위에서 받은 인자의 각 요소를 순회하여, 적당히 가공된 배열/유사배열/이터러블 객체를 반환할 수도 있다.

    => 이것은 인자로서 화살표 함수를 추가로 받아서 구현한다.

* 출처 : [Array.from() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

```javascript
const arr1 = Array.from([1, 2, 3]);
const arr2 = Array.from('ABCDE');
const arr3 = Array.from({
  '0': true,
  '1': false,
  '2': null,
  length: 3
});

console.log(arr1);
console.log(arr2);
console.log(arr3);

// [1,2,3]
// ['A', 'B', 'C', 'D', 'E']
// [true, false, null]
```

=> 배열, 유사배열객체, 이터러블을 인자로 받아서 배열로 반환한다.

=> 유사배열객체를 Array.from()을 하게 되면, for ~ of문을 쓸 수 있게 된다. (배열로 바뀌었으므로.)

```javascript
const arrLike = {
  0: '🍎',
  1: '🍌',
  2: '🥝',
  3: '🍒',
  4: '🫐',
  length: 5
};

// 일반 for문으로 순회 가능
for (let i = 0; i < arrLike.length; i++) {
  console.log(arrLike[i]);
}
```

```javascript
// 배열은 이터러블, 성능도 향상
for (const item of Array.from(arrLike)) {
  console.log(item);
}
```



Array.from() => 얕은 복사기능도 수행한다.

```javascript
const arr1 = [1, 2, 3];
const arr2 = Array.from(arr1);
arr2.push(4);

console.log(arr1, arr2);
//[1,2,3] [1,2,3,4]
```

```javascript
//얕은 복사
const arr1 = [{x: 1}, {x: 2}];
const arr2 = Array.from(arr1);
arr2.push({x: 3});

// 참조타입 요소의 내부값이 바뀔 경우
arr1[0].x = 0;
console.log(arr1, arr2);

// [{x:0}, {x:2}] [{x:0}, {x:2}, {x:3}]
```



Array.from()의 두번째 인자로서, 매핑 함수를 받아서 아래와 같이 조작이 가능하다.

```javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = Array.from(arr1, x => x + 1);
const arr3 = Array.from(arr1, x => x * x);
const arr4 = Array.from(arr1, x => x % 2 ? '홀' : '짝');

console.log(arr2); //[2,3,4,5,6]
console.log(arr3); //[1,4,9,16,25]
console.log(arr4); //['홀', '짝', '홀', '짝', '홀']
```



### 배열의 기본 메서드들

//Array.isArray 가 더 권장된다. (iframe에서도 작동되므로)

=> instanceof Array 와의 차이점은, Array.prototype 을 false/true로 해석하는 차이가 있다.

*=> (내 생각) 직접 `console.log(Array.prototype)` 을 찍으면, `__proto__` 의 타입이 Object라고 뜨는 것이 원인이 아닐까 싶다.*

*=> `console.log(new Array(8,2))` 를 찍어보면, `__proto__` 프로퍼티가 정확하게 Array.prototype 을 가리키는 것이 하나의 힌트가 되지 않을까 생각한다.*

```javascript
const arrays = [
  [], [1, 2, 3], new Array(),
  // ⚠️ instanceof에서는 결과가 다름
  Array.prototype // 배열임
];

const notArrays = [
  1, 'abc', true, null, {}
];

for (const item of arrays) {
  console.log(
    item,
    Array.isArray(item),
    item instanceof Array
  );
}

// [] true true
// [1, 2, 3] true true
// [] true true
// [constructor: ƒ, at: ƒ, concat: ƒ, copyWithin: ƒ, fill: ƒ, …] true false
```

그 외 메서드

at, includes, indexOf, lastIndexOf, join

=> 배열의 특정 원소를 찾거나, 해당 원소의 index를 찾거나, 구분자를 사용하여 배열의 요소들을 string으로 표현할 때 사용한다.

```javascript
//includes()
//true,false,false,false
//참조형 데이터의 경우, 주솟값이 다르다.

const obj1 = { x: 1, y: 2 };
const obj2 = { x: 1, y: 2 };

const arr = [
  obj1,
  { x: 3, y: 4 }
];

console.log(
  arr.includes(obj1),
  arr.includes(obj2),
  arr.includes({ x: 1, y: 2 }),
  arr.includes({ x: 3, y: 4 })
);
//true false false false
//	console.log(arr[1] === { x: 3, y: 4 }) 가 false가 나온다.
//	=> 아마, 메모리 주소로서 접근하는 것이 아닌가 생각된다.
```

join() 메서드는 아래와 같이 쓸 수 있다.

* 특이한 점은, 요소로서 객체가 들어가는 경우에는 [object Object]로 읽어들인다

  => (내 생각) 해당 변수에 들어있는 값으로 판단하는 것이 아닌가 생각된다.

  (값이 primitive value이면 그대로 값을 취하나, 그렇지 않고 메모리 주소값인 경우에는 [object Object]나 배열의 문자화로 취급하는 것이 아닐까 생각한다.)

 ```javascript
//join()

const arr1 = ['a', 'b', 'c', 'd', 'e'];
const arr2 = [
  1, true, null, undefined, '가나다', { x: 0 }, [1, 2, 3]
];

console.log(
  arr1.join() // 인자가 없다면 쉼표`,`로
);
//a,b,c,d,e

console.log(
  arr1.join('')
);
//abcde

console.log(
  arr1.join(' ')
);
//a b c d e

console.log(
  arr2.join(':')
);
//1:true:::가나다:[object Object]:1,2,3
 ```

활용 예시

```javascript
console.log(
  classIntro(3, '김민지', '영희', '철수', '보라')
); // 호이스팅

function classIntro (classNo, teacher, ...children) {

  // [ 4-3강 예제 ]

  // let childrenStr = '';
  // for (const child of children) {
  //   if (childrenStr) childrenStr += ', ';
  //   childrenStr += child;
  // }
  // return `${classNo}반의 선생님은 ${teacher}, `
  //   + `학생들은 ${childrenStr}입니다.`

  return `${classNo}반의 선생님은 ${teacher}, `
    + `학생들은 ${children.join(', ')}입니다.`
}

//3반의 선생님은 김민지, 학생들은 영희, 철수, 보라입니다.
```



코드 예시 (replace 메서드 쓰지 않는 방법)

```javascript
'010-1234-5678'.split('-').join('.');
```



배열을 변경하는 기본 메서드

push, unshift, pop, shift, splice, fill, reverse

=> 배열의 맨 첫번쨰/ 맨 마지막에 원소를 추가하거나, 추출하거나, 배열 자체에 대해 동일한 원소로 요소를 가득 매운다든가, 배열 요소의 순서를 거꾸로 한 배열을 반환할 때 사용한다.

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7];

// 2번 인덱스부터 2개 요소 제거
arr.splice(2, 2);

console.log(arr);

// 3번 인덱스부터 요소 제거 없이 'a' 추가
arr.splice(3, 0, 'a');

console.log(arr);

// 1번 인덱스부터 3개 요소 제거 후 '가', '나', '다' 추가
arr.splice(1, 3, '가', '나', '다');

console.log(arr);
```

delete 는 결국, 해당 인덱스 자체를 지우지 않고, "비어 있음" 으로만 남게 된다.

=> 따라서, 제대로 지우려면 splice를 사용하기. (이 때에는, 해당 index 의 메모리가 제거가 된다.)

```javascript
const arr = [1, 2, 3, 4, 5];
delete arr[2]; //arr[2]에는 undefined라는 값이 남아있게 된다.

console.log(arr); //길이 5짜리 배열이다.

//[1, 2, 비어 있음, 4, 5]
//0: 1
//1: 2
//3: 4
//4: 5
//length: 5
//[[Prototype]]: Array(0)

console.log(arr[2]); //undefined


//아래의 경우는 splice를 쓰는 경우
const arr2 = [1, 2, 3, 4, 5];
arr2.splice(2, 1);

console.log(arr2);

//[1, 2, 4, 5]
//0: 1
//1: 2
//2: 4
//3: 5
//length: 4
//[[Prototype]]: Array(0)

```

fill

```javascript
// 중간의 빈 값도 채움
const arr1 = [1, 2, , , 4, 5];
arr1.fill(7);

console.log('1.', arr1);

// 💡 특정 값으로 채운 배열 생성시 유용
const arr2 = new Array(10);
arr2.fill(1);

console.log('2.', arr2);

// 인자가 둘일 때: (채울 값, ~부터)
arr2.fill(2, 3);

console.log('3.', arr2);

// 인자가 셋일 때: (채울 값, ~부터, ~ 전까지)
arr2.fill(3, 6, 9);

console.log('4.', arr2);
```



참고사항

* arr.push() => 원본 배열을 조작하여 반환

* 배열의 스프레드 => 새로운 배열을 생성해서 반환



새 배열을 반환하는 기본 메서드들

* concat, splice, flat 등

  * 원본 배열을 수정하지 않는다.

  * 기본적으로 얕은 복사본이다.




concat

* 최종적으로 1개의 배열을 반환하는 함수이다
  * 2개 이상의 배열 또는 값을 인자로 받아서, 인자의 모든 요소(값)을 1개의 배열에 넣는다.
    * arr1 배열 뒤쪽에 넣는 방식으로 구현된다. (기존 arr1 배열은 변하지 않는다.)

```javascript
const arr1 = [1, 2, 3];
const arr2 = ['a', 'b', 'c'];
const arr3 = [true, false];

const arr4 = arr1.concat(arr2);
console.log(arr4);
// [1, 2, 3, 'a', 'b', 'c']


const arr5 = arr1.concat(arr2, 3);
console.log(arr5);
//[1, 2, 3, 'a', 'b', 'c', 3]

const arr6 = arr1.concat('ABC', arr2, arr3, 100);
console.log(arr6);
//[1, 2, 3, 'ABC', 'a', 'b', 'c', true, false, 100]

// ⭐️ 원본 배열들에는 변화 없음
console.log(arr1, arr2, arr3);
//[1, 2, 3] ['a', 'b', 'c'] [true, false]
```

slice

* 1개의 배열을 반환하며, arr1의 연속된 특정 요소들을 뽑아내어 return 할 배열에 담는다.

```javascript
const arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];

const arr2 = arr1.slice(3);
const arr3 = arr1.slice(3, 7);

console.log(arr2, arr3);
//[4, 5, 6, 7, 8, 9] [4, 5, 6, 7]

// 원본에는 변화 없음
console.log(arr1);
```

flat

* 1개의 배열을 반환하며, 배열 내 요소 중 배열이 있으면, 이를 다시 요소로 담아서 반환한다.
  * 인자로 숫자를 받으며, 이는 배열 내의 배열을 "몇 단계까지" flat화 할 것인지에 대한 정보이다.

```javascript
const orgArr = [
  1, 2,
  [3, 4],
  [5, [6, [7, 8]]]
];

// 인자가 없으면 1을 넣은 것과 같음
const arr0 = orgArr.flat();
const arr1 = orgArr.flat(1);

const arr2 = orgArr.flat(2);
const arr3 = orgArr.flat(3);

console.log('N:', arr0);
console.log('1:', arr1);
console.log('2:', arr2);
console.log('3:', arr3);

//N: (6) [1, 2, 3, 4, 5, Array(2)]
//1: (6) [1, 2, 3, 4, 5, Array(2)]
//2: (7) [1, 2, 3, 4, 5, 6, Array(2)]
//3: (8) [1, 2, 3, 4, 5, 6, 7, 8]



// 원본에는 변화 없음
console.log('org:', orgArr);
```



//slice()는 splice() 와 달리, 부수효과가 발생하지 않는다.

//flat()을 이용해서 완전히 다 풀려면, 인자값을 굉장히 크게 주면 된다.





### 고차함수 메서드들

forEach() => 기본적으로 인자 3개를 받음. (value, idx, arr)

forEach()는 콜백함수의 실행이 목적이지, 결과값을 원하는 목적은 아니므로, undefined가 출력된다.

```javascript
const arr = [1, 2, 3, 4, 5];

const result = arr.forEach(itm => {
  console.log(itm);
});
//1
//2
//3
//4
//5
```

```javascript
const arr = [10, 20, 30, 40, 50];

// 콜백함수의 인자가 둘일 때
arr.forEach((itm, idx) => {
  console.log(itm, idx);
});
//10 1
//20 2
//30 3
//40 4
//50 5
```

forEach()의 인자로, 함수 객체 그 자체만 넘겨도, 실행이 가능하다

```javascript
const arr = [1, 2, 3, 4, 5];

// 현존하는 함수를 인자로 - 💡 결과 살펴볼 것
arr.forEach(console.log);

//1 0 [1, 2, 3, 4, 5]
//2 1 [1, 2, 3, 4, 5]
//3 2 [1, 2, 3, 4, 5]
//4 3 [1, 2, 3, 4, 5]
//5 4 [1, 2, 3, 4, 5]
```



```javascript
const arr = [1, 2, 3, 4, 5];

// 콜백함수의 인자가 셋일 때
arr.forEach((itm, idx, arr) => {
  // 💡 세 번째 인자는 원본 배열의 참조임
  arr[idx]++;
  console.log(itm);
});

//1
//2
//3
//4
//5



// 위의 코드의 arr[idx]++ 로 인해, arr원본의 내용이 변경되게 된다.
console.log(arr);
//[2,3,4,5,6]
```



map()

* 결과물은 1개의 새로운 배열을 반환
  * 인스턴스로 받은 배열을, 인자로 받은 함수에 의해서 새로운 배열을 탄생시킨다.

```javascript
const orgArr = [1, 2, 3, 4, 5];

// ⭐️ 각 콜백함수는 어떤 값을 반환해야 함
const arr1 = orgArr.map(i => i + 1);
const arr2 = orgArr.map(i => i * i);
const arr3 = orgArr.map(i => i % 2 ? '홀수' : '짝수');

console.log(arr1);
console.log(arr2);
console.log(arr3);

// [2, 3, 4, 5, 6]
// [1, 4, 9, 16, 25]
// ['홀수', '짝수', '홀수', '짝수', '홀수']
```

```javascript
const orgArr = [
  { name: '사과', cat: '과일', price: 3000 },
  { name: '오이', cat: '채소', price: 1500 },
  { name: '당근', cat: '채소', price: 2000 },
  { name: '살구', cat: '과일', price: 2500 },
  { name: '피망', cat: '채소', price: 2500 },
  { name: '딸기', cat: '과일', price: 5000 }
];


const arr1 = orgArr.map(itm => {
  // 💡 블록 안에서는 return 문 필요함
  return {
    name: itm.name,
    cat: itm.cat
  }
});

console.log(arr1);

//[{name: '사과', cat: '과일'},{name: '오이', cat: '채소'},{name: '당근', cat: '채소'},{name: '살구', cat: '과일'},{name: '피망', cat: '채소'},{name: '딸기', cat: '과일'}]


// 디스트럭쳐링 사용 (편의에 따라 적절히)
// 결과는 위와 똑같다.
const arr2 = orgArr.map(({name, cat}) => {
  return { name, cat }
});

console.log(arr2);

//2번째 인자 사용
const joined = orgArr
.map(({name, cat, price}, idx) => {
  return `${idx + 1}: [${cat[0]}] ${name}: ${price}원`
})
.join('\n - - - - - - - - - \n');

console.log(joined);


//1: [과] 사과: 3000원
// - - - - - - - - - 
//2: [채] 오이: 1500원
// - - - - - - - - - 
//3: [채] 당근: 2000원
// - - - - - - - - - 
//4: [과] 살구: 2500원
// - - - - - - - - - 
//5: [채] 피망: 2500원
// - - - - - - - - - 
//6: [과] 딸기: 5000원
```

=> 화살표 사용 함수에서, 블록문 안에서는, return 문이 필요하다.



find, findLast, findIndex, findLastIndex

* 인자로서 콜백함수를 받으며, 해당 콜백함수는 아래와 같이 동작한다

  * true 또는 false를 받는다

  * 배열의 각 요소를 콜백함수의 인자로 받는다

    => 이 때, 콜백함수의 결과물이 true일 때, 콜백함수를 인자로 받았던 함수는, 해당 요소 또는 해당 요소의 index를 반환한다.  

```javascript
const arr = [1, 2, '삼', 4, 5, 6, '칠', 8, 9];

const isString = i => typeof i === 'string';
const isBoolean = i => typeof i === 'boolean';

console.log(
  arr.find(isString),
  arr.findLast(isString),
  arr.findIndex(isString),
  arr.findLastIndex(isString)
);
// 삼 칠 2 6

// 없을 시 값은 undefined, 인덱스는 -1 반환
console.log(
  arr.find(isBoolean),
  arr.findLast(isBoolean),
  arr.findIndex(isBoolean),
  arr.findLastIndex(isBoolean)
);

//undefined undefined -1 -1
```

```javascript
const arr = [
  { name: '사과', cat: '과일', price: 3000 },
  { name: '오이', cat: '채소', price: 1500 },
  { name: '당근', cat: '채소', price: 2000 },
  { name: '살구', cat: '과일', price: 2500 },
  { name: '피망', cat: '채소', price: 3500 },
  { name: '딸기', cat: '과일', price: 5000 }
];

const isCheapFruit = i => {
  return i.cat === '과일' && i.price < 3000;
}

console.log(
  arr.find(({cat}) => cat === '채소').name,
  arr.findLast(isCheapFruit).name
);
```



some, every

* 하나의 요소라도 true를 반환하면, some() 의 결과는 true를 반환
* 모든 요소가 true를 반환해야, every() 의 결과는 true를 반환

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(
  arr.some(i => i % 2),
  arr.every(i => i % 2),
  arr.some(i => i < 0),
  arr.every(i => i < 10)
);

//true false false true
```

```javascript
const arr = [
  { name: '사과', cat: '과일', price: 3000 },
  { name: '오이', cat: '채소', price: 1500 },
  { name: '당근', cat: '채소', price: 2000 },
  { name: '살구', cat: '과일', price: 2500 },
  { name: '피망', cat: '채소', price: 3500 },
  { name: '딸기', cat: '과일', price: 5000 }
];

const isCheapVege = i => {
  return i.cat === '채소' && i.price < 2000;
}
const isPlant = ({cat}) => {
  return ['과일', '채소'].includes(cat);
}

console.log(
  arr.some(isCheapVege),
  arr.every(isCheapVege),
  arr.some(isPlant),
  arr.every(isPlant)
);

//true false true true
```



filter

* 콜백함수를 인자로 받으며, 이 콜백 함수는 필터 로직을 받는다.
* 해당 콜백 함수를 true로 만드는 요소만 "filtering"하여, 새로운 배열에 담아서 반환한다.

```javascript
const arr = [
  { name: '사과', cat: '과일', price: 3000 },
  { name: '오이', cat: '채소', price: 1500 },
  { name: '당근', cat: '채소', price: 2000 },
  { name: '살구', cat: '과일', price: 2500 },
  { name: '피망', cat: '채소', price: 3500 },
  { name: '딸기', cat: '과일', price: 5000 }
];

console.log(
  '과일 목록:',
  arr
  .filter(({cat}) => cat === '과일')
  .map(({name}) => name)
  .join(', ')
);

//과일 목록: 사과, 살구, 딸기
```



reduce => 초깃값을 설정하는 것과 그렇지 않은 경우가 존재. 

* 배열의 여러 요소를 순차적으로, 그리고 반복적으로 계산하여 어떤 하나의 값(객체)를 도출해내는데 유용하게 사용되는 함수
  * 콜백함수를 적용할 때마다의 return 결과물은 prev에 저장된다.

* 초깃값이 별도로 설정되지 않는 경우, 맨 첫번쨰 인자가 prev 값에 할당된다.

  ```javascript
  //1+2+3... +9를 reduce()를 통해 구현
  
  const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  
  //prev = 1, cur = 2부터 시작
  console.log(
    arr.reduce((prev, curr, idx) => {
      console.log(`p: ${prev}, c: ${curr}, i: ${idx}`);
      return prev + curr;
    })
  );
  
  //p: 1, c: 2, i: 1
  //p: 3, c: 3, i: 2
  //p: 6, c: 4, i: 3
  //p: 10, c: 5, i: 4
  //p: 15, c: 6, i: 5
  //p: 21, c: 7, i: 6
  //p: 28, c: 8, i: 7
  //p: 36, c: 9, i: 8
  //45
  
  //초깃값이 존재하는 경우
  //prev = 10, cur = 1부터 시작
  const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  
  console.log(
    arr.reduce((prev, curr, idx) => {
      console.log(`p: ${prev}, c: ${curr}, i: ${idx}`);
      return prev + curr;
    }, 10)
  );
  
  //p: 10, c: 1, i: 0
  //p: 11, c: 2, i: 1
  //p: 13, c: 3, i: 2
  //p: 16, c: 4, i: 3
  //p: 20, c: 5, i: 4
  //p: 25, c: 6, i: 5
  //p: 31, c: 7, i: 6
  //p: 38, c: 8, i: 7
  //p: 46, c: 9, i: 8
  //55
  ```

  아래의 예에서는 prev와 curr은 다음과 같은 의미를 지닌다.

  (★ prev와 curr의 타입이 일치하지 않아도 된다는 것이 keypoint)

  * prev는 초깃값 혹은 이전 콜백함수 실행의 결과물
    * 초깃값을 꼭 배열의 타입에 맞추지 않아도 된다.

  * curr은 배열의 현재 요소를 의미 (즉 숫자이다)

    * 맨 마지막의 콜백 함수의 실행이 끝나게 되면, 이 때는 curr은 마지막 콜백함수의 결과물이 된다.

      (즉, 여기서는 숫자가 아니라, 객체가 된다.)

  ```javascript
  const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  
  // 홀수와 짝수 갯수
  console.log(
    arr.reduce((prev, curr) => {
      return {
        odd: prev.odd + curr % 2,
        even: prev.even + (1 - (curr % 2)),
      }
    }, { odd: 0, even: 0 })
  );
  
  //{odd: 5, even: 4}
  ```

  ```javascript
  const arr = [
    { name: '사과', cat: '과일', price: 3000 },
    { name: '오이', cat: '채소', price: 1500 },
    { name: '당근', cat: '채소', price: 2000 },
    { name: '살구', cat: '과일', price: 2500 },
    { name: '피망', cat: '채소', price: 3500 },
    { name: '딸기', cat: '과일', price: 5000 }
  ];
  
  ['과일', '채소'].forEach(category => {
    console.log(
      `${category}의 가격의 합:`,
      arr
      .filter(({cat}) => cat === category)
      .map(({price}) => price)
      .reduce((prev, curr) => prev + curr)
    );
  });
  
  // 과일의 가격의 합: 10500
  // 채소의 가격의 합: 7000
  ```

  => 여기서, 함수형 프로그래밍이 적용되었음을 알 수 있다.





sort는 배열을 (주어진 기준대로) 정렬

=> 원본 배열을 정렬하여 결과값으로 반환한다.

=> 따라서, 원본 배열은 수정된다.



아래의 경우는, sort() 에 인자를 주지 않아서 일반적인 정렬의 경우를 보여준다.

* 그리고, 암묵적으로 문자형으로 변환하여서 정렬하기 때문에, 숫자형의 경우에는 원치 않은 결과가 나온다.

```javascript
const arr = ['라', '사', '다', '가', '바', '마', '나'];

arr.sort();

console.log(arr);

//['가', '나', '다', '라', '마', '바', '사']
```

```javascript
let randomWord = 'DBKGICAHFEJ';

console.log(
  randomWord
  .split('')
  .sort()
  // .reverse()
  .join('')
);

console.log(randomWord);

//ABCDEFGHIJK
//DBKGICAHFEJ
```

```javascript
// ⚠️ 숫자일 시 문제가 생김
const arr = [1, 2, 30, 400, 10, 100, 1000];
console.log(arr.sort());

//[1, 10, 100, 1000, 2, 30, 400]
```



배열 내 숫자의 정확한 정렬을 위해서는, 콜백 함수 사용

=> 이는 웹 브라우저마다 정렬을 구현하는 방식이 다르므로, sort() 내부 콜백함수에서 console.log() 를 찍어보면 a와 b가 브라우저마다 다르게 적혀있음을 알 수 있다.

```javascript
const arr = [4, 2, 3, 1, 5, 6, 7, 8, 9];

// 오름차순 정렬
console.log(
  arr.sort((a, b) => {
    console.log(`a: ${a}, b: ${b}`);
    return a-b;
  })
);

console.log(arr);
//[1, 2, 3, 4, 5, 6, 7, 8, 9]

//a가 뒤에것, b가 앞에 것을 받는다.
```

```javascript
const arr = ['F', 'E', 'I', 'A', 'H', 'C', 'D', 'J', 'G', 'B'];

console.log(
  arr.sort((a, b) => a > b ? 1 : -1)
);

//['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']
```

*의문사항*

* *sort() 함수가 정확히 어떤 원리로 동작하는지 파악하고 싶다*
  * *버블 정렬과 같이 단순히 1개의 정렬을 활용한다고 보기에는, a와 b의 값을 추적해보면 그렇지 않다고 느껴서이다.* 



flatMap => mapping된 결과물을 평평하게 펼침

```javascript
const arr = [1, 2, 3, 4, 5];

console.log(
  arr.flatMap(i => [i * 10, i * 100, i * 1000])
);

//[10, 100, 1000, 20, 200, 2000, 30, 300, 3000, 40, 400, 4000, 50, 500, 5000]
```



//맨 마지막 코드는 아래와 같이 적어도 된다.

```javascript
const word = '하나 둘 셋 넷 다섯 여섯 일곱 여덟 아홉 열';

console.log(
  word
  .split(' ')
  .flatMap(i => i.split(''))
);
//['하', '나', '둘', '셋', '넷', '다', '섯', '여', '섯', '일', '곱', '여', '덟', '아', '홉', '열']

//아래의 코드로 작성해도 된다.
console.log(word.replaceAll(' ','').split(''))
```



### 배열의 스프레드와 디스트럭쳐링

스프레드

* 배열 내부의 요소들을, 대괄호를 제거하면서 다른 배열 속에 통째로 넣을 때 사용
* 함수를 정의할 때, 인자의 갯수가 몇 개를 받을지 불분명할 때에도 스프레드 문법을 활용한다.

```javascript
const arr1 = ['B', 'C'];
const arr2 = ['D'];
const arr3 = ['E'];

const arr4 = ['A', ...arr1, ...arr2, ...arr3, 'F']

console.log(arr4);
//['A', 'B', 'C', 'D', 'E', 'F']
```

```javascript
const arr1 = [1, 2, 3, 4, 5];
console.log(arr1);
//[1, 2, 3, 4, 5]

console.log(...arr1);
//1 2 3 4 5
// console.log(1, 2, 3, 4, 5); 과 결과가 같다.

//함수의 인자로서 스프레드를 활용할 수 있다.
console.log(
  Math.max(...arr1),
  Math.min(...arr1)
);

//5 1
```

스프레드 활용

```javascript
function classIntro (classNo, teacher, ...children) {
  return `${classNo}반의 선생님은 ${teacher}, `
    + `학생들은 ${children.join(', ')}입니다.`
}

const classNo = 3;
const teacher = '김민지';
const students = ['영희', '철수', '보라', '돌준', '달숙'];

console.log(
  classIntro(classNo, teacher, ...students)
);

//3반의 선생님은 김민지, 학생들은 영희, 철수, 보라, 돌준, 달숙입니다.
```

splice() 메서드와 스프레드를 활용해서, 아래와 같이 arr 배열에서 연속된 특정 요소들을 다른 요소들로 한꺼번에 대체할 수 있다.

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7];
const toAdd = ['둘', '셋', '넷'];

arr.splice(1, 3, ...toAdd);

console.log(arr);
//[1, '둘', '셋', '넷', 5, 6, 7]
```

concat() 메서드를 활용할 때, 스프레드를 활용하면 가독성이 보다 더 높아진다.

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

const arr3 = arr1.concat(arr2);
const arr4 = [...arr1, ...arr2];

//같은 결과를 나타낸다.
console.log(arr3, arr4);
//[1, 2, 3, 4, 5, 6]
//[1, 2, 3, 4, 5, 6]
```

...arr 은 얕은 복사만 가능하다.

그리고, 스프레드는 push와 unshift 대신 사용할 수 있으며, 가독성 면에서 보다 더 우수하다.

```javascript
let arr = [1, 2, 3];

arr = [...arr, 4];
console.log(arr);
//[1, 2, 3, 4]

arr = [0, ...arr];
console.log(arr);
//[0, 1, 2, 3, 4]
```



원본배열을 "유지"한 채, 일정부분만 연결하여 복사하는 메서드는 slice() 활용 (** splice()는 원본 배열을 변경시킴)

```javascript
const orgArr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
// 4 ~ 6을 제외한 새 배열 만들기

// 💡 slice는 원본을 변경하지 않음
const arr1 = [
  ...orgArr.slice(0, 3),
  ...orgArr.slice(6, 9)
];
console.log(arr1);

// [1, 2, 3, 7, 8, 9]
```



디스트럭쳐링

```javascript
const arr = [1, 2, 3];

const x = arr[0];
const y = arr[1];
const z = arr[2];

console.log(x, y, z);
// 1 2 3
```

아래처럼, x y z에는 순서대로 arr의 요소가 할당된다.

```javascript
const arr = [1, 2, 3];
const [x, y, z] = arr;

console.log(x, y, z);
//1 2 3
```

```javascript
const arr = [1, 2, 3];
const [x, y] = arr;

console.log(x, y);
//1 2
```

할당되지 않는 경우를 대비해서, 기본값을 미리 할당을 할 수 있다

=> 기본값이 주어진 상태에서 할당을 하면, 할당값이 우선시 된다.

```javascript
const arr = [1, 2, 3];

const [a, b, c, d = 4, e = 5] = arr;
console.log(a, b, c, d, e);

//1 2 3 4 5

// 기본값보다 할당값이 우선
const [f, g, h = 4] = arr;
console.log(f, g, h);
//1 2 3
```

아래처럼, 스프레드를 활용이 가능하며, 이 떄 y는 배열이 된다.

```javascript
const arr = [1, 2, 3, 4, 5];
const [x, ...y] = arr;

console.log(x, y);
//1 [2,3,4,5]
```

디스트럭쳐링 활용

=> 스프레드를 활용해서, 원본을 변화시키지 않고 점수 순서대로 정렬해서 1~3등을 출력

```javascript
const players = [
  { name: '순이', score: 91 },
  { name: '정환', score: 65 },
  { name: '윤수', score: 72 },
  { name: '철웅', score: 88 },
  { name: '지우', score: 98 },
  { name: '세아', score: 40 }
];

// 배열 중 첫 3개만 가져옴
function logTop3 ([first, second, third]) {
  console.log(
    `1등은 ${first}!! 2등과 3등은 ${second}, ${third}입니다.`
  );
}

logTop3(
  [...players] // 💡 원본의 얕은 복사본을 정렬
  .sort((a, b) => b.score - a.score)
  .map(({name}) => name)
);

//1등은 지우!! 2등과 3등은 순이, 철웅입니다.
```

아래와 같이 값을 바꾸는 용도로도 사용이 가능

```javascript
let a = 1;
let b = 2;

// 서로 값을 바꾸기
[a, b] = [b, a];

console.log(a, b);
//2 1
```



** 스프레드를 활용하는 곳은, sort()를 활용해서 생기는 문제점인, "원본 배열의 변경"을 예방하기 위해서이다.

=> 얕은 복사를 활용한다.



## Section 8. 객체 깊게 다루기

### Lesson 1. Object

Object 클래스



Object 생성자 함수의 인자로서, 특정 타입의 값을 주게 되면, 해당 값에 적합한 래핑함수가 자동으로 적용되어서 등장한다

```javascript
console.log(
  new Object(1),
  new Object('ABC'),
  new Object(true),
  new Object([1, 2, 3])
);

//Number {1} 
//String {'ABC'}
//Boolean {true}
//[1, 2, 3]
```





특정 객체에서 프로퍼티만 따서 또 다른 객체에 복사하는 것이 가능하다

* 스프레드를 활용하거나 정적 메서드인 assign 메서드를 활용해서 이루어진다.

  => 얕은 복사이기 때문에, 복사한 객체의 프로퍼티가 값이 아닌 객체라면, 복사되기 이전의 객체의 해당 프로퍼티와 공유한다.

  ```javascript
  //스프레드를 활용한 예
  const intro1 = {
    name: '홍길동'
  };
  const intro2 = { ...intro1 };
  
  console.log(intro1, intro2);
  
  // {name: '홍길동'} {name: '홍길동'}
  ```

  ```javascript
  // Object.assign() 메서드 활용
  
  const personal = {
    age: 25,
    married: false
  };
  const career = {
    job: '개발자',
    position: '팀장'
  }
  
  Object.assign(intro1, personal);
  console.log(intro1);
  
  //{name: '홍길동', age: 25, married: false}
  
  // 둘 이상의 원본에서 가져올 수도 있음
  Object.assign(intro2, personal, career);
  console.log(intro2);
  
  //{name: '홍길동', age: 25, married: false, job: '개발자', position: '팀장'}
  ```

  ```javascript
  //얕은 수준에서의 복사가 이루어짐
  const obj1 = new Object();
  const obj2 = { x: 1, y: 2 };
  const obj3 = { y: 3 };
  const obj4 = { z: { a: 1 }}
  
  Object.assign(obj1, obj2, obj3, obj4);
  
  console.log(obj1);
  //{x: 1, y: 3, z: {a: 1}}
  
  obj2.x = 0;
  obj4.z.a = 2;
  
  console.log(obj1);
  //{x: 1, y: 3, z: {a: 2}}   //obj1의 key z에 대한 객체는, obj2의 key z에 대한 객체와 공유한다.
  ```

  

* 특정 객체의 프로퍼티 중, KEY만 뽑을 수도 있고, value만 뽑을수도 있으며, 둘 다 뽑을 수도 있다

  => 셋 다 모두 반환 결과는 배열이 된다.

  ```javascript
  const obj = {
    x: 1,
    y: 2,
    z: 3
  };
  
  console.log(
    Object.keys(obj),
  );
  console.log(
    Object.values(obj),
  );
  console.log(
    Object.entries(obj),
  );
  
  // ['x', 'y', 'z']
  // [1, 2, 3]
  // [['x', 1], ['y', 2], ['z', 3]] 
  ```

* 객체의 프로퍼티를 추가/삭제/수정 금지할 수 있다. (얕은 수준)

  * 추가만 금지할 수 있고, 추가/삭제까지 금지할 수 있으며, 추가/삭제/수정까지 금지할 수 있다.

  * 셋 다 모두 정적 메서드로서 구현할 수 있다.

    * Object.preventExtensions(obj);
    * Object.seal(obj);
    * Object.isFrozen(obj);

    ```javascript
    //프로퍼티 추가만 금지
    const obj = { x: 1, y: 2 };
    
    console.log(Object.isExtensible(obj)); //true
    
    Object.preventExtensions(obj);
    
    console.log(Object.isExtensible(obj)); //false
    
    obj.x++; // 프로퍼티 수정 가능
    delete obj.y // 프로퍼티 삭제 가능
    obj.z = 3; // 💡 프로퍼티 추가 금지
    
    console.log(obj); //{x: 2}
    
    
    //프로퍼티 추가, 삭제 금지
    //프로퍼티 어트리뷰트 configurable 과 관련이 있다. (뒤에서 언급)
    const obj = { x: 1, y: 2 };
    
    console.log(Object.isSealed(obj)); //false
    
    Object.seal(obj);
    
    console.log(Object.isSealed(obj)); //true
    
    obj.x++; // 프로퍼티 수정 가능
    delete obj.y // 💡 프로퍼티 삭제 금지
    obj.z = 3; // 💡 프로퍼티 추가 금지
    
    console.log(obj); // {x: 2, y: 2}
    
    
    //프로퍼티 추가, 삭제, 수정 금지
    const obj = { x: 1, y: 2 };
    
    console.log(Object.isFrozen(obj)); //false
    
    Object.freeze(obj);
    
    console.log(Object.isFrozen(obj)); //true
    
    obj.x++; // 💡 프로퍼티 수정 불가
    delete obj.y // 💡 프로퍼티 삭제 금지
    obj.z = 3; // 💡 프로퍼티 추가 금지
    
    console.log(obj); //{x: 1, y: 2}
    
    
    //얕게만 적용
    const obj = {
      x: 1,
      y: { a: 1 }
    };
    
    Object.freeze(obj);
    
    obj.x++;
    obj.y.a++;
    
    console.log(obj); //{x: 1, y: {a: 2}}
    ```

    

  * 셋 다 모두 얕은 수준에서 실행되기 때문에, 깊은 수준까지 실행하기 위해서는 별도의 메서드를 사용해야 한다.



### 프로퍼티 어트리뷰트

프로퍼티에는 데이터 프로퍼티와 접근자 프로퍼티가 있다.

```javascript
const person = {

  // ⭐️ 1. 데이터 프로퍼티들
  fullName: '홍길동',
  ageInNumber: 25,

  // ⭐️ 2. 접근자 프로퍼티들
  get name () {
    return this.fullName
    .split('')
    .map((letter, idx) => idx === 0 ? letter : '*')
    .join('');
  },
  get age () { return this.ageInNumber + '세'; },
  set age (age) {
    this.ageInNumber = Number(age);
  }
}

console.log(
  person.name, person.age
);

// 홍**, 25세
```

객체의 프로퍼티 어트리뷰트는, 별도의 디스크립터 객체에 "프로퍼티" 로서 저장된다.

* 객체가 생성될 때, 프로퍼티 어트리뷰트는 엔진에 의해 자동으로 정의된다.

```javascript
// 특정 프로퍼티를 지정하여 반환
console.log('1.',
  Object.getOwnPropertyDescriptor(person, 'fullName')
);
console.log('2.',
  Object.getOwnPropertyDescriptor(person, 'ageInNumber')
);
console.log('3.', // set: undefined
  Object.getOwnPropertyDescriptor(person, 'name')
);
console.log('4.', // get, set 모두 있음
  Object.getOwnPropertyDescriptor(person, 'age')
);

//1. {value: '홍길동', writable: true, enumerable: true, configurable: true
//2. {value: 25, writable: true, enumerable: true, configurable: true}
//3. {set: undefined, enumerable: true, configurable: true, get: ƒ}
//4. {enumerable: true, configurable: true, get: ƒ, set: ƒ}

// 모든 프로퍼티의 어트리뷰트 객체로 묶어 반환
console.log(
  Object.getOwnPropertyDescriptors(person)
);
//{fullName: {…}, ageInNumber: {…}, name: {…}, age: {…}}
```

객체의 프로퍼티와 해당 프로퍼티의 어트리뷰트는, defineProperty() 라는 정적 메서드를 통해 설정할 수 있다

* ** 어트리뷰트는, 직접 객체에 접근하여 수정하는 것은 가능하지 않다.(writable 어트리뷰트에 직접 접근하여 true를 false로 바꾸어보는 코드를 작성해보았으나, 실행되지 않음)

  ```javascript
  const person = {};
  
  // 한 프로퍼티씩 각각 설정
  Object.defineProperty(person, 'fullName', {
    value: '홍길동',
    writable: true
    // 💡 누락한 어트리뷰트는 기본값으로 자동생성
  });
  
  Object.defineProperty(person, 'name', {
    get () {
      return this.fullName
      .split('')
      .map((letter, idx) => idx === 0 ? letter : '*')
      .join('');
    }
  });
  
  console.log(person, person.name);
  console.log( // ⚠️ 누락된 어트리뷰트들 확인해볼 것
    Object.getOwnPropertyDescriptors(person)
  );
  
  // {fullName: '홍길동'} 홍**
  // {fullName: {…}, name: {…}}
  
  //아래처럼 직접 어트리뷰트에 접근하여 수정을 시도하는 경우는, 실행되지 않는다
  Object.getOwnPropertyDescriptors(person).fullName.writable = false
  console.log(Object.getOwnPropertyDescriptors(person).fullName.writable)
  
  //true
  ```

  ```javascript
  // 여러 프로퍼티를 객체 형식으로 한꺼번에 설정
  Object.defineProperties(person, {
    ageInNumber: { 
      value: 25,
      writable: true
    },
    age: {
      get () { return this.ageInNumber + '세'; },
      set (age) {
        this.ageInNumber = Number(age);
      }
    }
  });
  
  person.age = 30;
  
  console.log(person, person.age);
  console.log(
    Object.getOwnPropertyDescriptors(person)
  );
  
  //{fullName: '홍길동', ageInNumber: 30} '30세'
  //{fullName: {…}, name: {…}, ageInNumber: {…}, age: {…}}
  ```



객체의 프로퍼티의 어트리뷰트를 조정하여, 아래의 과정을 시행할 수 있다

* 프로퍼티의 값을 조정

* 프로퍼티의 키값에 대해서, (특정 순환 메서드 사용 시) 순환대상에서 제외시키는 것

  ```javascript
  const person = {
    fullName: '홍길동',
    ageInNumber: 25,
  };
  
  // 💡 value를 전우치로 바꾸면
  Object.defineProperty(person, 'fullName', {
    value: '전우치'
  });
  
  console.log(person);
  //{fullName: '전우치', ageInNumber: 25}
  
  console.log(
    Object.keys(person)
  );
  //['fullName', 'ageInNumber']
  
  
  // 💡 enumerable을 false로 바꾸면, 해당 어트리뷰트의 프로퍼티는 순환대상에서 제외된다.
  Object.defineProperty(person, 'fullName', {
    enumerable: false
  });
  
  console.log(
    Object.keys(person)
  );
  //['ageInNumber']
  
  console.log(
    // ⭐️ Object의 또 다른 정적 메서드
    // ⭐️ enemerable이 false인 프로퍼티도 반환
    Object.getOwnPropertyNames(person)
  );
  //['fullName', 'ageInNumber']
  
  // 💡 seal: configurable을 false로 바꿈
  Object.seal(person);
  
  console.log(
    Object.getOwnPropertyDescriptors(person)
  );
  
  // 💡 freeze: configurable과 writable을 false로 바꿈
  // seal, configurable 보다 훨씬 엄격한 수준의 접근 제어라고 볼 수 있다.
  Object.freeze(person);
  
  console.log(
    Object.getOwnPropertyDescriptors(person)
  );
  ```

* 객체 동결

  * 새로운 속성을 추가, 기존 속성의 수정/제거가 불가능
  * 속성의 어트리뷰트가 변경되는 것을 모두 방지
  * 객체의 프로토타입이 변경되는 것도 방지
    * 의문사항) 이것은 생성자 함수를 통해서 접근했을 떄에도 방지되는지는 확인이 필요함.
  * 주의 사항 : freeze는 얕은 수준의 동결이기 때문에, 깊은 동결을 위해서는 객체의 프로퍼티가 객체가 아닌 primitive type이 나올때까지 재귀적으로 동결을 진행해야 한다.

  ```javascript
  function getDeepFrozen(obj) {
    console.log(obj);
  
    const result = {};
    const propNames = Object.getOwnPropertyNames(obj);
  
    for (const name of propNames) {
      const value = obj[name];
  
      result[name] = 
        (value && typeof value === 'object') ?
        getDeepFrozen(value) : value;
    }
    return Object.freeze(result);
  }
  
  //참고 : value && 가 필수적인 이유
  //	=> null이나 undefined인 경우, 위 코드는 무한반복되기 때문에 이를 방지하기 위함.
  ```

  ```javascript
  //얕은 동결 실행
  
  let myObj = {
    a: 1,
    b: {
      c: 2,
      d: {
        e: 3,
        f: {
          g: 4
        }
      }
    }
  }
  
  // 여러 번 실행해 볼 것
  myObj.a++;
  myObj.b.c++;
  myObj.b.d.e++;
  myObj.b.d.f.g++;
  
  console.log(myObj);
  //{a: 2, b: {c: 3, d: {e: 4, f: {g: 5}}}}
  
  
  //깊은 동결 실행
  myObj = getDeepFrozen(myObj);
  
  myObj.a++;
  myObj.b.c++;
  myObj.b.d.e++;
  myObj.b.d.f.g++;
  
  console.log(myObj);
  //myObj의 객체의 프로퍼티는 변한 점이 1개도 없다.
  ```

  ** 참고로, 깊은 동결의 경우 아래의 코드는 그렇게 좋지 않은 코드이다.

  (기능은 같다.)

  => object인자를 바꾸기 때문에, object를 재활용할 수 없다.

  => 함수에서는, 인자를 바꾸지 않고 일정한 연산에 의해서 어떠한 결과물을 도출해내는 것이 좋은 함수이다.

  ```javascript
  // mdn문서 코드
  
  function deepFreeze(object) {
    // 객체에 정의된 속성명을 추출
    var propNames = Object.getOwnPropertyNames(object);
  
    // 스스로를 동결하기 전에 속성을 동결
  
    for (let name of propNames) {
      let value = object[name];
  
      object[name] =
        value && typeof value === "object" ? deepFreeze(value) : value;
    }
  
    return Object.freeze(object);
  }
  
  var obj2 = {
    internal: {
      a: null,
    },
  };
  
  deepFreeze(obj2);
  
  obj2.internal.a = "anotherValue"; // 비엄격 모드에서 조용하게 실패
  obj2.internal.a; // null
  ```

  

  참고자료 : [Object.freeze() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)





참고

* 프로포티 생성 시, 자바 스크립트 엔진은 내부적으로 프로퍼티 어트리뷰트를 기본값으로 정의
  * 내부슬롯 이라고도 부른다
  * 개발자가 직접 접근할 수는 없으며, 간접적으로 확인할 수 있다. 

https://velog.io/@dbstjrwnekd/%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0-%EC%96%B4%ED%8A%B8%EB%A6%AC%EB%B7%B0%ED%8A%B8Property-Attribute

* 데이터 프로퍼티와 접근자 프로퍼티

  * 데이터 프로퍼티는 key-value로 이루어져 있다. 즉, 값을 가진다

    * 해당하는 어트리뷰트의 예시는 아래와 같다

      ```javascript
      {value: '홍길동', writable: true, enumerable: true, configurable: true}
      ```

  * 접근자 프로퍼티는, 값을 가지지 않는다

    * 데이터 프로퍼티의 값을 읽거나 변경하는데 사용된다

    * 해당하는 어트리뷰트는 4가지이며 아래와 같다

      ```javascript
      {set: undefined, enumerable: true, configurable: true, get: ƒ}
      ```

  * 객체가 생성될 때, 자바스크립트는 객체의 프로퍼티를 내부적으로 어트리뷰트를 통해서 관리를 한다

  * 출처 : https://velog.io/@seeh_h/%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0-%EC%96%B4%ED%8A%B8%EB%A6%AC%EB%B7%B0%ED%8A%B8feat.-%EB%82%B4%EB%B6%80-%EC%8A%AC%EB%A1%AF%EA%B3%BC-%EB%82%B4%EB%B6%80-%EB%A9%94%EC%86%8C%EB%93%9C



### JSON(JavaScript Object Notation)

일단, 객체를 문자열로 직렬화하는 예제를 살펴보자

=> 정적 메서드인 JSON.stringfy()를 활용한다.

```javascript
const person = {
  name: '김달순',
  age: 23,
  languages: ['Korean', 'English', 'French'],
  education: {
    school: '한국대',
    major: ['컴퓨터공학', '전자공학'],
    graduated: true,
  }
};

const personStr = JSON.stringify(person);

console.log(typeof personStr);
console.log(personStr);

//string
//{"name":"김달순","age":23,"languages":["Korean","English","French"],"education":{"school":"한국대","major":["컴퓨터공학","전자공학"],"graduated":true}}
```

* 아래에서, Infinity나 NaN이 null로 직렬화가 되는 이유는 아래와 같을 것이다. (내 생각)
  * null은 의도적으로 빈 값을 할당하는 상태이고, Infinity나 NaN 역시 어떠한 값이기 때문에 undefined보다 null이 적당하다고 판단될 것이다.
* 직렬화 시, 아래의 것들은 직렬화가 되지 않는다
  * 함수, Symbol, BigInt
    * 프로퍼티에서 key 나 value로서 위의 값이 존재한다면, 통째로 직렬화가 되지 않는다.
  * Date객체는 직렬화가 되기는 하지만, 역직렬화가 가능하지 않다.

```javascript
[
  JSON.stringify(1),
  JSON.stringify(Infinity), // ⚠️
  JSON.stringify(NaN), // ⚠️
  JSON.stringify('가나다'),
  JSON.stringify(true),
  JSON.stringify(null),
  JSON.stringify(undefined),
  JSON.stringify([1, 2, 3]),
  JSON.stringify({x: 1, y: 2}),
  JSON.stringify(new Date()), // ⚠️
]
.forEach(i => console.log(i));

//1
//null
//null
//'가나다'
//true
//null
//undefined
//[1,2,3]
//{"x":1, "y":2}
//"2023-10-19T22:25:16.958Z"

// 이후 배울 Symbol - 직렬화되지 않음
console.log( JSON.stringify(Symbol('hello')) ); // ⚠️
//undefined
```

* 아래는 값이 함수인 프로퍼티인 경우에는, 아예 직렬화 과정에서 생략됨을 확인할 수 있다

  * 함수 자체를 직렬화하려고 하면, undefined가 반환됨을 알 수 있다

  ```javascript
  const obj = {
    x: 1,
    y: 2,
    z: function () { return this.x + this.y }
  }
  console.log(obj.z())
  
  const objStr = JSON.stringify(obj);
  console.log(objStr);
  
  //3
  //{"x":1,"y":2}
  
  const func1 = (a, b) => a + b;
  function func2 () { console.log('HELLO'); }
  
  const func1Str = JSON.stringify(func1);
  const func2Str = JSON.stringify(func2);
  
  console.log(func1Str);
  console.log(func2Str);
  //undefined
  //undefined
  ```

  

JSON.stringify() 활용 시, 2번째 인자를 통해서 아래의 사항을 시행할 수 있다

=> 단순히, 객체 그대로를 직렬화하는 것이 아니라, 객체의 정보를 조작해서 변환할 수 있다

=> 이 때, 2번째 인자는 함수가 들어가며, 맨 첫번째 (key,value) 는 ('', 객체 그 자체) 가 무조건 들어간다는 것이 특징이다.

=> 2번째 인자로 배열이 들어갈 수도 있으며, 이 때 배열의 요소는 key 값이다.

```javascript
const obj = {
  a: 1,
  b: '2',
  c: 3,
  d: true,
  e: false
}

// 1. key와 value 매개변수
const objStr1 = JSON.stringify(obj, (key, value) => {
  if (key && key < 'a' || key > 'c') {
    // 해당 프로퍼티 생략
    return undefined;
    // ⚠️ 조건에 key && 을 붙이지 않으면 항상 undefined가 반환됨
    // key가 공백('')일 때(value는 객체 자체) undefined를 반환하므로...
    // key와 value를 로그로 출력해보며 확인해 볼 것
  }
  if (typeof value === 'number') {
    return value * 10;
  }
  return value;
});
console.log(objStr1);
//{"a":10,"b":"2","c":30}

// 2. 반환한 key의 배열 매개변수
const objStr2 = JSON.stringify(obj, ['b', 'c', 'd']);
console.log(objStr2);
//{"b":"2","c":3,"d":true}
```

* JSON.stringify()의 3번째 인자로 indent 정도를 넣을 수 있다

  * 가독성 있는 JSON 객체 결과물을 확인할 수 있다.

  ```javascript
  const obj = {
    a: 1,
    b: {
      c: 2,
      d: {
        e: 3
      }
    }
  };
  
  [
    JSON.stringify(obj, null),
    JSON.stringify(obj, null, 1),
    JSON.stringify(obj, null, 2),
    JSON.stringify(obj, null, '\t')
  ]
  .forEach(i => console.log(i));
  //{"a":1,"b":{"c":2,"d":{"e":3}}}
  
  {
   "a": 1,
   "b": {
    "c": 2,
    "d": {
     "e": 3
    }
   }
  }
  
  {
    "a": 1,
    "b": {
      "c": 2,
      "d": {
        "e": 3
      }
    }
  }
  
  {
  	"a": 1,
  	"b": {
  		"c": 2,
  		"d": {
  			"e": 3
  		}
  	}
  }
  ```

* 이외에도, 객체에 toJSON 프로퍼티가 있고, 그 값이 "함수"인 경우에는 해당 객체가 직렬화 되는 것이 아니라, 함수의 결과물이 출력된다

  ```javascript
  const obj = {
    x: 1,
    y: 2,
    toJSON: function () {
      return '훗, 나를 직렬화해보겠다는 건가';
    }
  }
  
  console.log(
    JSON.stringify(obj)
  );
  //"훗, 나를 직렬화해보겠다는 건가"
  
  const obj = {
    x: 1,
    y: 2,
    toJSON: 4444
  }
  
  //toJSON 프로퍼티의 키를 "문자열"로 취급하며, 객체 통째로 직렬화가 된다.
  console.log(
    JSON.stringify(obj)
  );
  //{"x":1,"y":2,"toJSON":4444}
  
  
  //Date 객체의 직렬화 결과물이 문자로 나오는 것도, Date 객체가 내부적으로 toJSON 프로퍼티를 가지고 있기 때문이다. (그리고 해당 프로퍼티의 값은 함수!)
  console.log(JSON.stringify(new Date()));
  //"2023-10-20T07:04:02.591Z"
  new Date().toJSON;  //Date 생성자 함수를 통해 만든 날짜 객체에 toJSON 프로퍼티가 있음을 확인할 수 있다.
  ```



역직렬화

=> JSON.parse() 함수를 통해 이루어지며, 2번째 인자인 함수를 통해서, 역직렬화시 객체의 프로퍼티의 값을 조작하여 역직렬화할 수 있는 기능이다.

=> "문자열"로 표현된 자바스크립트 데이터를, 해석하여 자바스크립트 자료형으로 변환시킨다.

```javascript
//따옴표와 내부따옴표를 통해서, string인지 다른 타입의 변수인지를 구분한다.
[
  JSON.parse('1'),
  JSON.parse('"가나다"'), // ⚠️ 안쪽에 따옴표 포함해야 함
  JSON.parse('true'),
  JSON.parse('null'),
  JSON.parse('[1, 2, 3]'),
  JSON.parse('{"x": 1, "y": 2}') // ⚠️ key도 따옴표로 감싸야 함
]
.forEach(i => console.log(i));

//1
//가나다
//true
//null
//[1,2,3]
//{x: 1, y: 2}
```

```javascript
//parse()는 깊은 곳까지 다 수행한다.
//(내 생각) 프로퍼티의 value가 primitive type이 아닌 경우, 해당 value에 대해 재귀적으로 탐색한다.

const objStr = '{"a":1,"b":"ABC","c":true,"d":[1,2,3]}';

const obj = JSON.parse(objStr, (key, value) => {
  console.log(key, value);
  if (key === 'c') { 
    // 해당 프로퍼티 생략
    return undefined;
  }
  if (typeof value === 'number') {
    return value * 100;
  }
  return value;
});
//a 1
//b ABC
//c true
//0 1
//1 2
//2 3
//d [100, 200, 300]
// {a: 100, b: 'ABC', d: [100, 200, 300]}


//parse()의 맨 마지막 인자로는, ('', 객체 그 자체)이며, 해당 객체는 조작 과정을 거친 후의 객체 obj이며, 해당 obj가 결국에 출력된다.
console.log(obj); // ⚠️ 내부까지 적용(배열 확인해 볼 것)
// {a: 100, b: 'ABC', d: [100, 200, 300]}
```



위의 parse()의 특징을 활용해서, (제한적으로) 객체의 깊은 복사가 가능하다

=> (제한적으로) 가능하다고 하는 이유는, "함수" 와 "Date객체" 와 "Symbol" 과 "BigInt" 는 깊은 복사가 가능하지 않기 때문이다.

```javascript
const obj1 = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3,
      f: {
        g: 4
      }
    }
  }
}

//역직렬화를 통해 깊은 복사 시도
const obj2 = JSON.parse(JSON.stringify(obj1));

console.log(obj1);
console.log(obj2);

console.log(obj1 === obj2); //false
```

```javascript
const obj1 = {
  a: 1,
  b: 2,
  c: function () { return this.a + this.b },
  d: new Date(),
  e: Symbol('안녕'),
  // g: 1n // ⚠️ 오류 발생
}

const obj2 = JSON.parse(JSON.stringify(obj1));

console.log(obj1);
console.log(obj2);

//{a: 1, b: 2, d: Fri Oct 20 2023 09:47:51 GMT+0900 (한국 표준시), e: Symbol(안녕), c: ƒ}
//{a: 1, b: 2, d: '2023-10-20T00:47:51.184Z'}
```





참고

* 어떠한 복잡한 구조의 자료를 보내는 형식에는 XML, JSON, YAML 이 있다.

  * XML

    * 태그를 활용하여 구조화된 정보를 나타낸다
    * 엔터와 탭을 제외하고 한 줄로 작성해도 컴퓨터는 정상적으로 인식한다.
    * <u>어떠한 문법적인 오류가 발생할 때, 오류가 발생하는 범위는 해당 태그 내이다.</u>
      * 해당 태그 바깥에서는, 정상적으로 작동한다.

    * xsd라는 문서를 통해서, xml의 요소 중 어떤 "필수적인 요소" 가 들어갔는지 명시한다.
      * XSD/XML Schema Generator를 통해 자동으로 생성이 가능하다.
    * 태그의 여닫는 코드가 필수적으로 들어가므로, 코드가 많아지며 가독성이 떨어진다는 단점.

  * JSON
    * {} 를 활용하여 구조화된 정보를 나타낸다.
    * XML보다 간결하다.
    * (이 부분은 추가적인 확인 요망) 어떠한 문법적인 오류가 발생할 때, 문서 전체에 오류가 생긴다
      * 이는 {}로 열고 닫는 JSON의 특성상, 어디가 
      * 내 생각) 
    * 필수적인 요소가 들어갔는지 검증하려면, 자체적으로는 기능이 없다
      * 별도의 프로그래밍을 통해 확인해야 한다.
    * 결론
      * 안전성이 요구되는 것보다, 가벼운 프로그래밍을 할 때 적절하다.

  * YAML
    * 사람의 가독성에 초점을 맞춘 문서
      * 따라서, indenting을 사용해서 직관적으로 표현하며, xml과 Json과 달리, 한 줄로 표현(=Minifying)이 불가하다.



* Symbol의 정의

  * (나중에 배우니 간단하게만 정리하고 넘어감)

  * primitive type 이며, 프로퍼티의 키를 고유하게 설정하여 프로퍼티 키의 충돌을 방지하는데 중점을 둔다

    * 일반적으로, 프로퍼티의 키는 문자열이 대부분인 점에 빗대어 본다면, "위의 의도"가 더욱 명료해진다.

    * Symbol은 생성자 함수가 될 수 없다

      (즉, wrapper 객체 형성이 불가능하다. 오직 Symbol 함수를 호출해서 "고유한" Symbol을 생성하는 것이 가능하다)

      * 여러 모듈에서 1개의 Symbol을 공유하고 싶다면, Symbol.for(k) 를 통해 Symbol을 만들면 된다

        => 전역 심볼 레지스트리에, key 가 k이면서 value가 Symbol로서 저장이 되고, 이미 그러한 과정이 이루어진 상태라면, 해당 Symbol을 활용한다.

  * 출처

    * https://it-eldorado.tistory.com/149

* null과 undefined의 차이

  * 둘 다 primitive type으로 취급을 받음
    * 그러나, console.log 상으로는, null은 object 타입이며 undefined는 undefined 타입으로 명시가 되어 있다.
  * undefined는 전역 객체의 속성 값 중 하나
    * 따라서, 변수를 선언하고 값을 할당하지 않을 떄, undefined가 자동으로 할당된다.
  * null은, 전역 객체의 속성 값이 아니다. 어떠한 리터럴 값이다.
    * 객체가 의도적으로 비어 있음을 표현할 떄 활용한다.
  * 출처 : https://2ssue.github.io/common_questions_for_Web_Developer/docs/Javascript/13_undefined&null.html#undefined



## Section 9. 추가 자료형들

### 2,8,16 진법과 비트 연산자

2진법, 8진법, 16진법은 아래와 같이 사용할 수 있다.

```javascript
[
  0b1,
  0b10,
  0b11,
  0b100,
  0b101
].forEach(i => console.log(i))

[
  0o7,
  0o10,
  0o100,
  0o1000,
].forEach(i => console.log(i))

[
  0x9,
  0xA,
  0xB,
  0xC,
  0xd,
  0xe,
  0xf,
  0x10,
  0xFFFFFF
].forEach(i => console.log(i))

```



진법 간 변환

* 10진법 -> n진법 (문자열 로 나타내짐)
* n진법 -> 10진법의 수로 나타낼 수 있다.

```javascript
const num = 123456789;

const binStr = num.toString(2);
const octStr = num.toString(8);
const hexStr = num.toString(16);

console.log(binStr, octStr, hexStr);
//111010110111100110100010101 726746425 75bcd15

console.log(
  parseInt(binStr, 2),
  parseInt(octStr, 8),
  parseInt(hexStr, 16)
);
//123456789 123456789 123456789

// 💡 상호변환
console.log(
  parseInt(hexStr, 16).toString(2),
  parseInt(binStr, 2).toString(8),
  parseInt(octStr, 8).toString(16)
);

//111010110111100110100010101 726746425 75bcd15
```



각종 연산자들

```javascript
let x = 0b1010101010; // 682
let y = 0b1111100000; // 992

//1. &연산자


	// 양쪽 모두 1인 자리에 1
const bitAnd = x & y;

console.log(bitAnd);
console.log(
  bitAnd.toString(2)
);
	//672
	//1010100000



//2. | 연산자
	// 한 쪽이라도 1인 자리에 1
const bitOr = x | y

console.log(bitOr);
console.log(
  bitOr.toString(2)
);
	//1002
	//1111101010


//3. ^연산자
	// 양쪽이 다른 자리에 1
const bitXor = x ^ y;

console.log(bitXor);
console.log(
  bitXor.toString(2)
);
	//330
	//101001010


//4. ~ 연산자
	// 각 비트 반전
console.log(~x);
console.log(
  (~x).toString(2)
);

	//-683
	//-1010101011



//5. 비트 연산자
let x = 0b101; // 5

console.log(x.toString(2), x);
	//101 5

	// 반복 실행해볼 것, 오른쪽 숫자를 늘려 볼 것
x = x << 1;

console.log(x.toString(2), x);
	//1010 10


	// 반복 실행해볼 것, 오른쪽 숫자를 늘려 볼 것
x = x >> 1;

console.log(x.toString(2), x);
	//101 5
```

참고

* ~연산자

  * 정수를 32비트로 나타내었을 때, 각 비트에 대해서 ~연산자를 적용한 꼴이다

    => 각 비트의 값이 1이면 0, 0이면 1로 치환한다.

    * **따라서, a 와 ~a를 2진법 으로서 더하면, 32비트 모든 값이 1이 된다** (즉, "거의 모든 경우" 에서 10진법으로는 -1이 된다.)
      * ** 예외는 맨 아래 참조

  * 32비트 중, 맨 앞의 1비트는 "정수의 부호" 를 나타낸다

    => 따라서, ~연산자를 적용하면 결과값은, 원래의 값과 부호가 반대로 나타난다.

  * 예

    ```javascript
     9 (base 10) = 00000000000000000000000000001001 (base 2)
                   --------------------------------
    ~9 (base 10) = 11111111111111111111111111110110 (base 2) = -10 (base 10)
    ```

  * `~-1` 과 `~(2^32-1)` 은 모두 0으로 계산된다. (위의 정의에 빗대어서 생각)

  * 출처 : [비트 NOT (~) - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Bitwise_NOT)

    

### BigInt

* 개요

  자바스크립트는 모든 수를 Number 형 (또는 BigInt 형)으로 나타낸다.

  => 이는, 자바스크립트는 64bit 형식의 부동소숫점 형식으로 수를 나타내기 때문이다.

  (정확히는 IEEE 754 표준 부동 소수점 방식 활용)

  * 64bit는 크게 아래의 3가지 방식으로 나뉜다.
    * 부호를 나타내는 1 bit (Sign)
    * 지수를 나타내는 11 bits (Exponent)
    * 실제 값을 나타내는 52bits (Mantissa)
    * 실질적인 데이터는 Mantissa로 표현된다

  * ** 참고 : https://jaehyeon48.github.io/computer-architecture/how-computers-represent-numbers/

* 위 64bit를 어떻게 활용하는 가에 따라, "안전하게" 표현할 수 있는 최대값과, 실제로 표현할 수 있는 최대값 개념이 등장한다

  * Number.MAX_SAFE_INTEGER

    * 2^53-1이다.

    * 이는, Mantissa의 52bit의 각 비트가 모두 1일 때 해당이 된다.

      * 기준값 Number.MAX_SAFE_INTEGER 에다가 1,2,3.... 을 순차적으로 더하게 되면, 여기서부터는 결과값이 1,2,3... 더한 결과값을 기대할 수 없게 될 수 있다.

        => 이는, 위 상황에서는 이제 Exponent의 값이 1이상이 되기 때문에, Mantissa를 1씩 더하게 되어도 결국 짝수만큼 더해지기 결과를 초래하기 떄문이다.

        => 이러한 상황에서는, 수를 "신뢰성있게" 표현할 수 없을 것이다.

      * (내 생각) 더해지는 메커니즘이 어떻게 되는지는 잘 모르겠다

        => 실제로 Number.MAX_SAFE_INTEGER 에다가 1,2,3.... 을 더하면 각각의 결과의 규칙을 아직까지는 해석을 못 하겠다.

    * 위의 한계를 극복하려면, Number.MAX_SAFE_INTEGER를 초과하는 수에 대해서는, BigInt 자료형을 써야 한다.

    * 참고

      * https://jaehyeon48.github.io/javascript/max-values/
      * https://stackoverflow.com/questions/307179/what-is-javascripts-highest-integer-value-that-a-number-can-go-to-without-losin#answer-49218637

  * Number.MAX_VALUE

    * 위 부동소수점으로 표현할 수 있는 가장 최대의 수이다.

      * 따라서, Number.MAX_VALUE를 초과하는 수는 Infinity로 표현하게 된다.

        (내 의견) Number.MAX_VALUE 에다가 1이 넘는 수를 곱하면, Infinity로 뜨지만, 반대로 더하게 되면, Infinity로 표현되지 않는다.

        => 곱하는 메커니즘과 더하는 메커니즘이 다르게 계산되는 거 같은데..... 잘 모르겠다.

* BigInt활용

  * ```javascript
    const bigInt1 = 9007199254740991n; // 끝에 n을 붙임
    const bigInt2 = BigInt(9007199254740991);
    const bigInt3 = BigInt('9007199254740991');
    const bigInt4 = BigInt(0x1fffffffffffff) // 9007199254740991
    
    for (let i = 0; i < 100; i++) {
      console.log(bigInt1 + BigInt(i));
    }
    ```

  * number 타입과 산술적인 연산은 불가하나, 비교(<, >, 조건문)은 가능하다.

    * 내 생각) 비교할 때는 암묵적으로 둘 중 하나를 타입변환을 시도하지 않을까? 생각한다.

      => 하지만, 가장 안전하게 하려면 양쪽의 타입을 다 맞추는 것이라고 (지금은) 생각한다.

      => 양 쪽의 숫자가 2^53-1보다 작다면, 타입에 관해 크게 신경 안 써도 되지만, 그렇지 않고 타입이 다르다면, 어떻게 타입변환이 이루어지는지 (혹은 진짜 타입 변환 자체가 이루어지는지)는 잘 모르겠다.

    ```javascript
    console.log(
      1n + 1
    ); //불가능
    
    // 양쪽 모두 BigInt로 변환하여 계산하는 방법 사용
    const calcAsBigInt = (x, y, op) => {
      return op(BigInt(x), BigInt(y));
    }
    
    console.log(
      calcAsBigInt(1n, 1, (x, y) => x + y)
    );
    
    
    //정렬 가능
    console.log(
      [4n, 7, 6n, 3, 1, 5, 9, 2n, 8n]
      .sort((a, b) => a > b ? 1 : -1)
    );
    //[1, 2n, 3, 4n, 5, 6n, 7, 8n, 9]
    ```

  * BigInt끼리는 산술연산이 가능하며, Number 타입으로 변환도 가능하다.

    * 이 때, Number 타입으로 변환할 때에는, 2^53-1보다 큰 수에 대해서는 유실에 주의해야 한다.

      ```javascript
      console.log(
        Number(1n),
        Number(9007199254740993n)
      );
      
      //1 9007199254740992
      ```

* (참고) 아마 BigInt는 부동소숫점 방식이 아니라, 다른 프로그래밍 방식으로 수를 표현하기에, 2^53-1 보다 더 큰 숫자를 표현하는 게 아닐까 생각한다. 



### Symbol

* 개요

  * 유일무이한 존재로서, 다른 Symbol과의 중복을 피할 수 있다
    * 따라서, 프로퍼티의 유일한 키로서 정의할 때 활용이 가능하다
    * 외부에서 Symbol을 호출할 수 없기 때문에, 프로퍼티의 접근 제한 용도로 활용하고 싶다면 key로 Symbol을 쓴다.
  * new 연산자를 통해서 만들 수 없다.

* 활용 예시

  * 기본

    ```javascript
    const mySymbol = Symbol();
    
    console.log(typeof mySymbol, mySymbol);
    
    //symbol Symbol()
    ```

  * 두 심볼은 같지 않다.

    ```javascript
    const symbol1 = Symbol('hello');
    const symbol2 = Symbol('hello');
    
    console.log(symbol1, symbol2);
    
    // ⭐️ 두 심볼은 같지 않다!
    console.log(symbol1 === symbol2);
    ```

  * 객체의 키로서 활용할 때는, []로 감싼다. (키는 보통 문자열로 표현하는데, 이렇게 표현함으로서 문자열과 구분시킬 수 있다)

    * 외부에서 호출이 불가능하므로, 외부에서의 프로퍼티 접근이 제한된다.

    ```javascript
    const obj = {
      [Symbol('x')]: 1,
      [Symbol('y')]: 2
    }
    
    console.log(obj);
    //{Symbol(x): 1, Symbol(y): 2}
    
    // 유일무이한 값이므로 다음과 같이 출력 불가
    console.log(
      obj[Symbol('x')],
      obj[Symbol('y')]
    );
    ```

    * Symbol을 활용해서, 내부에서 프로퍼티 접근을 허용하면서 , 외부에서는 접근 제한이 가능하다

    ```javascript
    const buildingKey = Symbol('secret');
    
    const building = {
      name: '얄코사옥',
      floors: 3,
      [buildingKey]: '1234#'
    }
    
    
    console.log(building);
    //{name: '얄코사옥', floors: 3, Symbol(secret): '1234#'}
    
    console.log(
      building.name,
      building.floors,
      building[buildingKey]
    );
    //얄코사옥 3 1234#
    
    
    // 외부로부터의 접근 차단
    console.log(
      building[Symbol('secret')]
    );
    //undefined
    ```

    * 또한, 프로퍼티의 키가 Symbol이라면, "Symbol" 에 접근할 수 있는 메서드를 활용해야만, 해당 프로퍼티에 접근할 수 있다.

      => Symbol이 키인 프로퍼티는, 접근성 제한이 또한 보장되는 부분이다

    ```javascript
    const buildingKey = Symbol('secret');
    
    const building = {
      name: '얄코사옥',
      floors: 3,
      [buildingKey]: '1234#'
    }
    
    //일반적인 순회나, 일반적인 프로퍼티 관련 메서드로는 key 가 Symbol인 프로퍼티에 접근할 수 없다.
    
    for (key in building) {
      console.log(key);
    }
    //name
    //floors
    
    console.log(
      Object.keys(building),
      Object.values(building),
      Object.entries(building),
      Object.getOwnPropertyNames(building)
    );
    //['name', 'floors']
    //['얄코사옥', 3]
    //[['name', '얄코사옥'], ['floors', 3]]
    //['name', 'floors']
    
    
    //아래의 메서드를 통해서, 키가 Symbol인 프로퍼티들만 다룰 수 있게 된다. 
    
    console.log(
      Object.getOwnPropertySymbols(building),
      Object.getOwnPropertySymbols(building)[0],
    );
    //[Symbol(secret)] Symbol(secret)
    
    console.log(
      building[
        Object.getOwnPropertySymbols(building)[0]
      ]
    );
    //1234#
    ```

* 전역 심볼 레지스트리

  * "키가 중복되지 않은" 심볼들이 저장되는 공간

    => 즉, 찾고자 하는 심볼이 없다면 생성하고, 이미 생성되어 있는 심볼이라면 해당 심볼을 활용한다

    => Symbol()로 생성하게 되면, 위의 역할을 기대할 수 없다.

    => 그러므로, Symbol.for() 함수를 활용하여 위의 역할을 수행하게 된다.

    ```javascript
    // 전역 심볼 레지스트리에 해당 키로 등록된 키가 없을 시:
    // 심볼을 새로 생성
    const symbol1 = Symbol.for('hello');
    
    // 전역 심볼 레지스트리에 해당 키가 존재할 시:
    // 해당 심볼을 반환
    const symbol2 = Symbol.for('hello');
    
    console.log(symbol1 === symbol2);
    //true
    
    //전역 심볼 레지스트리에 있는 심볼을 키로 지정
    const obj = {
      [symbol1]: 'SECRET STRING'
    }
    
    console.log(
      obj[Symbol.for('hello')]
    );
    //SECRET STRING
    ```
  
    심볼의 키를 반환하는 메서드를 활용할 때에는, "전역 심볼 레지스트리" 에 저장된 심볼에 한해서만 가능하다 (그렇지 않은 심볼은, 키를 반환받을 방법이 없다.)
  
    ```javascript
    const symbol1 = Symbol.for('hello');
    const symbol2 = Symbol.for('hello2');
    const symbol3 = Symbol('not');
    
    console.log(Symbol.keyFor(symbol1));
    console.log(Symbol.keyFor(symbol2));
    console.log(Symbol.keyFor(symbol3));
    
    //hello
    //hello2
    //undefined
    ```
  
    
  
  * 전역 심볼 레지스트리 활용 예시
  
    * 표준 빌트인 객체에, 개발자가 직접 만든 메서드를 넣고 싶은 경우에 활용이 가능하다.
  
      => 추후에 해당 기능의 메서드가 개발이 되더라도, 개발자가 정의한 메서드 이름과  중복이 생기는 것을 확실하게 방지할 수 있다.

      ```javascript
      // 숫자 요소들의 평균을 구하는 메서드 추가
      Array.prototype[Symbol.for('average')] = function () {
        let sum = 0, count = 0;
        for (const i of this) {
          if (typeof i !== 'number') continue;
          count++;
          sum += i;
        }
        return sum/count
      }
      
      const v = Symbol.for('average');
      console.log([1, 2, 3, 4, 5, 6][v]());
      //3.5
      ```
  
      * 아래의 경우는, "브라우저"에 한번에 입력하면 에러가 뜬다.
  
        (`console.log([1,2,3,4,5,6][Symbol.for('average')]())` 이 부분을 따로 치면 에러가 발생하지 않는다.)
  
        => 왜 그런지는 모르겠다.
  
        => 또한, 리터럴 객체 대신, new Array(1,2,3,4,5,6) 으로 바꾼 후, 한 화면에 치면 에러가 발생하지 않는다. (왜 그런지는 아직 모르겠음)
  
        ```javascript
        // 숫자 요소들의 평균을 구하는 메서드 추가
        Array.prototype[Symbol.for('average')] = function () {
          let sum = 0, count = 0;
          for (const i of this) {
            if (typeof i !== 'number') continue;
            count++;
            sum += i;
          }
          return sum/count
        }
        
        
        [1, 2, 3, 4, 5, 6][Symbol.for('average')]();
        //Uncaught TypeError: Cannot read properties of undefined (reading 'Symbol(average)')
            at <anonymous>:13:19
        ```
  





## 섹션10. 이터러블과 제너레이터

### Set

정의

* 값들의 순서가 무의미하며, 동일한 값을 여러 번 포함할 수 없다.

```javascript
// Set 생성
const set1 = new Set();

// add 메서드 - 요소 추가
set1.add(1);
set1.add('A');
set1.add(true);

console.log(set1);

// 이미 포함된 요소는 추가하지 않음
set1.add(1);
set1.add(true);

console.log(set1);




// 배열을 인자 넣으면 생성 + 초기화
// 중복된 요소 제거
const set2 = new Set([1, 1, 1, 'A', true]);

console.log(set2);
//Set(3) {1, 'A', true}

// has 메서드 - 요소 포함여부 확인
console.log(
  set2.has(1),
  set2.has('A'),
  set2.has(4)
);
//true true false


// delete 메서드 - 요소 제거 & 성공 여부 반환
console.log(
  set2.delete('A'),
  set2.delete(true),
  set2.delete(100)
);
//true true false

console.log(set2);
//Set(1) {1}

// add 메서드는 결과 셋을 반환
const set3 = set2.add(2);

console.log(set3);

// 💡 메서드 체이닝을 할 수 있다는 의미
set2
.add(3)
.add(4)
.add(5)

// 참조형이므로 둘이 같은 Set을 가리킴
console.log(set2, set3);


// size 프로퍼티 - 요소의 개수
console.log(
  set2.size
);


// keys, values, entries 메서드 - 값 / 값 / [값, 값] 반환
// key를 value와 같이 취급
console.log(
  set2.keys(),
  set2.values(),
  set2.entries()
);

//SetIterator {1, 2, 3, 4, 5} 
//SetIterator {1, 2, 3, 4, 5} 
//SetIterator {1 => 1, 2 => 2, 3 => 3, 4 => 4, 5 => 5} //key와 value가 같다.


```

참조형 데이터를 추가하는 경우는, 코드를 어떻게 작성하느냐에 따라 다른 데이터로 인식하기도 하고, 같은 데이터로 인식하기도 한다.

```javascript
const objSet1 = new Set()
.add({ x: 1, y: 2 })
.add({ x: 1, y: 2 })
.add([1, 2, 3])
.add([1, 2, 3]);

// 각기 다른 것으로 인식 (참조하는 주소가 다르므로)
console.log(objSet1);
//Set(4) {{…}, {…}, Array(3), Array(3)}


const obj = { x: 1, y: 2 };
const arr = [1, 2, 3];

const objSet2 = new Set()
.add(obj)
.add(obj)
.add(arr)
.add(arr);

// 같은 것들로 인식
console.log(objSet2)
//Set(2) {{…}, Array(3)}
```



이터러블로서의 Set

* Set은 Iterable한 객체이므로, for...of 문 사용이 가능하다.
* 스프레드를 활용하여, 중복된 원소가 포함된 배열의 모든 원소를, Set으로 옮기는 것이 가능하다.

```javascript
const arr = ['A', 'B', 'C', 'D', 'E'];
const set = new Set(arr);

for (item of set) {
  console.log(item);
}
//A
//B
//C
//D
//E

const newArr = [...set];

console.log(newArr);
//(5) ['A', 'B', 'C', 'D', 'E']

// 활용 - 중복을 제거한 배열 반환
const arr1 = [1, 1, 1, 2, 2, 3, 4, 5];

const arr2 = [...new Set(arr1)];

console.log(arr2);
//(5) [1, 2, 3, 4, 5]



const [x, y] = set;
console.log(x);
console.log(y);
//A
//B


const [a, b, ...rest] = set;

console.log(a);
console.log(b);
console.log(rest);
//A
//B
//['C', 'D', 'E']
```

forEach() 메서드 사용 가능

```javascript
const set = new Set(['A', 'B', 'C', 'D', 'E']);

// ⚠️ 두 번째 인자가 인덱스가 아님!
// 배열과 달리 순서 개념이 없으므로...
// 형식을 맞추기 위한 인자일 뿐

set.forEach(console.log);

// 아래의 결과와 같음
// set.forEach((item, idx, set) => {
//   console.log(item, idx, set)
// });


//A A Set(5) {'A', 'B', 'C', 'D', 'E'}
//B B Set(5) {'A', 'B', 'C', 'D', 'E'}
//C C Set(5) {'A', 'B', 'C', 'D', 'E'}
//D D Set(5) {'A', 'B', 'C', 'D', 'E'}
//E E Set(5) {'A', 'B', 'C', 'D', 'E'}

```



### Map

개요

* 키와 쌍으로 이루어진 컬렉션



map을 생성하는 데에는 아래의 2가지 방법이 존재한다.,

* set() 함수로 key-value를 설정하는 경우
* 배열로 생성

```javascript
// Map 생성
const map1 = new Map();

// set 메서드 - 키와 값의 쌍 추가
map1.set('x', 1);
map1.set(123, 'ABC');
map1.set(true, { a: 1, b: 2 });

console.log(map1);
// Map(3) {'x' => 1, 123 => 'ABC', true => { a: 1, b: 2 }}


// [[키 쌍]...] 배열로 생성 + 초기화
const map2 = new Map([
  ['x', 1],
  [123, 'ABC'],
  [true, { a: 1, b: 2 }],
]);

console.log(map2);
// Map(3) {'x' => 1, 123 => 'ABC', true => { a: 1, b: 2 }}
```

그리고, map 객체는 key,value에 대해서 아래의 기능 역시 수행

* 원하는 key를 가졌는지 확인이 가능하며, 모든 객체를 key로 가질 수 있다. (Object와 가장 큰 차이)

* key-value를 추가, 삭제 가 가능하며, 갯수를 다 count할 수 있음.

```javascript
// 키의 중복 불허 - 해당 키 있을 시 덮어씀
map2.set('x', 2);

console.log(map2);

// has 메서드 - 요소 포함여부 확인
console.log (
  map2.has('x'),
  map2.has('y')
);
//true false

// get 메서드 - 값에 접근
console.log(
  map2.get('x'),
  map2.get(123),
  map2.get(true),

  // 없는 키로 접근시
  map2.get('y')
);
//2 'ABC' {a: 1, b: 2} undefined



// 💡 참조값도 키로 사용 가능
const objKey = { x: 1, y: 2 };
const arrKey = [1, 2, 3];

map2.set(objKey, 'OBJ_KEY');
map2.set(arrKey, 'ARR_KEY');

console.log(map2);
//Map(5) {'x' => 2, 123 => 'ABC', true => {…}, {…} => 'OBJ_KEY', Array(3) => 'ARR_KEY'}


// ⚠️ [참조값]이 키임에 유의 => 아래의 경우, 원하는 결과를 얻을 수 없다.
// 💡 5-1강의 객체와 비교해 볼 것
console.log(
  map2.get({ x: 1, y: 2 }),
  map2.get([1, 2, 3])
);
//undefined undefined

// 또한, map 객체의 각 요소를 추가,삭제할 수 있으며, map 객체의 요소 갯수를 정확하게 간편히 count할 수 있다.



// delete 메서드 - 요소 제거 & 성공 여부 반환
console.log(
  map2.delete('x'),
  map2.delete(objKey),
  map2.delete({x: 3, y: 4})
);
console.log(map2);
//true true false
//Map(3) {123 => 'ABC', true => {…}, Array(3) => 'ARR_KEY'}


// add 메서드는 결과 맵을 반환
// 💡 메서드 체이닝을 할 수 있다는 의미
const map3 = map2
.set(1, 'X')
.set(2, 'Y')
.set(3, 'Z');

console.log(map2, map3);
//Map(6) {123 => 'ABC', true => {…}, Array(3) => 'ARR_KEY', 1 => 'X', 2 => 'Y', …}
//Map(6) {123 => 'ABC', true => {…}, Array(3) => 'ARR_KEY', 1 => 'X', 2 => 'Y', …}



//map 객체의 요소가 몇 개인지, "type"에 관계하지 않고 정확하게 다 셀 수 있다.
// size 프로퍼티 - 요소의 개수
console.log(
  map2.size
);
//6


//map의 키,값,entries들을 모두 반환하는 함수 존재
//이 때 MapIterator 타입이다. (의문 : 실제로 이런 타입은 없던데, 콘솔창에 이렇게 뜨길래 일단 정리함)
// keys, values, entries 메서드 - 키 / 값 / [키, 값] 반환
console.log(
  map2.keys(),
  map2.values(),
  map2.entries()
);
//MapIterator {123, true, Array(3), 1, 2, …} 
//MapIterator {'ABC', {…}, 'ARR_KEY', 'X', 'Y', …} 
//MapIterator {123 => 'ABC', true => {…}, Array(3) => 'ARR_KEY', 1 => 'X', 2 => 'Y', …}


// clear 메서드 - 모든 요소들을 삭제
map2.clear();

console.log(map2, map3);
```



map 객체는 iterable 하므로, 각 key-value를 순환할 수 있다.

```javascript
const arr = [
  ['🐶', '강아지'],
  ['🐱', '고양이'],
  ['🐯', '호랑이'],
  ['🐵', '원숭이'],
  ['🐨', '코알라']
];
const map = new Map(arr);

for ([key, value] of map) {
  console.log(key, value);
}

//디스트럭쳐링
const [a, b, ...rest] = map;

console.log(a);
console.log(b);
console.log(rest);


// 아래의 결과와 같음
// map.forEach((item, idx, set) => {
//   console.log(item, idx, set)
// });
map.forEach(console.log);
```







가장 큰 궁금증

* Object와 Map의 차이점

  * 위의 의문을 생각하게 된 계기
    * Object는 각 프로퍼티가 key-value로서 이루어져 있고, Map 함수로 만들어진 map 타입의 객체 역시 key-value를 활용한다
    * 그렇다면, 굳이 별도의 map 객체를 정의해야 할 필요가 있을까? 하는 생각이 든다
  * 차이점 1. key 값
    * Object는 key 값으로 사실상 string이나 Symbol만 가능
    * map은 key값으로 모든 타입이 가능 => Object 역시 가능
  * 차이점 2. key - value 삽입 순서
    * Object는 삽입한 프로퍼티 순서대로 key가 항상 정렬되지는 않는다
    * Map은 삽입한 프로퍼티 순서대로 key가 정렬된다.
  * 차이점 3. 빈번한 key-value 삽입/삭제 시
    * (내 생각) 이 부분은 확인이 필요하다. 이론적으로 밝히기에는 쉽지가 않다
    * Object는 빈번한 추가/삭제 에 대한 최적화가 되어 있지 않다
    * Map은 빈번한 추가/삭제 에 대한 최적화가 되어 있다

  * 차이점 4. Iteration / Enumerable 여부
    * Map은 Iterable 하다.
    * Object는 Iterable 하지 않고, Enumerable 하다
      * 따라서, for ... in 구문이나 Object.keys() 함수를 써야 한다
  * 차이점 5. JSON 변환 여부
    * Object는 JSON 직렬화/역직렬화가 가능
    * map은 JSON 직렬화/역직렬화가 "바로는" 불가능. (다만, JSON.stringify() 나 JSON.parse() 의 2번쨰 인자 함수를 통해서, 조정해서 직렬화를 할 수는 있다.)
  * 차이점 6. 사이즈 크기 구하기
    * Object는 프로퍼티의 갯수를 구하는 것을 수동으로 해야 한다
      * 열거 불가능하거나, Symbol이 있거나...... 등의 변수가 있기 떄문
    * Map은 size() 의 함수를 통해, 크기를 정확하게 구할 수 있다.

  * 출처
    * https://velog.io/@namda-on/JavaScript-Map-%EA%B3%BC-Object-%EC%9D%98-%EC%B0%A8%EC%9D%B4
    * (Map 과 Object의 성능 차이에 대해 직접 실험으로 확인하는 예시)
      * https://velog.io/@oneook/%EB%B2%88%EC%97%AD-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Map%EC%9D%84-Object-%EB%8C%80%EC%8B%A0-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC%ED%95%A0-%EB%95%8C%EB%8A%94-%EC%96%B8%EC%A0%9C%EC%9D%BC%EA%B9%8C%EC%9A%94



* 참고
  * for... in 과 for... of의 차이점
    * for... in은 객체의 Enumerable한 프로퍼티에 대해 반복순회, for... of는 iterable한 객체에 대해 key-Value를 반복 순회
    * 출처 : https://velog.io/@bining/javascript-for-in-for-of-forEach-%EC%B0%A8%EC%9D%B4%EC%A0%90
    * https://velog.io/@adguy/for..in-vs-for..of-Enumerable-vs-Iterable-%EC%9A%94%EB%85%80%EC%84%9D%EB%93%A4%EC%97%90-%EB%8C%80%ED%95%9C-%EB%82%98%EB%A6%84%EC%9D%98-%EA%B3%A0%EC%B0%B0





## 섹션 11. 문제들에 대비하기

### 에러 핸들링

개요

* 코드 실행 중, 에러가 발생하게 되면, 에러 메세지를 띄우면서 뒤의 코드는 실행되지 않는다

  => 따라서, 코드의 흐름을 계속 유지하고 싶다면, try - catch 문을 활용하자.

  * ```javascript
    console.log('에러 발생 전');
    
    // ⚠️ 오류를 발생시키는 코드
    (3).split('');
    
    // 출력되지 않음
    console.log('에러 발생 후');
    
    
    
    //결과는 아래와 같다
    
    //에러 발생 전
    //Uncaught TypeError: 3.split is not a function at <anonymous>:4:5
    ```

    => "에러 발생 후" 는 안 찍힘을 알 수 있다.

  * ```javascript
    //try - catch 문 적용
    
    console.log('에러 발생 전');
    
    try {
      (3).split('');
    
    } catch (e) {
      console.error('🛑 에러!!', e);
    }
    
    console.log('에러 발생 후');
    
    
    //에러 발생 전
    //🛑 에러!! TypeError: 3.split is not a function at <anonymous>:6:7
    //에러 발생 후
    ```

    => 코드 흐름이 정상적으로 유지가 됨을 확인할 수 있다.

  * try - catch 문을 응용한다면, 배열의 요소 중, 문자열에 해당하는 것만 각 문자를 담은 배열을 반환하고, 문자열이 아니면 빈 배열을 반환하는 로직을 짤 수 있다.

    ```javascript
    const arr = ['ABC', '가나다', 123, '123'];
    
    function getLetterArray (str) {
      // 💡 인자로 어떤 타입의 값이 주어질지 모르는 상황
      try {
        return str.split('');
    
      } catch (e) {
        console.error('🛑 에러!!', e);
        return [];
      }
    }
    
    arr.forEach(i => {
      console.log(getLetterArray(i));
    });
    
    //['A', 'B', 'C']
    //['가', '나', '다']
    //🛑 에러!! TypeError: str.split is not a function at getLetterArray (<anonymous>:6:16) at <anonymous>:15:15 at Array.forEach (<anonymous>)at <anonymous>:14:5       
    //[]
    //['1', '2', '3']
    ```

  * try - catch를 실행하고 나서, 반드시 실행되고자 하는 구문을 추가하고자 할 떄는, try - catch - finally 구문을 사용하자

    => try나 catch 문에 return 구문이 있어도, finally 구문이 반드시 실행된다는 점이 주목된다.

    ```javascript
    function connect () { console.log('☀️', '통신 연결'); }
    function disconnect () { console.log('🌙', '통신 연결 해제'); }
    function sendArray (arr) { console.log('전송', arr); }
    
    function sendStringAsArray (str) {
      connect();
    
      try {
        sendArray(str.split(''));
        return true;
    
      } catch (e) {
        console.error('🛑 에러!!', e);
        return false;
    
      } finally {
        // 💡 전송 성공 여부와 관계없이 연결은 끊어야 함
        disconnect();
        console.log('- - - - - - - -');
      }
    
      // ❓ 이곳에 넣는 것과 무엇이 다른가?
      // 아래로 대체하여 실행해 볼 것
      // disconnect();
      // console.log('- - - - - - - -');
    }
    
    ['ABC', '가나다', 123, '123'].forEach(i => {
      console.log(
        sendStringAsArray(i) 
        ? '[성공]' : '[실패]', '\n\n'
      );
    });
    
    
    
    //☀️ 통신 연결
    //전송 (3) ['A', 'B', 'C']
    //🌙 통신 연결 해제
    //- - - - - - - -
    //[성공] 
    
    
    //☀️ 통신 연결
    //전송 (3) ['가', '나', '다']
    //🌙 통신 연결 해제
    //- - - - - - - -
    //[성공] 
    
    
    //☀️ 통신 연결
    //🛑 에러!! TypeError: str.split is not a function
    //    at sendStringAsArray (<anonymous>:9:19)
    //    at <anonymous>:30:5
    //    at Array.forEach (<anonymous>)
    //    at <anonymous>:28:28
    //sendStringAsArray
    //(anonymous)
    //(anonymous)
    //🌙 통신 연결 해제
    //- - - - - - - -
    //[실패] 
    
    
    //☀️ 통신 연결
    //전송 ['1', '2', '3']
    //🌙 통신 연결 해제
    //- - - - - - - -
    //[성공] 
    
    ```

* Error 객체

  * 직접 생성하는 것이 가능

  * 2번째 인자로 cause 프로퍼티를 추가할 수 있다. (MDN 스펙에 명시되어 있음)

    * (실험 결과) cause 이름 외에 다른 이름의 프로퍼티를 추가하려고 하면, 무시된다. (아마 내부적으로 그렇게 짜여져 있지 않았나 싶다.)

      => (내 생각) cause 프로퍼티 이름 자체가 회색이며, error.xxx 로 다른 임의의 프로퍼티를 추가할 때 노란색인 걸 보면(엣지 기준), cause 프로퍼티는 내부적으로 특별한 프로퍼티로서 간주되는 듯 하다.

    ```javascript
    const error = new Error('뭔가 잘못됐어');
    
    console.dir(error);
    //Error: 뭔가 잘못됐어at <anonymous>:1:13
    //	message: "뭔가 잘못됐어"
    //	stack: "Error: 뭔가 잘못됐어\n    at <anonymous>:1:13"
    //	[[Prototype]]: Object
    //		constructor: ƒ Error()
    //		message: ""
    //		name: "Error"
    //		toString: ƒ toString()
    //		[[Prototype]]: Object
    
    
    
    // 두 번째 인자로 이유를 명시할 수도 있음
    const error = new Error(
      '뭔가 잘못됐어',
      { cause: '뭘 잘못했으니까' }
    );
    
    console.dir(error);
    //cause 프로퍼티는, 프로토타입에 정의된 걸 덮어씌우지 않고, 객체의 프로퍼티로서 추가된다. (즉, error.cause로 cause 프로퍼티를 호출할 때, 이 때부터는 객체의 프로퍼티의 cause가 호출이 된다.)
    ```

  * 기본 인스턴스 프로퍼티 및 메서드는 아래와 같으며, 의도적으로 에러를 발생시키는 것도 가능하다.

    ```javascript
    // 두 번째 인자로 이유를 명시할 수도 있음
    const error = new Error(
      '뭔가 잘못됐어',
      { cause: '뭘 잘못했으니까' }
    );
    
    console.log(error.name);
    console.log(error.message);
    
    // cause를 입력했을 경우
    console.log(error.cause);
    
    // 에러 자체를 로그 출력하면 나오는 문구
    console.log(error.toString());
    
    
    
    //Error
    //뭔가 잘못됐어
    //뭘 잘못했으니까
    //Error: 뭔가 잘못됐어
    ```

    ```javascript
    //의도적으로 에러 발생시키기
    throw new Error('이유를 묻지 마라');
    ```

* 에러의 여러 종류

  * 여러 종류의 에러들이 있으나, 모두 Error (정확하게는 Error function 이라고 하는 게 맞지 않나..... 라는 게 내 생각)를 상속받는다

    * SyntaxError
    * TypeError
    * ReferenceError
    * RangeError
    * 이외 여러 가지 Error 참고 : [Error - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Error#오류_유형)

  * 에러의 예시

    * ```javascript
      const x x;
      //Uncaught SyntaxError: Missing initializer in const declaration
      ```

    * ```
      const errorFuncs = [
        // 자료형에 맞지 않는 메서드 호출
        () => { (3).split(''); },
      
        // 선언되지 않은 함수 호출
        () => { hello(); },
      
        // 부적절한 숫자를 인자로 전달
        () => { (123.45).toFixed(-1); }
      ];
      ```

    * ```javascript
      //에러를 출력
      const errorFuncs = [
        // 자료형에 맞지 않는 메서드 호출
        () => { (3).split(''); },
      
        // 선언되지 않은 함수 호출
        () => { hello(); },
      
        // 부적절한 숫자를 인자로 전달
        () => { (123.45).toFixed(-1); }
      ];
      
      errorFuncs.forEach(func => {
        try {
          func();
      
        } catch (e) {
          console.error(e);
          console.log(e.name);
          console.log(e.message, '\n\n');
        }
      });
      
      
      //TypeError: 3.split is not a function
      //TypeError
      //3.split is not a function 
      
      //ReferenceError: hello is not defined
      //ReferenceError
      //hello is not defined
      
      //RangeError: toFixed() digits argument must be between 0 and 100
      //RangeError
      //toFixed() digits argument must be between 0 and 100
      
      ```

  * 에러의 종류에 따라 대처하는 코드(에러 발생 시, 흐름이 끊어지지 않게끔 짠 코드)

    ```javascript
    const errorFuncs = [
      // 자료형에 맞지 않는 메서드 호출
      () => { (3).split(''); },
    
      // 선언되지 않은 함수 호출
      () => { hello(); },
    
      // 부적절한 숫자를 인자로 전달
      () => { (123.45).toFixed(-1); }
    ];
    
    errorFuncs.forEach(func => {
      try {
        func();
    
      } catch (e) {
        if (e instanceof TypeError) {
          console.error('자료형 확인하세요.');
          return;
        }
        if (e instanceof ReferenceError) {
          console.error('선언 안 된 거 쓴 거 없는지 확인하세요.');
          return;
        }
        console.error('아니, 뭘 한 거에요?');
      }
    });
    
    //자료형 확인하세요.
    //선언 안 된 거 쓴 거 없는지 확인하세요.
    //아니, 뭘 한 거에요?
    ```

  * 에러를 수동으로 생성하여, 개발자가 원하는 형식의 데이터만 받도록 코드를 짤 수 있다.

    ```javascript
    // 특정 월의 당번으로 지원하는 함수
    function applyForMonth (date) {
      try {
        if (typeof date !== 'number') {
          throw new TypeError('숫자로 입력해주세요.');
        }
        if (date < 1 || date > 12) {
          throw new RangeError('유효한 월을 입력해주세요.');
        }
    
        console.log(`${date}월 당번으로 등록되셨습니다.`);
    
      } catch (e) {
        console.error('🛑 에러 발생!', e);
        console.log('다시 등록해주세요.');
      }
    }
    
    applyForMonth(5);
    applyForMonth('5');
    applyForMonth(13);
    
    //5월 당번으로 등록되셨습니다
    
    //🛑 에러 발생! TypeError: 숫자로 입력해주세요.
    //다시 등록해주세요.
    
    //🛑 에러 발생! RangeError: 유효한 월을 입력해주세요.
    //다시 등록해주세요.
    ```

* 커스텀 에러 만들기

  * Error (function)을 상속받은 새로운 Error 클래스를 정의할 수 있다.

    * 참고 : function을 상속받은 클래스를 정의하는 것이 가능하다. (실험해 봄)

    * 아래의 경우는, 계급(position)과 말한 단어(word)를 입력받을 때, word의 끝이 다/까로 끝나지 않으면, position에 따라 각기 다른 error message를 출력하는 코드를 보여준다

      ```javascript
      class MilitaryError extends Error {
        constructor (position, ...params) {
          super(...params); // 이 때, MilitaryError 내의 message 프로퍼티가 정의된다.
      
          this.name = 'MilitaryError';
      
          switch (position) {
            case '이병':
              this.message = '개판이군. 맞선임 데려와봐.';
              break;
            case '일병':
              this.message += ' 엎드려 뻗쳐.';
              break;
            case '상병':
              this.message = '짬을 거꾸로 먹었나. ' + this.message;
              break;
            default:
              this.message = '집에 갈 때 됐다 이거지? ㅎㅎ';
          }
        }
      }
      
      class Soldier {
        constructor (position) {
          this.position = position;
        }
      
        speak (word) {
          console.log(this.position + ':', word);
          try {
            if (!'다나까'.includes(word.at(-1))) {
              throw new MilitaryError(
                this.position,
                '군대에서 모든 말은 다나까로 끝낸다.'
              );
            }
      
          } catch (e) {
            console.error(e);
          }
        }
      }
      
      ['이병', '일병', '상병', '병장'].forEach(pos => {
        const soldier = new Soldier(pos);
        soldier.speak('무슨 일입니까');
        soldier.speak('왜요');
      });
      ```

* 에러 버블링을 활용하여 로직 짜기

  * 에러를 발생시키면, 해당 함수 내에서 처리 못하면 호출된 곳으로 에러가 넘어가게 된다.

    * 이를 활용하여, 에러가 주어진다면, 사장을 제외한 아래 직급에서 해결할 수 있는 에러는, 제일 말단에서 처리되도록
    * if문에서, undefined는 false로 인식하며, null이 아닌 모든 객체는 treue로 인식함을 활용 (심지어 error 객체도 true로 인식)

    ```javascript
    function func1 (e) { // 사원
      try {
        console.log(e);
        if (e) { throw e }
        console.log('저 가 봐도 되죠?');
        console.log('- - - - - - - - - -');
    
      } catch (e) {
        if (e instanceof SyntaxError) {
          console.error('저 이건 알아요!', e);
          console.log('- - - - - - - - - -');
          return;
        }
        console.log('대리님, 이거 뭐에요?');
        throw e; // 💡 처리하지 못하는 에러는 윗선으로 던짐
      }
    }
    
    function func2 (e) { // 대리
      try {
        func1(e);
      } catch (e) {
        if (e instanceof TypeError) {
          console.error('내가 할 테니 가봐요.', e);
          console.log('- - - - - - - - - -');
          return;
        }
        console.log('부장님, 이건 제 선에서 안 되겠습니다.');
        throw e;
      }
    }
    
    function func3 (e) { // 부장
      try {
        func2(e);
      } catch (e) {
        if (e instanceof ReferenceError) {
          console.error('잘 하자, 응?', e);
          console.log('- - - - - - - - - -');
          return;
        }
        console.log('사장님, 이것 좀 보셔야겠습니다.');
        throw e;
      }
    }
    
    function func4 (e) { // 사장
      try {
        func3(e);
    
      } catch (e) {
        console.error('전원 집합.', e);
      }
    }
    
    func4(); //이 떄 e가 undefined이므로, if이 false가 된다.
    //저 가 봐도 되죠?
    //- - - - - - - - - -
    
    func4(new SyntaxError());
    //저 이건 알아요! SyntaxError
    //- - - - - - - - - -
    
    func4(new TypeError());
    //대리님, 이거 뭐에요?
    //내가 할 테니 가봐요. TypeError
    //- - - - - - - - - -
    
    func4(new ReferenceError);
    //대리님, 이거 뭐에요?
    //부장님, 이건 제 선에서 안 되겠습니다.
    //잘 하자, 응? ReferenceError
    //- - - - - - - - - -
    
    func4(new RangeError);
    //대리님, 이거 뭐에요?
    //부장님, 이건 제 선에서 안 되겠습니다.
    //사장님, 이것 좀 보셔야겠습니다.
    //전원 집합. RangeError
    ```



참고

* constructor 활용 시, super()를 활용하면, super()를 호출하는 주체는 자식 객체이다.

  * 따라서, 부모 constructor 내부에 정의된 프로퍼티 정의 코드들은, 자식 객체의 프로퍼티로 자동으로 할당한다. (이 경우 부모 constructor 내부의 this는 자식 객체이기 때문이다.)
* 실험해보니, function을 상속받은 클래스를 정의하는 것이 가능하다.
  * (내 생각 - 클래스의 prototype이 function, 즉 prototype으로 상속을 정의하니까 가능하지 않을까... 생각한다.)




### 구시대의 유물 var

* var과 let/const와의 차이점

  * 미리 선언한 변수가 없는 상태에서, 변수 정의 시, 기본적으로 var로 선언된다.

    ```javascript
    notDeclared = 1; // 미리 선언한 부분이 없을 시 var로 만들어짐
    console.log(notDeclared);
    
    // num이 var로 선언된 것
    for (num of [1, 2, 3]) {
      console.log(num);
    }
    ```

  * var로 선언한 변수는 재선언이 가능하나, let이나 const로 선언한 변수는 재선언을 하면 오류가 발생한다.

    ```javascript
    let a = 1;
    let a = 2; // ⚠️ 오류
    ```

    ````javascript
    const b = 1;
    const b = 2; // ⚠️ 오류
    ````

    ```javascript
    var c = 1;
    var c = 2;
    ```

    * (내 생각) ES6으로 들어오면서 코딩의 실수를 줄이기 위해서, var와 달리 재선언을 막은 것이 아닐까.... 라는 생각이 든다.

  * var로 선언한 변수는 블록 scope가 무시되며, let/const로 선언한 변수는 블록 scope에 따라 변수의 값이 달라진다.

    * 이는 for문 scope에 대해서도 동일하게 적용된다.

      * ```javascript
        let num1 = 1;
        {
          let num1 = 2;
          {
            let num1 = 3;
          }
        }
        
        console.log(num1);
        //1
        
        var num2 = 1;
        {
          var num2 = 2;
          {
            var num2 = 3;
          }
        }
        
        console.log(num2);
        //3
        ```

      * ```javascript
        // for문의 스코프도 무시
        for (var i = 0; i < 5; i++) {
          var pow2 = i ** 2;
          console.log(pow2);
        }
        
        console.log(i, pow2);
        
        //0
        //1
        //4
        //9
        //16
        //5 16
        ```

      * 다만, 함수 scope에 대해서는, var로 선언한 변수일지라도, 해당 함수의 scope내에서만 변수가 유효하다.

        ```javascript
        var num3 = 1;
        
        function func1 () {
          var num3 = 2;
          return num3;
        }
        
        console.log(num3); //1
        console.log(func1()); //2
        ```

  * var로 선언된 변수나 const/let으로 선언된 변수 모두 hoisting이 된다.

    * 다만, var로 선언된 변수는 undefined로 초기화되어 console에 찍을 수 있지만, let/const로 선언된 변수는 uninitialized로 (맞는지 확인) 초기화되므로 이 변수를 console에 찍으려고 하면 에러 발생.
    * (확인해보니) let도 hoisting이 되지만, TDZ에 속해서 오류가 생긴다고 한다.



### 엄격 모드

* 문서나, 함수 최상단에 'use strict' 를 작성해서 사용한다. (꼭 최상단에 사용하여야만 한다.)

  ```javascript
  notDeclared = 1; // 💡 암묵적으로 전역 var 변수로 선언
  ```

  ```javascript
  // ⚠️ 새로고침 후 실행해볼 것
  // 선언되지 않은 변수 사용 금지
  'use strict'; // 쌍따옴표도 가능
  
  notDeclared = 1; // 오류 발생!
  
  //Uncaught ReferenceError: notDeclared is not defined at <anonymous>:5:13
  ```

  ```javascript
  //'use strict' 를 함수 내부의 최상단에 작성 시, 해당 함수 내에서만 엄격모드가 작동된다.
  
  notDec1 = 1;
  
  function strictFunc () {
  'use strict';
  
   notDec2 = 2;
   console.log(notDec2);
  }
  
  console.log(notDec1);
  strictFunc();
  
  //1
  //Uncaught ReferenceError: notDec2 is not defined at strictFunc (<anonymous>:6:10) at <anonymous>:11:1
  ```

  

* 엄격 모드는, 태그별 or 문서별로만 동작함.

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  <head>
  <script src="./1.js"></script>
  <script src="./2.js"></script>
  </head>
  </html>
  ```

  ```javascript
  // 1.js
  'use strict';
  x = 1;
  console.log(x); // 오류 발생
  ```

  ```javascript
  // 2.js
  y = 2;
  console.log(y); // 오류 발생하지 않음
  ```

* 엄격 모드에서는, 삭제 불가한 것을 삭제 시 오류가 발생한다.

  * 삭제 불가한 것의 예로는, 변수, 함수, 인자 등이 해당된다.

  ```javascript
  // 실제로 지워지지도 않지만 오류를 발생시키지도 않음
  
  let toDelete1 = 1;
  delete toDelete1;
  
  console.log('1.', toDelete1);
  
  //1. 1
  ```

  ```javascript
  function funcToDel1 () { console.log(true); }
  delete funcToDel1;
  
  console.log('2.', funcToDel1);
  
  //2. ƒ funcToDel1 () { console.log(true); }
  ```

  ```javascript
  'use strict';
  
  let toDelete2 = 1;
  delete toDelete2;
  
  //Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.
  ```

* 엄격 모드에서는, 인자명이 중복된 경우 오류가 발생한다.

  * (내 생각) 함수에 대해, 동일한 이름의 인자를 2개 이상 받게 되면, 맨 나중에 지정된 인자의 값이 최종적으로 할당되는 듯 하다.

    ```javascript
    function add(x, x) {
      return x + x;
    }
    
    console.log(add(1, 2));
    
    //4
    ```

    ```javascript
    'use strict';
    
    function add2(x, x) {
      return x + x;
    }
    
    console.log(add2(1, 2));
    
    //Uncaught SyntaxError: Duplicate parameter name not allowed in this context
    ```





### 옵셔널 체이닝

* 존재하지 않은 값이나, 정체를 확실히 모르는 데이터에 대해서, 프로퍼티를 호출할 때 발생하는 에러를 방지하는 법이다.

  * 아래의 경우, 에러가 발생한다.

    ```javascript
    // undefined로부터 값에 접근할 때
    let undefObj;
    console.log(undefObj.x);
    ```

    ```javascript
    // null부터 값에 접근할 때
    let nullObj = null;
    console.log(nullObj.x);
    ```

    ```javascript
    // 무효한 배열에 접근할 때
    let undefArry;
    console.log(undefArry[1]);
    ```

    ```javascript
    // 존재하지 않는 함수를 호출할 때
    let noFunc = {}
    noFunc.func();
    ```

  * 아래의 경우, prop3이 있을 수도 있고, 없을 수도 있다. 

    * 없다면, 에러가 발생하게 되므로, 이러한 경우까지 다룰 수 있는 코드 작성이 필요하다.

      ```javascript
      // 최소 undefined
      // 최대 {prop1:{prop2:{prop3:'성공!'}}}
      // 까지 반환하는 함수
      const rand = () => Math.random() < 0.75;
      
      const notSure = () => rand() ? {
        prop1: rand() ? {
          prop2: rand() ? {
            prop3: rand() ? '성공!' : undefined
          } : undefined
        } : undefined
      } : undefined;
      
      //prop3이 없을 수도 있다.
      
      console.log(JSON.stringify(notSure())); //값이 undefined 인 프로퍼티는, 직렬화될 때, 무시된다.
      ```

      ```javascript
      const result = notSure();
      console.log(JSON.stringify(result));
      
      // ⚠️ 바로 접근하려 할 시에는 실패시 에러
      console.log(result.prop1.prop2.prop3);
      ```

    * prop3이 없는 경우까지 다루는 코드는 아래와 같이 작성할 수 있다.,

      * undefined는 falsy 한 성질을 이용

        ```javascript
        // 방법 1
        const result = notSure();
        
        if (result) {
          if (result.prop1) {
            if (result.prop1.prop2) {
              console.log(result.prop1.prop2.prop3);
            }
          }
        }
        ```

      * && 연산자 이용 (맨 마지막의 데이터가 출력되거나, falsy한 맨 첫번째 데이터가 출력되는 점을 이용)

        ```javascript
        // 방법 2
        const result = notSure();
        
        console.log(
          result
          && result.prop1
          && result.prop1.prop2
          && result.prop1.prop2.prop3
        );
        ```

      * try - catch 활용

        ```javascript
        // 방법 3
        const result = notSure();
        
        try {
          console.log(result.prop1.prop2.prop3);
        } catch {
        console.log('qqqq');
        }
        ```

    * 참고사항

      * undefined 값에서, 함수 프로퍼티를 호출하려고 할 때에는, 에러 발생
        * 이외 객체에서, 정의되지 않은 프로퍼티를 호출할 때 undefined 반환
      * 객체를 직렬화할 때, undefined 프로퍼티는 무시된다.

  * 위 코드 외에도, 옵셔널 체이닝을 통해서 코드를 짤 수 있다.

    * 호출 대상이 undefined거나 null인 경우, 프로퍼티를 호출하면 오류가 발생

      * 또는, 호출 대상이 불분명한 경우, 특정 값을 호출할 때 오류가 발생할 수 있다.

      => 이러한 경우에 대해, 오류가 일어나지 않게끔 하고 undefined를 반환한다.

      ```javascript
      let undef = undefined;
      
      console.log(
        undef?.x,
        undef?.['x'],
        undef?.[1],
        {}.func?.()
      );
      //undefined undefined undefined undefined
      ```

      ```javascript
      // 옵셔널 체이닝을 사용한 방법
      const result = notSure();
      
      console.log(
        result?.prop1?.prop2?.prop3
      );
      ```

      ```javascript
      //유무가 불확실할 때에도 옵셔널 체이닝을 활용할 수 있다.
      const objs = [
        { func () { console.log(1) } },
        {},
        { func () { console.log(2) } },
        {},
        { func () { console.log(3) } },
      ]
      
      objs.forEach(o => o.func?.());
      //1
      //2
      //3
      // //undefined (forEach()의 return 된 결과물이 웹 브라우저에 찍힌 것임)
      
      // 추가) 콜백함수에 대해 실행하기만 하므로, 2번째와 4번째 인자에 대해서는 브라우저에 undefined 조차 찍히지 않는 것이 맞다.
      ```

      

## 12강 스코프와 바인딩

### 렉시컬과 클로저

자바 스크립트는 기본적으로 Dynamic Scope가 아니라, Lexical Scope를 따른다.

* 즉, 변수는 함수의 선언 위치에 따라 값이 할당된다고 말할 수 있다. (함수의 호출 위치가 아님!)

  * 참고) 이것이 compile 언어와의 차이가 아닐까 생각한다.,
  * 참고2) Dynamic Scope의 예로는 Perl 등이 있다고 하나.... 이 부분은 일단 넘어가자.
  * 출처 : https://velog.io/@tess/Lexical-Scope-vs-Dynamic-Scope

* 아래의 두 예시는, func2가 func1과 동일 레벨에 정의되어 있는 경우와, func2가 func1 내부에 정의된 경우에 대해 차이를 다룬다.

  * ```javascript
    const x = 1;
    const y = 1;
    const z = 1;
    
    function func1 () {
      const y = 2;
      const z = 2;
    
      console.log('2', x, y, z);
      func2();
    }
    
    function func2 () {
      const z = 3;
    
      console.log('3', x, y, z);
    }
    
    
    console.log('1', x, y, z)
    func1();
    
    
    // '1' 1 1 1
    // '2' 1 2 2
    // '3' 1 1 3
    
    ```

    => 즉, func2 내부의 x,y,z값은, 맨 바깥에 정의된 x,y,z값을 참조한다.

  * ```javascript
    const x = 1;
    const y = 1;
    const z = 1;
    
    function func1 () {
      const y = 2;
      const z = 2;
    
      function func2 () {
        const z = 3;
    
        console.log('3', x, y, z);
      }
    
      console.log('2', x, y, z);
      func2();
    }
    
    console.log('1', x, y, z)
    func1();
    
    // 1 1 1 1
    // 2 1 2 2
    // 3 1 2 3
    ```

    => 즉, func2는 func1 내부에 정의되어 있으므로, func1 내부에 정의된 x,y,z 변수를 우선적으로 참조한다.

* func2가 func1 내부에 정의된 예시를 다시 살펴보자

  ```javascript
  const x = 1;
  const y = 1;
  const z = 1;
  
  function func1 (a) {
    const y = 2;
    const z = 2;
  
    function func2 (b) {
      const z = 3;
  
      console.log('3', x, y, z, b);
    }
  
    console.log('2', x, y, z, a);
    func2(a + 1);
  }
  
  console.log('1', x, y, z)
  func1(1);
  ```

  * 렉시컬 환경에는, 아래의 3가지로 정리할 수 있다.

    * 전역 렉시컬 환경

      => 해당하는 스코프에는 x=1, y=1, z=1이 정의되어 있다.

    * func1 렉시컬 환경

      * 자체적인 스코프(환경 레코드)를 우선적으로 참조한다.

        => 해당하는 스코프에는 a=1, y=2, z=2가 정의되어 있다.

      * 이후, 해당하는 변수가 없으면, 외부 렉시컬 환경을 참조한다.

        => 여기서는, 외부 렉시컬 환경이 "전역 렉시컬 환경이다"

    * func2 렉시컬 환경

      * 자체적인 스코프(환경 레코드)를 우선적으로 참조한다.

      * 이후, 해당하는 변수가 없으면, 외부 렉시컬 환경을 참조한다.

        => 여기서는, 외부 렉시컬 환경이 "func1 렉시컬 환경이다"

        => 여기에도 참조하고자 하는 변수가 없다면, 더 외부의 렉시컬 환경(전역 렉시컬 환경)을 참조하게 된다.



* 클로저

  * 내부 함수에서, 외부 함수의 값에 접근할 수 있게끔 하는 개념

    * 내 생각) 컴파일 언어와 구별되는 특징이라고 생각한다. 

  * ```javascript
    function func1 () {
      const word = 'Hello';
    
      function func2 () {
        console.log(word);
      }
      
      return func2;
    }
    
    const logHello = func1();
    
    logHello();
    
    //Hello
    ```

    * 위의 코드에서, word는 func1 내부에 정의되어 있음에도 불구하고, func2 함수를 가리키는 logHello 에서도 word에 Hello가 할당되어 있음을 확인할 수 있다.
    * 이는, logHello 내부 (즉, func2 내부)의 클로저에 word 변수의 데이터가 저장되어 있다.
    * (당연한 말일수도 있겠지만) func1을 호출하기 전까지는, func2는 정의되어 있지 않다. (따라서, 제일 바깥 scope에서 func1을 호출하지 않고 func2를 콘솔에 찍으려고 하면 에러가 발생한다.)

  * 외부 함수를 호출해서, 외부 함수 내부에 정의된 함수를 여러 번 반환받아도, 해당 closure는 1개이다. 

    * 즉 해당 값이 저장되는 외부환경(closure)는 유지된다!

      * (이는 아래의 코드를 통해 유추해 볼 수 있다)

    * 내 생각) 아마 메모리 절약 문제 때문이지 않을까....

      ```javascript
      function createCounter (start) {
        let num = start;
      
        return function () {
          console.log(++start);
          return start;
        }
      }
      //start 변수가 closure에 저장된다.
      
      const count = createCounter(10);
      
      count(); // ⭐ 반복 실행해 볼 것
      count(); // ⭐ 반복 실행해 볼 것
      count(); // ⭐ 반복 실행해 볼 것
      
      //11
      //12
      //13
      
      ```

       => start 변수가 저장되어 있는 closure는 계속 유지가 되기 때문에, start 변수의 값이 계속 증가한다.

  * 함수 내에 정의되어 있는 변수를, 해당 함수 내부 함수가 사용할 때에는 closure에 저장되는 특성을 활용하면 아래의 과정이 가능하다.

    * private field 흉내내기

      * function내부에 지역변수로서 _name, _age를 설정하고, 매개변수를 통해 값을 할당한다

      * 해당 function은 _name 과 _age를 반환하는 메서드를 프로퍼티로 가지는 객체를 반환한다.

        => 외부에서 해당 function을 호출하면, _name과 _age를 반환하는 메서드를 가진 "객체"가 반환된다.

        => 해당 객체의 메서드를 호출하면, closure에 있는 데이터를 활용하게 된다.

        ```javascript
        function employeeCreator (name, age) {
          let _name = name;
          let _age = age;
        
          return {
            name: () => _name,
            age: () => _age,
            setAge: function (age) { _age = age; },
            getOlder: function (years) { _age += years; }
          }
        }
        
        const employee = employeeCreator('홍길동', 20);
        
        console.log(employee);
        console.log(employee.name(), employee.age());
        // {name: ƒ, age: ƒ, setAge: ƒ, getOlder: ƒ}
        // 홍길동 20
        
        
        employee.setAge(25);
        console.log(employee.name(), employee.age());
        // 홍길동 25
        
        
        employee.getOlder(3);
        console.log(employee.name(), employee.age());
        // 홍길동 28
        ```



### this의 동적 바인딩

* 전역에서의 this

  ```javascript
  console.log(this);
  ```

  * 브라우저의 콘솔창의 경우는, this는 globalThis
  * Node.js의 REPL의 경우는, this는 globalThis
  * .js 문서의 경우, this는 빈 객체

* 함수 안에서의 this

  * 엄격 모드와 느슨한 모드일 때 다르다.

    ```javascript
    function func () {
      console.log(this); // globalThis
    }
    
    func();
    //Window 객체
    ```

    ```javascript
    'use strict';
    
    function func () {
      console.log(this); // undefined
    }
    
    func();
    //undefined
    ```

    

* 객체 안에서의 this

  * 객체 리터럴 - 해당 객체를 가리킴

    * (내 생각) 화살표 함수를 쓸 수 없는 이유가, x가 어디를 가리키는지 잘 몰라서 그러지 않을까... (아래 코드 참조)

    ```javascript
    const obj = {
      x: 123,
      getX: function () {
        return this.x;
      }
    }
    
    console.log(obj.getX()); //123
    
    //참고. 아래의 코드도 가능
    
    const obj = {
      x: 123,
      getX: () => obj.x
    }
    
    console.log(obj.getX()); //123
    
    
    //참고2. 아래의 코드는 안 됨.
    
    const obj = {
      x: 123,
      getX: () => this.x
    }
    
    console.log(obj.getX());
    //undefined
    
    
    //참고3. 아래의 코드는 에러가 뜸
    const obj = {
      x: 123,
      getX: () => x
    }
    
    console.log(obj.getX());
    //Uncaught ReferenceError: x is not defined
    ```

  * 생성자 함수 - this는 생성될 인스턴스를 가리킨다.

    ```javascript
    function Person (name, age) {
      this.name = name;
      this.age = age;
      this.introduce = function  () {
        return `저는 ${this.name}, ${this.age}세입니다.`
      }
    }
    
    console.log(
      new Person('홍길동', 20).introduce()
    );
    // 저는 홍길동, 20세입니다.
    ```

  * 클래스 선언 - this는 생성될 인스턴스를 가리킨다

    ```javascript
    class YalcoChicken {
      constructor (name, no) {
        this.name = name;
        this.no = no;
      }
      introduce () {
        return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
      }
    }
    
    console.log(
      new YalcoChicken('강남', 17).introduce()
    );
    
    //안녕하세요, 17호 강남점입니다!
    ```

* this의 동적 바인딩

  * 아래의 경우, italian에게 한국 김치찌개 만드는 법을 알려주어야 하는데, this의 동적 바인딩 성질로 인해서, italian이 피자찌개를 만드는 우스꽝 스러운 결과를 초래할 수 있다.

  * ```javascript
    const korean = {
      favorite: '김치',
      makeStew: function (isHot, pots) {
        return `${isHot ? '매운' : '순한'} ${this.favorite}찌개 ${pots}냄비`;
      }
    };
    
    const italian = {
      favorite: '피자'
    };
    
    
    //1. 한국인이 김치찌개를 끓임
    console.log(
      korean.makeStew(true, 1)
    );
    //매운 김치찌개 1냄비
    
    
    //2-1. 이탈리안 객체에, 김치찌개 끓이는 비법 함수 삽입
    // 이탈리아인에게 한국인이 찌개 끓이는 법을 알려줌
    italian.makeStew = korean.makeStew;
    
    
    //2-2. italian이 makeStew 함수를 호출하면, this가 italian을 가리키므로 아래의 우스꽝스런 결과 초래
    console.log(
      italian.makeStew(false, 2)
    );
    // 순한 피자찌개 2냄비
    ```

  * 이제, this가 무엇을 가리키는지 명확하게 드러내는 코드를 작성할 것이다

    => call, apply, bind 함수 호출을 우선적으로 다루자

    * ```javascript
      const korean = {
        favorite: '김치',
        makeStew: function (isHot, pots) {
          return `${isHot ? '매운' : '순한'} ${this.favorite}찌개 ${pots}냄비`;
        }
      };
      
      const italian = {
        favorite: '피자'
      };
      
      // 이탈리아인에게 한국인이 찌개 끓이는 법을 알려줌
      italian.makeStew = korean.makeStew;
      
      
      //call, apply 함수 호출
      //this를 인자로 넘겨서, 함수 실행 시 this를 명확히 지시한다.
      
      console.log(
        italian.makeStew.call(korean, false, 2)
      );
      //순한 김치찌개 2냄비
      
      console.log(
        italian.makeStew.apply(korean, [false, 2])
      );
      //순한 김치찌개 2냄비
      
      
      //bind 함수 호출
      //bind 함수는, this의 주체를 명확히 한 "함수"를 반환한다.
      	// + 물론 this를 넘기면서 인자까지 넘기는 것도 가능하다.
      
      // ⭐ this가 바인딩된 새 함수를 만듦
      italian.makeRightStew = korean.makeStew.bind(korean);
      
      console.log(
        italian.makeRightStew(false, 2)
      );
      //순한 김치찌개 2냄비
      
      
      // 💡 추가 인자들까지 바인딩 가능 
      italian.makeClassicStew = korean.makeStew.bind(korean, true, 1);
      
      console.log(
        italian.makeClassicStew()
      );
      //매운 김치찌개 1냄비
      ```

    * 참고) call이나 apply 함수는 this를 인자로 넘기므로, 1회성의 실행이 필요할 때 해당 함수를 활용하는 것이 좋을 것으로 보인다. 

    * bind 함수는, "this가 명확한" 함수를 반환하므로, 아래의 예도 가능하다

      * 어떤 객체에다가, 바인딩된 함수를 프로퍼티로 추가

        => 다른 객체에서 바인딩된 함수를 호출하면, 무조건 위의 객체의 프로퍼티를 활용하게 된다.

      ```javascript
      const korean = {
        favorite: '김치',
        makeStew: function (isHot, pots) {
          return `${isHot ? '매운' : '순한'} ${this.favorite}찌개 ${pots}냄비`;
        },
        teachMakingStew: function () {
          return this.makeStew.bind(this);
        }//바인딩된 함수를 프로퍼티로 추가
      };
      
      const italian = {
        favorite: '피자'
      };
      
      italian.makeStew = korean.teachMakingStew();
      
      console.log(
        italian.makeStew(false, 2)
      );
      //순한 김치찌개 2냄비
      ```

    * 생성자 함수의 경우, 아래의 과정으로 바인딩할 것이다

      * 우선, 함수 프로퍼티 추가
      * 해당 함수 프로퍼티를 바인딩하고, 해당 함수의 이름(즉, 프로퍼티의 key값) 으로 덮어씌운다.

      ```javascript
      d
      function Korean () {
        this.favorite = '김치';
        this.makeStew = function (isHot, pots) {
          return `${isHot ? '매운' : '순한'} ${this.favorite}찌개 ${pots}냄비`;
        };
      
        // 💡 여기서 바인딩을 고정시켜버림
        this.makeStew = this.makeStew.bind(this);
      }
      
      function Italian () {
        this.favorite = '피자';
      }
      
      const korean = new Korean();
      const italian = new Italian();
      
      italian.makeStew = korean.makeStew; //이미 바인딩된 함수가 프로퍼티로 추가된다.
      
      
      
      console.log(
        italian.makeStew(false, 2)
      );
      // 순한 김치찌개 2냄비
      ```

* 배열 메서드의 thisArg

  * 콜백 함수 내의 this가 가리키는 대상이다

  * 배열 메서드 호출 시, 인자로 넘긴다. (즉, 인자로 this가 가리키는 대상을 명확하게 전달한다.)

  * 아래의 상황에서 활용이 가능하다.

    * 2명의 사람(peter, jane)이 각각의 성별, 사이즈에 해당하는 옷들을 모두 출력하고자 한다. (성별은 공용인 U도 가능하다.)

    * 주어진 상황은 아래와 같다.

      * 2명의 사람은 각각 name(이름), sex(성별), size(사이즈)이 프로퍼티로 주어져 있다.

      * 옷의 목록들이 배열로서 제시되어 있다

        * 옷은 객체로서 정의되어 있고, sex(성별)과 size(사이즈)를 프로퍼티로 가진다.

      * 아래와 같이 코드를 짜자.

        ```JAVASCRIPT
        //실행할 로직이 담긴 함수
        //아래에서, thisArg는 me이다. 즉, this는 me를 가리킨다고 할 수 있다.
        function recommendForYou(me) {
            const products = [
            { sex: 'F', size: 'M' },
            { sex: 'M', size: 'L' },
            { sex: 'F', size: 'M' },
            { sex: 'U', size: 'S' },
            { sex: 'M', size: 'L' },
            { sex: 'F', size: 'S' },
            ]; 
        
            products.map((itm, idx) => {return {...itm, idx}})
            .filter(function({sex,size}) {
                return ['U', this.sex].includes(sex) && this.size===size
            },me) //이 때 me가 thisArg이다.
            .forEach(function({idx}){
                console.log(`${this.name}님, ${++idx}번은 어떠신가요??`)
            },me)
        }
        
        
        
        //2명의 사람
        const peter = {
          name: '피터',
          sex: 'M',
          size: 'L'
        };
        
        const jane = {
          name: '제인',
          sex: 'F',
          size: 'S'
        };
        
        
        
        //실행
        recommendForYou(peter);
        recommendForYou(jane);
        
        //피터님, 2번은 어떠신가요??
        //피터님, 5번은 어떠신가요??
        //제인님, 4번은 어떠신가요??
        //제인님, 6번은 어떠신가요??
        ```



### this의 정적 바인딩

* 객체에서 함수를 프로퍼티로 설정할 때에는 아래와 같이 3가지 종류가 존재한다.

  ```javascript
  const obj = {
    // function 선언 함수
    func1: function () { return true; },
  
    // 메서드
    func2 () { return true; },
  
    // 화살표 함수
    func3: () => true
  }
  
  console.log(
    obj.func1(),
    obj.func2(),
    obj.func3()
  );
  ```

  * 아래의 과정을 통해, 생성자 역할을 수행하는 함수는 function으로 선언된 함수일 뿐이다.

    ```javascript
    const func1 = new obj.func1();
    const func2 = new obj.func2();
    const func3 = new obj.func3();
    ```

    => prototype이 func1에만 정의되어 있기 때문이다.

  * 이외에도 아래의 차이점이 있다. (흐름을 파악하는 것이 우선이므로, 지금은 대략적인 내용만 정리하고 추후 정리하기)

    |                    | 생성자 역할 | 프로토타입 | arguments | super |
    | ------------------ | ----------- | ---------- | --------- | ----- |
    | function 선언 함수 | O           | O          | O         | X     |
    | 메서드             | X           | X          | O         | O     |
    | 화살표 함수        | X           | X          | X         | X     |

    * 출처 : https://velog.io/@hangem422/js-es6-function

* 화살표 함수와 this

  * function 선언 함수와, 메서드와 가장 "두드러지는" 특징은 this의 바인딩 차이이다

    * 화살표 함수 내부의 this는 정적 바인딩이다. (즉, 호출된 위치와 상관없이 무조건 화살표 함수 선언 위치의 가장 근접한 상위 스코프에 바인딩 된다.)

    * 아래의 코드를 통해 알아보자

      ```javascript
      const obj = {
        x: 1,
        y: 2,
      
        func1: function () {
          console.log('1.', this);
        },
        func2 () {
          console.log('2.', this);
        },
        func3: () => {
          console.log('3.', this);
        }
      }
      
      // this가 해당 객체를 가리킴
      obj.func1();
      obj.func2();
      
      // 💡 this가 상위 스코프를 가리킴 => 여기서는 Window 객체가 될 것이다.
      obj.func3(); 
      ```

      ```javascript
      const outer = {
        a: true,
        b: false,
      
        func: function () {
          const inner = {
            x: 1,
            y: 2,
      
            func1: function () {
              console.log('1.', this);
            },
            func2 () {
              console.log('2.', this);
            },
            func3: () => {
              console.log('3.', this);
            }
          }
      
          // this가 inner를 가리킴 
          inner.func1();
          inner.func2();
      
          // this가 outer를 가리킴
          inner.func3();
        }
      }
      
      outer.func();
      ```

    * 생성자 함수 내에서, function 선언 함수와 화살표 함수를 선언해서 차이를 알아보자.

      ```javascript
      function Korean () {
        this.favorite = '김치';
      
        this.makeStew = function (isHot) {
          return `${isHot ? '매운' : '순한'} ${this.favorite}찌개`;
        };
        this.fryRice = (isHot) => {
          return `${isHot ? '매운' : '순한'} ${this.favorite}볶음밥`;
        };
      }
      
      function Italian () {
        this.favorite = '피자';
      }
      
      const korean = new Korean();
      const italian = new Italian();
      
      console.log(korean.makeStew(true)); //매운 김치찌개
      console.log(korean.fryRice(true)); //매운 김치볶음밥
      
      italian.makeStew = korean.makeStew;
      italian.fryRice = korean.fryRice;
      
      //this의 동적 바인딩과 정적 바인딩 차이를 알 수 있다.
      console.log(italian.makeStew(false)); //순한 피자찌개
      console.log(italian.fryRice(false)); //순한 김치볶음밥
      ```

    * 클래스의 경우에도 마찬가지이다.

      ```javascript
      // ♻️ 새로고침 후 실행
      class Korean {
        constructor () {
          this.favorite = '김치';
          this.fryRice = (isHot) => {
            return `${isHot ? '매운' : '순한'} ${this.favorite}볶음밥`;
          }
        }
        makeStew (isHot) {
          return `${isHot ? '매운' : '순한'} ${this.favorite}찌개`;
        }
      }
      
      class Italian {
        constructor () {
          this.favorite = '피자';
        }
      }
      
      const korean = new Korean();
      const italian = new Italian();
      
      console.log(korean.makeStew(true)); //매운 김치찌개
      console.log(korean.fryRice(true)); //매운 김치볶음밥
      
      
      
      italian.makeStew = korean.makeStew;
      italian.fryRice = korean.fryRice;
      
      //this의 동적 바인딩과 정적 바인딩의 차이가 잘 드러난다.
      console.log(italian.makeStew(false)); //순한 피자찌개
      console.log(italian.fryRice(false)); //순한 김치볶음밥
      ```

  * 화살표 함수는 this에 대해 정적 바인딩을 하므로, call이나 apply나 bind 함수의 this 인자는 무시된다. 

    ```javascript
    // ♻️ 새로고침 후 실행
    class Korean {
      constructor () {
        this.favorite = '김치';
        this.fryRice = (isHot) => {
          return `${isHot ? '매운' : '순한'} ${this.favorite}볶음밥`;
        }
      }
      makeStew (isHot) {
        return `${isHot ? '매운' : '순한'} ${this.favorite}찌개`;
      }
    }
    
    const korean = new Korean();
    
    console.log(
      korean.fryRice.call({favorite: '된장'}, true)
    );
    console.log(
      korean.fryRice.apply({favorite: '된장'}, [true])
    );
    console.log(
      korean.fryRice.bind({favorite: '된장'}, true)()
    );
    //매운 김치볶음밥
    //매운 김치볶음밥
    //매운 김치볶음밥
    ```

* node.js 파일을 실행 시, this 관련한 정보가 다소 다르게 나타난다.

  * node.js는 각 파일을 모듈로 만들어서 실행한다

  * 파일 내 모든 코드는, 모듈의 메서드 안으로 들어가서 실행된다.

    ```javascript
    // this가 모듈 객체(현재 비어있음)를 가리킴
    console.log('0.', this);
    
    function func1 () {
      // this가 전역 객체를 가리킴
      console.log('1.', this);
    }
    
    function func2 () {
      'use strict';
      
      // this가 undefined를 가리킴
      console.log('2.', this);
    }
    
    const func3 = () => {
      // 💡 this가 모듈 객체(이 함수의 상위 스코프)를 가리킴
      console.log('3.', this);
    }
    
    
    //0. {}
    func1(); // 1. <ref *1> Object [global]
    func2(); // 2. undefined
    func3(); // 3. {}
    ```

  * vscode로 node.js 실행 시 참고한 사이트

    * https://bitkunst.tistory.com/entry/Nodejs-%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0-with-Visual-Studio-Code



## 프로토타입

### 프로토타입의 개념

* 자바스크립트에서, 모든 객체는 prototype을 가진다

  * 여기서, 최상위 prototype은 Object.prototype임을 유추할 수 있다.

    * 때문에, 아래의 빈 객체에서 함수를 호출할 수 있는 이유도 여기에 있다.

      ```javascript
      console.log(
        obj.toString()
      );
      
      console.log(
        obj.valueOf()
      );
      ```

* prototype을 활용하여, prototype chain을 활용할 수 있다.

  * 즉, 특정 객체에 호출된 프로퍼티가 없다면, 해당 객체의 프로토타입에서 찾는다

  * 예를 들면, Array 생성자 함수로 만들어진 객체에는, valueOf() 함수가 정의되어 있지 않지만, [[prototype]]에는 (즉, Object의 prototype) valueOf() 함수가 정의되어 있으므로, array.valueOf() 가 가능하다

    * Array.prototype에서 valueOf()를 재정의하여 사용할 수 있다

      => 이처럼 prototype chain을 이용하여 함수를 재정의할 수 있다.





* 코드로 프로토타입에 접근하기

  * `__proto__ ` 접근자 사용해서 접근할 수 있으나, 권장되지 않는다.

    * 아래의 방식으로 접근할 것이다. (Object.getPrototypeOf({}))

      ```javascript
      console.log(
        Object.getPrototypeOf({})
      );
      ```

    * 생성자 함수에서는 prototype에 접근 가능하며, 접근이 안 되는 함수는 생성자 함수로 동작하지 않는다고 얘기할 수 있다.

      ```javascript
      function Person (name) {
        this.name = name;
      }
      
      // 인스턴스들에 공유될 프로토타입에 다음과 같이 접근
      console.log(Person.prototype);
      
      //생성자 함수로 동작하는 Set 함수
      console.log(
        Set.prototype
      );
      
      // 생성자 함수로 동작하지 않는 빌트인 객체
      console.log(
        Math.prototype
      ); //undefined
      ```

      

* prototype 사용 예시

  * class 내에 함수를 정의하면, 기본적으로 prototype의 프로퍼티로 정의가 된다.  => 그렇게 하지 않고, Dog의 prototype에 직접 접근하여 정의해도 된다. 

    ```javascript
    class Dog {
      constructor (name) {
        this.name = name;
      }
    }
    
    Dog.prototype.sound = '멍멍';
    Dog.prototype.bark = function () { // 메서드로 만드는 것과 같음
      console.log(this.sound)
    };
    
    const badugi = new Dog('바둑이');
    
    badugi.bark(); //prototype에 정의된 bark() 가 호출된다. 
    ```

  * 결국, 여러 개 객체를 생성 시, 모든 객체는 공통된 기능을 수행하므로, 해당 기능을 구현하는 코드(= 함수)는, 각 객체가 공유하게끔 하면 메모리가 절약된다.

    => 즉, 객체의 생성자 함수의 prototype에 함수를 정의하는 것이 효율적이다!

    * 특정 객체는 다른 기능을 수행하게끔 하고 싶다면, 해당 객체의 "인스턴스 레벨"에서 함수를 재정의하면 될 것이다.

      => 이는 prototype chain의 특성을 활용한 것이다. 

    ```javascript
    function YalcoChicken (name, no) {
      this.name = name;
      this.no = no;
    }
    
    // 공통된 요소들은 프로토타입 프로퍼티로
    YalcoChicken.prototype.titleEng = 'YalcoChicken';
    
    YalcoChicken.prototype.introduce = function () {
      return `안녕하세요, ${this.no}호 ${this.name}점입니다!`;
    }
    
    YalcoChicken.prototype.introEng = function () {
      return `Welcome to ${this.titleEng} at ${this.name}!`;
    };
    
    const chain1 = new YalcoChicken('판교', 3);
    const chain2 = new YalcoChicken('강남', 17);
    const chain3 = new YalcoChicken('제주', 24);
    
    console.log(chain1.introduce());
    console.log(chain1.introEng());
    
    //chain4는 introduce()를 재정의 (즉, 인스턴스 레벨에서 덮어씌움.)
    const chain4 = new YalcoChicken('평양', 456);
    chain4.introduce = function () {
      return `어서오시라요, ${this.no}호 ${this.name}점입네다!`;
    }
    
    console.log(chain4.introduce());
    ```

    

### 프로토타입과 상속

* 프로토타입으로 상속하기

  * `Object.create(Function.prototype)` 을 활용하여 프로토타입을 상속한다

    * 아래의 코드를 통해 성질을 알아보자.

      ```javascript
      function Parent() {};
      function Child() {};
      
      console.log(Parent.prototype);
      console.log(Child.prototype);
      
      //{constructor: ƒ}
      //	constructor: ƒ Parent()
      //	[[Prototype]]: Object
      
      //{constructor: ƒ}
      //	constructor: ƒ Child()
      //	[[Prototype]]: Object
      
      console.log("===============");
      
      
      let v = Object.create(Parent.prototype); //빈 객체를 생성하며, v의 prototype에 접근하게 되면 이것이 Parent.prototype과 완전히 유사하다.
      
      console.log(v);
      console.log(Object.getPrototypeOf(v) === Parent.prototype);
      
      
      //Parent {}
      //	[[Prototype]]: Object
      //		constructor: ƒ Parent()
      //		[[Prototype]]: Object
      
      //true
      
      console.log("===================");
      
      console.log("아래의 과정을 통해, prototype으로 상속이 이루어짐을 알 수 있다");
      Child.prototype = v; //Child.prototype = Object.create(Parent.prototype); 과 동일
      ```

    * 즉, Child와 Parent 생성자 함수의 prototype은 서로 다른 객체이다

      => Object.getPrototypeOf(Child.prototype) 을 적용해야, 비로소 Parent.prototype과 동일하다

  * 아래의 예시를 통해 확인할 수 있다.

    ```javascript
    function Bird (name, sound) {
      this.name = name;
      this.sound = sound;
    }
    Bird.prototype.fly = function () {
      console.log(`${this.name} ${this.sound} 비행중`);
    }
    
    function Eagle (name, sound, prey) {
      this.name = name;
      this.sound = sound;
      this.prey = prey;
    }
    
    // ⚠️ 순서 주의! 상속을 먼저 받음
    Eagle.prototype = Object.create(Bird.prototype);
    // Eagle.prototype = Bird.prototype; // 💡 비교해 볼 것 => 이 경우는 Eagle의 prototype과 Bird의 prototype이 완전히 동일시되어, Eagle prototype만의 프로퍼티를 재정의할 수 없게 된다.
    
    // 상속 이후 자신의 프로토타입 작성
    Eagle.prototype.hunt = function () {
      console.log(`${this.name} ${this.prey} 사냥중`);
    }
    
    
    
    const bird = new Bird('새돌이', '파닥파닥');
    const eagle = new Eagle('독돌이', '푸드덕', '토끼');
    
    // 상속 구조 확인
    console.log(bird);
    console.log(eagle);
    
    console.log(
      eagle instanceof Bird,
      bird instanceof Eagle
    );
    //true false
    
    bird.fly();
    eagle.fly();
    eagle.hunt();
    //새돌이 파닥파닥 비행중
    //독돌이 푸드덕 비행중
    //독돌이 토끼 사냥중
    ```

    

* 부모의 생성자를 활용해서, 상속할 수 있다

  * 부모의 생성자의 코드 중, 자식의 생성자의 코드와 중복된다면, 상속을 활용하여 코드를 줄일 수 있다

  * 이 때, 자식 함수에서 부모의 생성자 함수를 호출하므로, this의 주체를 명확히 하기 위해 call 함수를 활용한다.

    ```javascript
    function Bird (name, sound) {
      this.name = name;
      this.sound = sound;
    }
    Bird.prototype.fly = function () {
      console.log(`${this.name} ${this.sound} 비행중`);
    }
    
    function Eagle (name, sound, prey) {
      // 💡 call 호출방식 사용
      Bird.call(this, name, sound);
      this.prey = prey
    }
    
    Eagle.prototype = Object.create(Bird.prototype);
    
    Eagle.prototype.hunt = function () {
      console.log(`${this.name} ${this.prey} 사냥중`);
    }
    
    const eagle = new Eagle('독돌이', '푸드덕', '토끼');
    console.log(eagle);
    
    eagle.fly();
    eagle.hunt();
    //독돌이 푸드덕 비행중
    //독돌이 토끼 사냥중
    ```

* 클래스로도 상속을 구현할 수 있다

  * 본질적으로, 프로토타입 기반으로 구현되어 있다.

    * 때문에, 클래스 내에서 메서드로서 함수가 정의되어 있다면, 이는 자동으로 클래스의 prototype에 속하게 된다.

      (메서드 이외 다른 형태로 정의되어 있다면, "인스턴스 레벨에서" 함수의 프로퍼티가 정의된다.)

  * super키워드와  extends를 활용한다.

  * 아래의 예시는, 인스턴스 레벨에 속하는지, 프로토타입에 속하는지를 보여준다.

    ```javascript
    function AAA () {
      this.field = 1;
      this.run = function () { return 1; };
    }
    
    class BBB {
      field = 1;
      run = function () { return 1; }
    }
    
    class CCC {
      field = 1;
      run () { return 1; }
    }
    
    console.log(new AAA()); // 인스턴스에 속함
    console.log(new BBB()); // 인스턴스에 속함
    console.log(new CCC()); // 프로토타입에 속함
    
    
    //AAA {field: 1, run: ƒ}
    //BBB {field: 1, run: ƒ}
    //CCC {field: 1}
    ```

  * extends와 super를 활용해서 상속하는 코드는 아래와 같다

    * 이 때, extends 를 사용하게 되면, `Eagle.prototype = Object.create(Bird.prototype)` 의 효과가 발생하게 된다.

      ```javascript
      // ♻️ 새로고침 후 실행
      
      class Bird {
        constructor (name, sound) {
          this.name = name;
          this.sound = sound;
        }
        fly () {
          console.log(`${this.name} ${this.sound} 비행중`);
        }
      }
      
      class Eagle extends Bird {
        constructor (name, sound, prey) {
          super(name, sound);
          this.prey = prey;
        }
        hunt () {
          console.log(`${this.name} ${this.prey} 사냥중`);
        }
      }
      
      const bird = new Bird('새돌이', '파닥파닥');
      const eagle = new Eagle('독돌이', '푸드덕', '토끼');
      
      console.log(bird);
      console.log(eagle);
      //Bird {name: '새돌이', sound: '파닥파닥'}
      
      //Eagle {name: '독돌이', sound: '푸드덕', prey: '토끼'}
      //	name: "독돌이"
      //	prey: "토끼"
      //	sound: "푸드덕"
      //	[[Prototype]]: Bird
      //		constructor: class Eagle
      //		hunt: ƒ hunt()
      //		[[Prototype]]: Object
      //			constructor: class Bird
      //			fly: ƒ fly()
      //			[[Prototype]]: Object
      
      
      bird.fly();
      eagle.fly(); //프로토타입 체인을 활용하여, 최종적으로 Bird.prototype 내의 fly() 함수를 호출하게 된다.
      eagle.hunt();
      
      //새들이 파닥파닥 비행중
      //독돌이 푸드덕 비행중
      //독돌이 토끼 사냥중
      ```

      

* Object.assign()을 활용하여 아래 종류의 상속이 가능하다.

  * 일반적으로, 위에서 배운 상속은 1개의 부모로부터 상속받음

  * 그러나, Object.assign(Function.prototype, 객체1, 객체2...) 를 통해서 인자를 받은 객체의 프로퍼티(데이터 프로퍼티, 함수 프로퍼티 모두 가능)를 모두 Function.prototype의 프로퍼티로 정의하게 된다.

    ```javascript
    const runner = {
      run : function () {
        console.log(`${this.name} 질주중`);
      }
    }
    const swimmer = {
      swim: function () {
        console.log(`${this.name} 수영중`);
      }
    }
    const flyer = {
      fly: function () {
        console.log(`${this.name} 비행중`);
      }
    }
    const hunter = {
      hunt: function () {
        console.log(`${this.name} 사냥중`);
      }
    }
    
    
    
    class Owl {
      constructor (name) {
        this.name = name;
      }
    }
    
    class FlyingFish {
      constructor (name) {
        this.name = name;
      }
    }
    
    class PolarBear {
      constructor (name) {
        this.name = name;
      }
    }
    
    //Function.prototype에 프로퍼티 설정
    Object.assign(Owl.prototype, flyer, hunter);
    Object.assign(FlyingFish.prototype, flyer, swimmer);
    Object.assign(PolarBear.prototype, runner, swimmer, hunter);
    
    //각 객체의 프로토타입 체인 확인
    const owl = new Owl('붱돌이');
    const f_fish = new FlyingFish('날치기');
    const p_bear = new PolarBear('극곰이');
    
    console.log(owl);
    console.log(f_fish);
    console.log(p_bear);
    
    //Owl {name: '붱돌이'}
    //	name: "붱돌이"
    //	[[Prototype]]: Object
    //		fly: ƒ ()
    //		hunt: ƒ ()
    //		constructor: class Owl
    //		[[Prototype]]: Object
    
    //FlyingFish {name: '날치기'}
    //	name: "날치기"
    //	[[Prototype]]: Object
    //		fly: ƒ ()
    //		swim: ƒ ()
    //		constructor: class FlyingFish
    //		[[Prototype]]: Object
    
    //...
    
    ```

    

    

### 비동기의 개념과 타임아웃

비동기 프로그래밍은 아래와 같이 진행된다.

* 자바스크립트 코드는 단일 스레드로 실행 (즉, 동기적으로 실행된다)

  * 이 때, 자바스크립트 실행 환경은 멀티 스레드로 실행된다.

    => 그래서, 비동기 작업은 실행환경으로 넘겨지고, 계속 자바스크립트 코드는 실행된다.,

  * 실행이 끝난 비동기 작업은, 태스크 큐로 보내진다.

    => js코드가 모두 실행이 끝난 후에야, 태스크 큐에 있던 비동기 작업이 다시, 자바스크립트 코드로서 실행되게 된다.

    => 이 과정은 "이벤트 루프"에 의해서 행해진다.



### 프로미스

//setTimeOut()의 반환값으로 TIMEOUTid 값이 반환된다는데... 솔직히 잘 모르겠다.



//콜백함수로 작성한 이유는, 이전 콜백함수의 결과값을 활용해야 할 때 활용한다.

//확인해보니, nextFunc는 비동기함수가 아니므로, 실행될 때, nextFunc의 호출이 다 끝나고 나서야 다음 코드가 실행됨

```javascript
const DEADLINE = 1400;

function relayRun (name, start, nextFunc, failMsg) {
  console.log(`👟 ${name} 출발`);
  const time = 1000 + Math.random() * 500;
  for(let j=0; j<20; j++) {console.log("prvprvprvprvprv");}

  setTimeout(() => {
    if (time < DEADLINE) {
      console.log(`🚩 ${name} 도착 - ${(start + time)/1000}초`);
      nextFunc?.(start + time);
      for(let i=0; i<8; i++){console.log("testtesttesttest");}  //여기는, nextFunc()의 호출이 끝나고 나서야 비로소 실행된다.    
    } else {
      console.log(failMsg);
      console.log(`😢 완주 실패 - ${(start + time)/1000}초`);
    }

    if (time >= DEADLINE || !nextFunc) {
      console.log('- - 경기 종료 - -');
    }
  }, time);
}


```



//Promise 관련

resolve는 콜백함수를 받음

//promise 객체가 생성될 때, 내부의 코드를 모두 실행한 후 객체가 생성되는 듯 하다.

//resolve는 2번이상 넣어도 무시되는 듯 하다.

//resolve 콜백함수는 항상 비동기 식으로 맨 나중에 실행된다는 사실을 관찰(setTimeOut 제거해도 마찬가지)

//우선, Promise 객체 내에 정의되어 있는 콜백함수를 우선적으로 실행한다. (동기적)



//then 의 결과로 나오는 프로미스는, 자기 자신이 아닌 또다른 프로미스 객체

//PromiseResult에서 값을 저장

//promise.then() 시행이 비동기시행인 듯 하다. (그래야 논리적으로도 맞다고 생각한다. => resolve에 대한 콜백함수를 받아야만 시행이 되기 때문)

=> 실제로, then()을 실행하기 전에 이미, resolve() 를 제외한 모든 프로미스 내부 코드가 실행이 되며, then()을 실행할 떄, 넘겨받은 콜백함수를 근거로 resolve()를 마저 시행한다.

```javascript
const borrow = 20;

const payWith10perc = new Promise((resolve, reject) => {
  //비동기코드
  resolve(borrow * 1.1);
});

console.log(22222);

// ⚠️ 콘솔에서 분리해서 실행하면 안 됨!
// 프로미스가 생성되는 순간부터 시간 경과
payWith10perc
.then(result => {
  console.log(result + '만원');
});
for(let i=0; i<5000; i++) {console.log(1000000);}

//22222
//(5000)1000000
//22만원
```



//promise.then()하고나서, reject 함수가 시행되었는데 catch나 reject 콜백함수 전달 안 되어 있으면 에러 뜬다

=> 이는, promise.then()을 시행 도중, 에러가 뜰 때 "즉각적으로" 새로운 promise 객체가 반환되면서 catch() 함수가 실행된다고 한다. 

(출처 : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)

//아래를 보면 알 수 있듯이, promise 객체 생성 시, 코드 내부에 에러가 뜬다고 해서 즉시 에러가 뜨는 것이 아니라, 일단 javascript의 메인 코드를 다 실행하고 난 후, catch() 메서드가 보이지 않는다면 그 때서야 에러가 뜸을 확인할 수 있다. 

예시 코드)

```

```



//아래 2개의 코드는 상당한 차이가 있다. 

* 우선 함수 정의 코드는 2개 모두 공통

```javascript
const DEADLINE = 1400;

function getRelayPromise (name, start, failMsg) {
  console.log(`👟 ${name} 출발`);

  // 💡 랜덤 시간만큼 달리고 결과를 반환하겠다는 약속을 만들어 반환
  return new Promise((resolve, reject) => {
    const time = 1000 + Math.random() * 500;

    setTimeout(() => {
      if (time < DEADLINE) {
        console.log(`🚩 ${name} 도착 - ${(start + time)/1000}초`);
        resolve(start + time);
      } else {
        
        console.log(failMsg);
        reject((start + time) / 1000);
      }
    }, time);
  })
}
```

* 아래 3가지 경우로 실행하면, 전혀 다른 결과를 가져오게 된다.

  * 아래의 경우는, then 함수의 콜백 함수 인자가 promise 객체를 반환받는다.

    => 이 때, then 함수가 반환하는 promise 객체는, 위의 콜백 함수 인자가 반환하는 promise 객체와 상태가 같아진다고 한다. (내 생각)

    => 그리고, then()을 시행하기 이전에는, resolve()를 제외한 모든 promise 내부 코드가 시행된다. (비동기 코드까지도)

    => 그리고, then()을 시행한다면, 넘겨받은 콜백함수를 근거로 resolve()만 시행이 된다는 것을 확인한다. (이 과정까지 해서, promise.then() 의 promise 객체 내부의 모든 코드가 비로소 시행이 완료가 된다고 말할 수 있다.)

  ```javascript
  getRelayPromise('철수', 0, '철수부터 광탈입니다. ㅠㅠ')
  .then(result => {
    return getRelayPromise('영희', result, '영희가 완주하지 못했네요.');
  })
  .then(result => {
    return getRelayPromise('돌준', result, '돌준이 분발해라.');
  })
  .then(result => {
    return getRelayPromise('정아', result, '정아에게 무리였나보네요.');
  })
  .then(result => {
    return getRelayPromise('길돈', result, '아아, 아깝습니다...');
  })
  .catch(msg => {
    console.log(`😢 완주 실패 - ${msg}초`);
  })
  .finally(() => {
    console.log('- - 경기 종료 - -');
  });
  ```

  * 아래의 코드는, 위 코드와 동일한 원리로 동작한다
    * then 함수 인자의 콜백함수에서, 함수의 실행 부분 몸체 `{}`를 작성하지 않고, return 역시 명시하지 않는다면, 자동으로 promise chain에서 다음 then 블록으로 값을 전달한다.

  ```javascript
  getRelayPromise('철수', 0, '철수부터 광탈입니다. ㅠㅠ')
  .then(result =>getRelayPromise('영희', result, '영희가 완주하지 못했네요.'))
  .then(result => getRelayPromise('돌준', result, '돌준이 분발해라.'))
  .then(result => getRelayPromise('정아', result, '정아에게 무리였나보네요.'))
  .then(result => getRelayPromise('길돈', result, '아아, 아깝습니다...'))
  .catch(msg => {
    console.log(`😢 완주 실패 - ${msg}초`);
  })
  .finally(() => {
    console.log('- - 경기 종료 - -');
  });
  ```

  * 아래의 코드는, 위 2개의 코드랑 완전히 다르게 작동한다.
    * then 함수 인자의 콜백함수는 최종적으로 undefined를 반환한다.
    * 때문에, 우리가 원하는대로 promise chain이 동작하지 않는다.

  ```javascript
  getRelayPromise('철수', 0, '철수부터 광탈입니다. ㅠㅠ')
  .then(result => {getRelayPromise('영희', result, '영희가 완주하지 못했네요.')}) //(*)
  .then(result => {getRelayPromise('돌준', result, '돌준이 분발해라.')})
  .then(result => {getRelayPromise('정아', result, '정아에게 무리였나보네요.')})
  .then(result => {getRelayPromise('길돈', result, '아아, 아깝습니다...')})
  .catch(msg => {
    console.log(`😢 완주 실패 - ${msg}초`);
  })
  .finally(() => {
    console.log('- - 경기 종료 - -');
  });
  ```

  => (*) 부분에서, then 이 반환하는 promise 객체가 값을 전달받지 못하면서, promise chain 동작의 오류가 발생한다. (내 생각) promise 객체 자체가, 어떠한 값을 제대로 전달받지 못하면, promise chain 동작이 순차적으로 발생하지 않도록 설계된듯 하다.

  * 참고
    * https://triplexblog.kr/138
    * https://velog.io/@eunjin/Javascript-Promise-Chaining-%ED%94%84%EB%A1%9C%EB%AF%B8%EC%8A%A4-%EC%B2%B4%EC%9D%B8-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0



### 프로미스의 병렬 진행

아래의 경우, 일단 javascript의 코드가 다 실행되고 난 후에, ~~promise 내부 코드가 비동기적으로 실행된다.~~

=> javascript 코드가 실행되는 과정에서, promise 내부코드도 (동기적으로) 함께 시행된다.

=> 다만, promise 내부 코드에 비동기 코드가 존재하는 경우에는, javascript의 코드가 다 실행되고 난 이후에 promise 내부 코드가 실행된다.

```javascript
// 다섯 주자들이 동시에 질주
// 데드라인(밀리초) 안에 들어오지 못하면 탈락
let DEADLINE = 1450;

function getRunPromise (name) {
  return new Promise((resolve, reject) => {
    const time = 1000 + Math.random() * 500;

    setTimeout(() => {
      if (time < DEADLINE) {
        console.log(`🚩 ${name} 도착 - ${(time)/1000}초`);
        resolve({name, time});

      } else {
        reject((`${name} 시간초과`));
      }
    }, time);
  });
}

console.log("prv");
console.log(
  '철수,영희,돌준,정아,길돈'
  .split(',')
  .map(getRunPromise)
);
console.log("aft");

//prv
//[Promise 객체, Promise 객체, Promise 객체, Promise 객체, Promise 객체]
//aft

//	*(이제 Promise 객체 내부의 비동기 코드 실행) => 무작위로 실행된다.

//🚩 철수 도착 - 1.0340770288730459초
//🚩 정아 도착 - 1.090304709290944초
//🚩 돌준 도착 - 1.1644156953212312초
//🚩 길돈 도착 - 1.2597545978902094초
//🚩 영희 도착 - 1.1644156953212312초
```

Promise의 경우는 아래의 정적 메서드가 존재한다.

* 주어진 상황은 아래와 같다

  ```javascript
  let DEADLINE = 1450;
  
  function getRunPromise (name) {
    return new Promise((resolve, reject) => {
      const time = 1000 + Math.random() * 500;
  
      setTimeout(() => {
        if (time < DEADLINE) {
          console.log(`🚩 ${name} 도착 - ${(time)/1000}초`);
          resolve({name, time});
  
        } else {
          reject((`${name} 시간초과`));
        }
      }, time);
    });
  }
  ```

  * all

    * 프로미스의 배열을 받아서, 최종적으로 프로미스의 resolve된 값을 인자로 받아서 배열로 만들어 반환

      * 이는 모두 성공한 경우에 한함. 

        => 하나라도 프로미스 내부 코드 실행 과정에서 reject되는 과정이 있다면, catch 과정으로 넘어감

      * 아래 코드의 경우에는, Promise.all()은 프로미스 객체를 받고, 내부적으로는 배열을 최종적으로 받는다

        * 해당 배열의 요소는 {name, time} 의 객체이다.

    ```javascript
    // 한 명이라도 탈락하면 전체 탈락
    Promise.all(
      '철수,영희,돌준,정아,길돈'
      .split(',')
      .map(getRunPromise)
    )
    .then(console.log)
    .catch(console.error)
    .finally(() => {
      console.log('- - 경기 종료 - -');
    });
    
    //Promise.all() 은, 프로미스 객체를 반환하며, 이 객체의 promise 객체 내부에는 아래의 배열이 존재하게 된다.
    // [resolve된 객체, resolve된 객체, resolve된 객체, resolve된 객체, resolve 된 객체]를 반환하게 된다.
    
    //then() 메서드에서, 프로미스 객체의 PromiseResult 슬롯의 값을 활용한다.
    ```

    * 응용
      * 5명 모두 DEADLINE 통과 시, 상위 3명만 표시

    ```javascript
    // 성공시 탑3 표시
    Promise.all(
      '철수,영희,돌준,정아,길돈'
      .split(',')
      .map(getRunPromise)
    )
    .then(arr => {
      return arr.sort((a, b) => {
        return a.time - b.time
      })
      .map(({name}) => name)
      .splice(0, 3) //3개까지 잘라서 표현하며, 배열이 호출하는 함수로서 결과도 배열로 반환된다.
      .join(', ');
    }) //상위 3명의 이름이 문자열로 찍힌 값이, promise 객체의 PromiseResult 슬롯에 담긴다.
    .then(top3 => {
      console.log(`탑3: ${top3}`);
    }) //여기서부터는, promise 객체의 내부 값이 필요없으므로, return을 명시하지 않은 것으로 파악된다. 
    .catch(console.error)
    .finally(() => {
      console.log('- - 경기 종료 - -');
    });
    
    
    ```

  * allSettled

    * resolve가 실행되든, reject가 되든 then()을 실행한다.
      * resolve가 실행되면, status 프로퍼티와 value 프로퍼티를 가진다
        * value 프로퍼티에는,  resolve에서 넘겨받은 이유가 담긴다

      * reject가 실행되면, status 프로퍼티와 reason 프로퍼티를 가진다.
        * reason 프로퍼티에는, reject 메세지 인자가 넘어온다.


    ```javascript
  Promise.allSettled(
    '철수,영희,돌준,정아,길돈'
    .split(',')
    .map(getRunPromise)
  )
  .then(console.log)
  // ⚠️ catch는 동작하지 않음
  .finally(() => {
    console.log('- - 경기 종료 - -');
  });


  //결과물
  //[{…}, {…}, {…}, {…}, {…}]
  //0: {status: 'fulfilled', value: {…}} 
  	//value: {name: '철수', time: 1188.5151482323533}
  //1: {status: 'fulfilled', value: {…}}
  //2: {status: 'rejected', reason: '돌준 시간초과'}    //reject된 결과물
  //3: {status: 'fulfilled', value: {…}}
  //4: {status: 'fulfilled', value: {…}}
    ```

    ```javascript
  //따라서, 아래처럼, 성공한 사람의 경우와 실패한 사람의 경우를 나눠서 데이터를 다룰 수 있다.

  Promise.allSettled(
    '철수,영희,돌준,정아,길돈'
    .split(',')
    .map(getRunPromise)
  )
  .then(arr => {
    return {
      succ: arr.filter(result => {
        return result.status === 'fulfilled'
      }),
      fail: arr.filter(result => {
        return result.status === 'rejected'
      })
    }
  })
  .then(res => {
    res.succ.sort((a, b) => {
      return a.value.time - b.value.time;
    });
    console.log(
      `완주: ${res.succ.length}명 (1등: ${res.succ[0].value.name})`
    );
    console.log(
      `탈락: ${res.fail.length}명`
    );
  })

  .finally(() => {
    console.log('- - 경기 종료 - -');
  });
    ```

  * any

    * 가장 먼저 성공한 프로미스의 결과를 then 으로 반환
      * 이 때, 실험 결과, 개발자가 입력한 프로미스의 순서가 아니라, 서버가 (멀티 스레드로) 무작위로 처리한 프로미스 중, 가장 첫번째로 성공한 프로미스의 결과를 출력함을 알 수 있다.
      * (내 개인적인 생각) 어디에다가 사용할 수 있을까?

    ```javascript
    DEADLINE = 1050;
    
    Promise.any(
      '철수,영희,돌준,정아,길돈'
      .split(',')
      .map(getRunPromise)
    )
    .then(console.log)
    // ⚠️ 모두 실패해도 catch는 동작하지 않음
    .finally(() => {
      console.log('- - 경기 종료 - -');
    });
    
    
    //🚩 돌준 도착 - 1.0322985546617611초
    //{name: '돌준', time: 1032.298554661761}
    // - - 경기 종료 - -
    // 🚩 길돈 도착 - 1.1631042733434747초
    // 🚩 철수 도착 - 1.2487807030668345초
    // 🚩 정아 도착 - 1.3200488190607453초
    // 🚩 영희 도착 - 1.3673388376741022초
    ```

    => 위에서, 길돈 도착 부터는, 비동기 처리로 인한 결과물이며, resolve()는 실행되지 않음을 알 수 있다.

  * race

    * 성공, 실패에 관계없이 가장 첫번째 결과물을 반환
      * then() 또는 catch() 로 반환한다.

    ```javascript
    // 다섯 주자들이 선택한 도착지로 질주
    // 도착지에 '꽝'이 있으면(50% 확률) 실패
    function getBombRunPromise (name) {
      return new Promise((resolve, reject) => {
        const time = 1000 + Math.random() * 500;
    
        setTimeout(() => {
          console.log(`🚩 ${name} 도착 - ${(time)/1000}초`);
          if (Math.random() < 0.5) {
            resolve((`🙌 ${name} 승리!`));
          } else {
            
            reject((`💣 ${name} 꽝!`));
          }
        }, time);
      });
    }
    
    Promise.race(
      '철수,영희,돌준,정아,길돈'
      .split(',')
      .map(getBombRunPromise)
    )
    .then(console.log)
    .catch(console.error)
    .finally(() => {
      console.log('- - 경기 종료 - -');
    });
    
    
    
    //🚩 정아 도착 - 1.0801407471925275초
    //💣 정아 꽝!
    //- - 경기 종료 - -
    //🚩 길돈 도착 - 1.1205264261618435초
    //🚩 영희 도착 - 1.248736503487603초
    //🚩 철수 도착 - 1.402315335294787초
    //🚩 돌준 도착 - 1.4806423943234441초
    ```





### async & await 함수

async 함수

* 프로미스를 기반으로 동작한다

  * async 함수 내부에 await가 없는 경우, 동기 함수와 결과가 차이가 없게 된다.

    * 아래의 코드를 실행 시, 동기적으로 실행되었음을 확인할 수 있다.

    * ```javascript
      function getMult10Promise (number) {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            resolve(number * 10);
          }, 1000);
        });
      }
      
      async function doAsyncWorks () {
        console.log("1st");
        const result1 = getMult10Promise(1);
        console.log(result1);
      
        console.log("2nd");
        const result2 = getMult10Promise(2);
        console.log(result2);
      
        console.log("3rd");
        const result3 = getMult10Promise(3);
        console.log(result3);
        
        console.log("4th");
      }
      
      doAsyncWorks();
      console.log('💡 이 문구가 먼저 출력됨');
      
      
      //1st
      //Promise {<pending>}
      //2nd
      //Promise {<pending>}
      //3rd
      //Promise {<pending>}
      //4th
      //💡 이 문구가 먼저 출력됨
      ```

  * Promise 객체를 return 하는 함수를 호출할 때, await를 붙이지 않으면 Promise 객체가 반환된다.

    * 반면, await를 붙이게 되면, Promise 객체 내부의 PromiseResult 슬롯의 값이 반환된다.

      * 이 때, 반환되기까지 시간이 얼마간 걸리며, 이 과정은 비동기로 실행된다.

        => 자바스크립트의 실행 스레드는 그대로 다른 코드를 실행하게 된다.

      * 중요한 점은, async 내부 코드 전체가 비동기적으로 실행되지 않고, 맨 첫번째 await 직전까지는 동기적으로 실행됨을 알 수 있다.

      ```javascript
      function getMult10Promise (number) {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            resolve(number * 10);
          }, 1000);
        });
      }
      
      async function doAsyncWorks () {
        console.log("1st");
        const result1 = await getMult10Promise(1);
        console.log(result1);
      
        console.log("2nd");
        const result2 = await getMult10Promise(2);
        console.log(result2);
      
        console.log("3rd");
        const result3 = await getMult10Promise(3);
        console.log(result3);
        console.log("4th");
      }
      
      doAsyncWorks();
      console.log('💡 이 문구가 먼저 출력됨');
      
      
      
      //1st
      //💡 이 문구가 먼저 출력됨
      //10
      //2nd
      //20
      //3rd
      //30
      //4th
      ```

* try - catch를 이용하여, reject된 경우, reject된 인수를 넘겨받아 실행할 수 있다.

  ```javascript
  // 빌린 금액으로 약속을 하는 함수
  function moneyLend (borrow) {
    return new Promise((resolve, reject) => {
      console.log(`채무 ${borrow}만원`);
  
      setTimeout(() => {
        if (Math.random() < 0.1) {
          reject('채무자 파산');
        }
  
        resolve(borrow * 1.1);
      }, 1000);
    });
  }
  
  async function lend5times () {
    try {
      const lend1 = await moneyLend(20);
      const lend2 = await moneyLend(lend1);
      const lend3 = await moneyLend(lend2);
      const lend4 = await moneyLend(lend3);
      const lend5 = await moneyLend(lend4);
  
      console.log(`💰 반납 ${lend5}만원`);
    } catch (msg) {
      console.error(msg);
    } finally{
      console.log('- - 대금업 종료 - -');
    }
  }
  
  lend5times();
  
  //채무 20만원
  //채무 22만원
  //채무 24.200000000000003만원
  //채무자 파산
  //- - 대금업 종료 - -
  ```

* 릴레이를 할 때, 제한시간 내로 돌아오지 못하면 실패 메시지가 뜨게 하는 코드도 async-await 를 활용해서 짤 수 있다. 

  ```javascript
  const DEADLINE = 1400;
  
  function getRelayPromise (name, start, failMsg) {
    console.log(`👟 ${name} 출발`);
  
    // 💡 랜덤 시간만큼 달리고 결과를 반환하겠다는 약속을 만들어 반환
    return new Promise((resolve, reject) => {
      const time = 1000 + Math.random() * 500;
  
      setTimeout(() => {
        if (time < DEADLINE) {
          console.log(`🚩 ${name} 도착 - ${(start + time)/1000}초`);
          resolve(start + time);
  
        } else {
          console.log(failMsg);
          reject((start + time) / 1000);
        }
      }, time);
    })
  }
  
  async function relay5 () {
    try {
      const time1
       = await getRelayPromise('철수', 0, '철수부터 광탈입니다. ㅠㅠ');
  
      const time2
       = await getRelayPromise('영희', time1, '영희가 완주하지 못했네요.');
  
      const time3
       = await getRelayPromise('돌준', time2, '돌준이 분발해라.');
  
      const time4
       = await getRelayPromise('정아', time3, '정아에게 무리였나보네요.');
  
      const time5
       = await getRelayPromise('길돈', time4, '아아, 아깝습니다...');
  
    } catch (msg) {
      console.log(`😢 완주 실패 - ${msg}초`);
    } finally {
      console.log('- - 경기 종료 - -');
    }
  }
  
  relay5();
  
  
  //👟 철수 출발
  //🚩 철수 도착 - 1.3029266242147302초
  //👟 영희 출발
  //🚩 영희 도착 - 2.3954508363971065초
  //👟 돌준 출발
  //🚩 돌준 도착 - 3.480323119251557초
  //👟 정아 출발
  //🚩 정아 도착 - 4.590776739024533초
  //👟 길돈 출발
  //🚩 길돈 도착 - 5.9350017665714025초
  //- - 경기 종료 - -
  ```

  

### 네트워크 통신에서의 활용

Fetch API

* Web API에서 가져오는 기능으로서, 네트워크로부터 리소스를 받아온다

  * 프로미스 객체를 반환한다.
  * response.json()을 통해서, response body에 있는 텍스트를 JSON 객체로 변환하여 반환

  ```javascript
  fetch('https://showcases.yalco.kr/javascript/mockserver/race-result')
  .then(response => {
    console.log(response);
    return response;
  })
  .then(response => response.json())
  .then(console.log);
  
  //[{…}, {…}, {…}, {…}, {…}]
  //0: {runner_idx: 1, record: 1454.3881}
  //1: {runner_idx: 2, record: 1198.4922}
  //2: {runner_idx: 3, record: 1404.1087}
  //3: {runner_idx: 4, record: 1218.7154}
  //4: {runner_idx: 5, record: 1374.5151}
  //length: 5
  //[[Prototype]]: Array(0)
  ```

  ```JAVASCRIPT
  fetch('https://WRONG-ADDRESS')
  .then(response => response.json())
  .then(console.log)
  .catch(msg => {
    console.error(`😳 에러 발생: ${msg}`)
  })
  .finally(() => {
    console.log('- - 통신 종료 - -')
  })
  
    
  // GET https://wrong-address/ net::ERR_NAME_NOT_RESOLVED
  // 😳 에러 발생: TypeError: Failed to fetch
  // - - 통신 종료 - -
  ```

* 아래의 예시에 대해, Promise로도 구현이 가능하며, async와 await를 활용해서도 구현이 가능하다'

  * 예시
    * 5명의 경기 결과를 받아와서, 1등을 선별한다
    * 1등의 학교 정보에 대해 구체적으로 출력

  * 프로미스 형태로 구현

  ```javascript
  const SERVER_URL = 'https://showcases.yalco.kr/javascript/mockserver/';
  
  fetch(SERVER_URL + 'race-result')
  .then(result => result.json())
  .then(arry => {
    return arry.sort((a, b) => {
      return a.record - b.record
    })[0].runner_idx
  })
  .then(winnerIdx => {
    return fetch(`${SERVER_URL}runners/${winnerIdx}`)
  })
  .then(result => result.json())
  .then(({school_idx}) => school_idx)
  .then(schoolIdx => {
    return fetch(`${SERVER_URL}schools/${schoolIdx}`)
  })
  .then(result => result.json())
  .then(console.log)
  .catch(console.error);
  ```

  * async와 await로 구현

  ```javascript
  const SERVER_URL = 'https://showcases.yalco.kr/javascript/mockserver/';
  
  async function getResult() {
      //총 결과를 가져온다.
      //그 중, 점수가 가장 높은 사람을 선별하여 1등 식별자를 얻어낸다
      //1등 식별자를 토대로 1등에 대한 구체적인 정보를 얻어낸다 => 이 중, 학교 식별자를 얻어낸다.
      //학교 식별자를 토대로 학교 정보를 얻어서, 출력
      const totalResult = await fetch(`${SERVER_URL}race-result`)
          .then(result => result.json())
          .then(arr => {return arr.sort((a,b) => {return a.record - b.record})[0].runner_idx})
          .then(winnerIdx => fetch(`${SERVER_URL}runners/${winnerIdx}`))
          .then(result => result.json())
          .then(({school_idx}) => school_idx)
          .then(schoolIdx => {return fetch(`${SERVER_URL}schools/${schoolIdx}`)})
          .then(result => result.json())
          .then(console.log)
          .catch(console.error);
  }
  
  
  getResult();
  ```

  

## HTML 코드 파일 다루기

### HTML에 불러오는 방법들

일반적인 방법으로는, 동기적으로 HTML 파일을 파싱하므로, 아래와 같이 (HTML 요소를 활용한) JS파일을 HTML 파일 뒷부분에 명시해두면 에러가 발생한다.

```html
<!-- index.html -->

<!DOCTYPE html>
<html lang="ko">
<head>
  <title>제대로 파는 자바스크립트</title>
  <script src="./src/script.js"></script>
</head>
<body>
  <span>변경 전...</span>
</body>
</html>
```

```javascript
//script.js
//위치 : ./src/script.js

document.querySelector('span').innerText = '텍스트 변경됨';
```

* 위의 html 파일을 실행하게 되면, (브라우저의 콘솔창에) 아래와 같이 뜨게 된다.

  ```javascript
  Uncaught TypeError: Cannot set properties of null (setting 'innerText')
      at script.js:1:42
  ```

  * (내 생각) 이미 innerText 라는 프로퍼티는, document.querySelector 의 프로퍼티로서 이미 가지고 있지 않았나 생각된다. (왜냐하면, 프로퍼티의 값이 null이라고 떠있기 때문)

* 따라서, `<script src="./src/script.js"></script>` 을 body 요소의 맨 아래 부분에 배치하면 해결은 되지만, 정답은 아니다.

  * 왜냐하면, 애초에 `<script src="./src/script.js"></script>` 는, head 요소에 넣으라고 만든 태그이기 때문이다

    => onload 이벤트를 활용하면 되기는 하지만, 동기적이라는 한계가 존재. 

    (즉, 비록 실행은 맨 나중에 되어서 로직적으로는 문제가 생기지 않지만, js파일이 크다면, 로딩하는 동안 여전히 아래의 요소들은 파싱이 되지 않는다.)

    ```html
    <!-- index.html -->
    
    <!DOCTYPE html>
    <html lang="ko">
    <head>
      <title>제대로 파는 자바스크립트</title>
      <script src="./script.js"></script>
    </head>
    <body>
      <span>변경 전...</span>
    </body>
    </html>
    ```

  * ```javascript
    //script.js
    //위치 : ./src/script.js
    
    window.onload = function() {
    	document.querySelector('span').innerText = '텍스트 변경됨';
    }
    ```






HTML 파싱

* 기본적으로, HTML 파일은 동기적으로 파싱한다.

  * 따라서, body요소보다 스크립트가 먼저 로드되는 경우, 변수에 원치 않은 데이터가 저장될 수 있다.

    * 이 경우, 기본적으로 스크립트를 맨 뒤로 쓰면 해결되는 문제이다.

    * 혹은, 스크립트를 비동기적으로 실행하게 하여, 스크립트를 로딩하는 도중에도 html 파싱이 지속해서 일어나도록 한다.

      => defer, async 방식을 사용하거나, onload 방식이 존재한다

    * onload 방식은, window객체의 onload 메서드를 오버라이딩 함으로서 구현된다

      * onload함수 자체가, 문서가 사용되는 시점에 실행된다는 특징을 활용한 것이다.

        => script가 먼저 로딩이 되더라도, script의 실행은 맨 나중으로 되므로 원하는 의도대로 구현이 된다.

      * 출처

        * https://velog.io/@leyuri/javaScript-window.onload%EB%9E%80

      * 하지만, onload 방식 역시 동기적이라는 한계점이 존재.

    * async, defer 방식은 비동기적으로 스크립트를 로딩하는 점이 공통적이나, 실행 시점에서 차이를 보인다.

      * async 방식은 (비동기적인) 스크립트의 로딩이 끝나자마자 스크립트가 실행이 된다

        * 이 때, 스크립트가 실행되는 동안은 html 파싱이 멈춘다.

        * async 속성이 붙은 script는 페이지와 완전히 독립적으로 동작하므로, html에서 async 스크립트의 배치 순서대로 script가 실행이 되지는 않는다.

          => 길이가 짧은 async script가 맨 아래에 배치되는 경우, 이것이 가장 먼저 실행될 수 있다는 의미이다.

        * 따라서, DOM을 조작하는 코드가 async script에 존재한다면, 원하지 않은 결과를 얻을 수 있다.

      * 반면, defer 방식은, (비동기적인) 스크립트의 로딩이 끝나도 스크립트의 실행이 지연되며, html의 파싱이 끝나고 나서야 비로소 실행이 된다.

        * defer 속성이 붙은 script는 html에서의 defer 스크립트 배치 순서대로 실행이 된다. (html 페이지와 defer 스크립트는 의존관계에 있다는 의미로 해석할 수 있다.,)

      * 출처

        * https://ko.javascript.info/script-async-defer

* 참고

  * 자바스크립트는, 기본적으로 싱글 스레딩이다.

    * 자바스크립트에서 비동기 처리를 하는 코드를 짜더라도, 처리 순서에 차이가 있을 뿐 사실 주요 로직은 싱글 스레드에서 처리가 되기 때문이다.

      => 자바스크립트에서도 멀티 스레드 코드를 짜게끔 하기 위해, "웹 워커" 라는 개념이 도입되었다.

    * 출처

      * https://inpa.tistory.com/entry/%F0%9F%8C%90-js-async#%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98_%EB%B9%84%EB%8F%99%EA%B8%B0_%EC%B2%98%EB%A6%AC
      * https://www.zerocho.com/category/HTML&DOM/post/5a85672158a199001b42ed9c



### 모듈과 라이브러리

html 페이지에서, 모듈을 활용하지 않고 자바스크립트 파일을 (비동기적으로) 활용하게 되면 아래의 문제가 발생한다

* 여러개의 script 파일로 나누어 작성하더라도, 결국 하나의 큰 파일을 작성하는 것과 다를 바가 없어진다
  * 각각의 파일에서는, 같은 변수명이나 상수를 사용하지 못한다.
  * 또한, 이로부터, 다른 파일에 있는 변수명에 저장된 값을 원치 않은 의도로 조작이 될 수 있음을 알 수 있다. 
  * 각각의 파일이 의존적이므로, html에서 스크립트 파일 코드를 작성 시, 파일의 순서를 신경써야만 한다.
* => 결국, 모듈을 활용하여 위의 문제를 해결하여야 한다. 



모듈 활용 예시

* html 문서에 로드하고자 하는 모듈을 명시한다. (모듈 A 라고 하자)

  * 이 때, 모듈 A는 자동으로 defer로 로드된다.
  * 해당 모듈 A는, 다른 모듈 B의 변수의 값을 읽어올 수 있으며, 이는 export / import를 활용해서 이루어진다.
    * 이 때 B는 html 문서에 명시할 필요는 없다.
    * B에서 변수에 대해 export 하여 다른 모듈에서 해당 변수를 읽어들이게끔 하고, A에서는 import 하여 해당 변수의 값을 읽어들인다. (이 값을 다른 변수로 naming 해서 받아들일 수도 있다 => 식별자 중복 방지)

  ```html
  <!-- index.html -->
  
  <!DOCTYPE html>
  <html lang="ko">
  <head>
    <title>제대로 파는 자바스크립트</title>
  
    <!-- 💡 모듈로서 로드 -->
    <script type="module" src="./main.js"></script>
  </head>
  <body>
    <script>
      console.log('모듈은 defer 방식으로 로드됩니다.');
    </script>
  </body>
  </html>
  ```

  ```javascript
  <!-- main.js -->
  
  import { 
    x as a,
    y as b,
    person as individual
  } from './module1.js';
  
  console.log(a, b);
  console.log(individual);
  ```

  ```javascript
  <!-- module1.js -->
  
  export const x = 1;
  export const y = 2;
  
  export const person = {
    name: '홍길동',
    age: 20
  }
  ```

  

* import 하는 모듈에서, 모든 객체를 다 읽어들일 수 있으므로 아래의 예시 또한 가능하다.

  * 아래의 eagle객체는, Bird 클래스를 import 하지 않았음에도 Bird에 있는 기능을 사용할 수 있따

    * 다만, Bird 클래스를 활용해 객체를 생성하는 코드는 허용되지 않는다. (실험 결과임)

      => 이 부분은, Eagle 객체 생성 전이나 후나 동일하게, Bird 클래스만을 활용해서 객체를 생성하는 것은 허용되지 않았다.

      => (내 생각) 일단 모듈 module3.js 전체 코드가 메모리에 올라는 가는데, main.js에서 "문법적으로" 접근하는 것이 막혀있는 듯 하다. (low level 관점에서.... 바라본 내 생각임.)


  ```javascript
<!-- module1.js -->

export const x = 1;
export const y = 2;

export const person = {
  name: '홍길동',
  age: 20
}
  ```

  ```javascript
<!-- module2.js -->

export const add = (a, b) => a + b;
export const subt = (a, b) => a - b;
export const mult = (a, b) => a * b;
export const div = (a, b) => a / b;
  ```

  ```javascript
<!-- module3.js -->

export class Bird {
  constructor (name, sound) {
    this.name = name;
    this.sound = sound;
  }
  fly () {
    console.log(`${this.name} ${this.sound} 비행중`);
  }
};

export class Eagle extends Bird {
  constructor (name, sound, prey) {
    super(name, sound);
    this.prey = prey;
  }
  hunt () {
    console.log(`${this.name} ${this.prey} 사냥중`);
  }
};
  ```

  ```javascript
<!-- main.js -->

// 💡 필요한 것만 선별하여 가져오기
import { x, y } from './module1.js';
import { add, mult } from './module2.js';
import { Eagle } from './module3.js';

console.log(
  add(x, y), mult(x, y)
);

const eagle = new Eagle('독돌이', '푸드덕', '토끼');
eagle.hunt();
  ```

* 다른 모듈에 있는 것을 선별해서 가져오는 것이 아니라, 통째로(하나의 모듈 객체로) 묶어서 가져올 수 있다.

  ```javascript
  <!-- module4.js -->
  
  export const isOdd = x => x % 2;
  export const square = x => x ** 2;
  
  export function logResult (result) {
    console.log(
      `결과는 ${result}입니다.`
    );
  };
  ```

  ```javascript
  <!-- main.js -->
  import * as funcs from './module4.js';
  
  // 💡 로그 살펴볼 것!
  console.log(funcs);
  
  funcs.logResult(
    [1, 2, 3, 4, 5, 6, 7, 8, 9]
    .filter(funcs.isOdd)
    .map(funcs.square)
    .join(', ')
  );
  ```

* default를 사용하여, 다른 모듈에서 참고할 수 있도록 할 수도 있다.

  ```javascript
  // 💡 default를 사용하면 let, const 사용 불가
  // main.js에서 mod5 변수로서 받을 것이다.
  export default {
    x: 1,
    arry: [1, 2, 3, 4, 5],
    obj: {
      a: true,
      b: false
    },
    isEven: x => !(x % 2),
  };
  
  export let z = 4444;
  ```

  ```javascript
  <!-- main.js -->
  //mod5로서 default 객체를 받아들인다.
  import mod5 from './module5.js';
  
  console.log(mod5);
  
  console.log(
    mod5.arry
    .filter(mod5.isEven)
    .join(', ')
  );
  ```

* node.js에서 모듈을 사용하고자 할 때에는 아래와 같이 활용하자

  * package.json에 아래의 type 항목을 추가

    => 이는, module에서 통용되는 export / import 문법을 사용할 수 있게 해 준다.

    ```javascript
    {
      "type": "module"
    }
    ```

  * package.json은, 프로젝트의 메타 정보를 담고 있다.

    * json 형식으로 작성 

    * 의존성 관리, 스크립트 정의, 기타 설정 등을 할 수 있다.

    * 이 때, 모듈 타입을 지정할 수 있으며, type 속성을 통해서 ES6 모듈 시스템을 사용함을 지정할 수 있다.

      => 이렇게 되면, import / export 코드로 짠 javascript 파일이 실행이 가능해진다.

    * 참고

      * https://beomy.github.io/tech/etc/package-json/







참고

* 실험을 통해 알아낸 경우는 아래와 같다

  * 하나의 HTML 페이지에 2개 이상의 모듈을 쓸 수 있다.

  * (잘 안 쓰이겠지만) 1개의 모듈 페이지가 다른 (모듈 아닌) 스크립트의 파일을 참조할 수 있다. (별도의 export, import 를 (모듈 아닌) 스크립트 파일에 명시하지 않고도 가능하다)

    * 참고) 아래 html 페이지에서, script 코드의 순서를 뒤바꾸면 tt 변수를 읽어들이지 못 한다.

    ```html
    <!-- index.html -->
    
    <!DOCTYPE html>
    <html lang="ko">
    <head>
      <title>제대로 파는 자바스크립트</title>
      <script defer src="./script1.js"></script> <!-- 모듈이 아닌 자바스크립트 파일-->
      <script type="module" src="./test2.js"></script>
      <!--위의 script 순서를 바꿔서 작성하면 tt 변수를 읽어들이지 못함 -->
    </head>
    <body>
    </body>
    </html>
    ```

    ```javascript
    <!-- script1.js -->
    const tt = 1;
    
    console.log(tt);
    ```

    ```javascript
    <!-- test2.js -->
    import {a,b} from './main.js';
    
    console.log(tt);
    
    console.log('-------');
    console.log(a);
    console.log(b);
    ```

  * 기본적으로, 하나의 모듈 파일에서 import 하는 모듈 파일은, (로딩이 되지 않았다면) 해당 파일을 로딩과 동시에 실행한다.

    * 이미 로딩이 된 상태라면, 건너뛴다.

    ```html
    <!DOCTYPE html>
    <html lang="ko">
    <head>
      <title>제대로 파는 자바스크립트</title>
      <script type="module" src="./script1.js"></script>
      <script type="module" src="./test2.js"></script>
    </head>
    <body>
    </body>
    </html>
    ```

    ```javascript
    <!-- script1.js -->
    export const tt = 1;
    
    console.log(tt);
    ```

    ```javascript
    <!-- test2.js -->
    
    import {a,b} from './main.js';
    import {un} from './test3.js';
    import {tt} from './script1.js';
    
    console.log(tt);
    
    console.log('-------');
    console.log(a);
    console.log(b);
    ```

    ```javascript
    <!-- test3.js -->
    export const un = 100;
    
    console.log(un);
    ```

    ```javascript
    //결과
    
    1    script1.js:3
    1 2     main.js:5 
    {name: '홍길동', age: 20}     main.js:6 
    100    test3.js:3 
    1 	test2.js:8 
    -------   test2.js:10 
    1 	test2.js:11 
    2 	test2.js:12 
    ```

    => test2.js에서, import하는 순서대로 자바스크립트 파일이 실행이 되었음을 알 수 있다. 



### 웹팩과 바벨

웹팩

* 다수의 파일(js, html, css, png 등)을 하나 또는 소수의 파일들로 압축

  => 하나의 파일로 번들링한다고 한다.

  => entry, output 등의 속성을 활용하여 원하는 번들링을 할 수 있다.

  * 여러가지 파일을 하나로 압축하므로, http 요청 수가 줄어들어서, 네트워크 환경이 다소 느리더라도 웹사이트 로딩 속도가 최적화 된다는 장점이 있다.
  * 참고
    * https://myung-ho.tistory.com/98

* webpack.config.js 파일에서 작성하게 되며, 보통 commonJS 형식으로 쓰인다.

  * 때문에, ES6 모듈 시스템을 사용하지 않아도 되므로 package.json 파일에서 `{"type" : "module"}` 항목을 제거해도 된다.
    * (의문 사항) - 제거하지 않으면 에러가 발생하던데, 저 type 속성이 결국에는 commonJS랑 ES6 모듈 시스템이랑 양자택일해서 읽는? 시스템인지 싶다.
  * 결국, 웹팩이 build 역할을 하게 되는 것이므로, 프로젝트 메타파일(package.json)에서 "빌드는 webpack.config.js"에서 이루어짐을 명시해주는 코드가 있어야 한다.
  * (강의 내용으로 최종 요약)
    * webpack.config.js에서 require 방식을 쓰기 때문에, `{"type" : "module"}` 를 제거하면 webpack.config.js에서 require 방식을 적용하게 되고, 명시되어 있는 코드대로 (=모듈 방식으로) 번들링을 진행하게 된다.

* 주요 과정은 아래와 같다

  * 소스저장소(src폴더)를 만들고, 모든 소스 파일을 해당 폴더로 이동.

  * 웹팩 관련 모듈 설치

  * 웹팩 설정 파일 작성 (주요사항 작성 예시)

    ```javascript
    //webpack.config.js
    
    const path = require('path'); //path 모듈을 가져온다.
    
    module.exports = {
      entry: './src/main.js',
      output: {
        filename: 'main.js',
        path: path.resolve(__dirname, 'dist'), //배포되는 파일. 즉, main.js와 main.js가 필요한 모듈들이 하나의 파일로 번들링되는 폴더를 의미
      },
    
      // 💡 추가설정들
      watch: true, // 파일 수정 후 저장시 자동으로 다시 빌드
      experiments: {
        topLevelAwait: true // 모듈 await 가능하도록
      }
    };
    ```

    

  * 빌드 명령

    * npm run build를 통해서 실행

    * 이 때, package.json에서, webpack.config.js를 참조하는 코드가 없다면, 이 코드를 추가하기.

      * `"scripts": {    "build": "webpack"  }` 

    * 배포된 파일의 코드를 javascript beautifier 에 넣고 돌리면, 원래 코드와 유사한 코드가 등장한다.

      (더러운 코드가 되는 이유는, 번들링 과정에서 역으로 해석(?) 하는 것을 방지하기 위해서이다)

* 웹팩 관련 추가 참고사항

  * 주요 속성 (entry, output, loaders, plugins ...)
    * https://dev-chim.tistory.com/entry/Webpack-webpackconfigjs
    * https://velog.io/@suyeon9456/Webpack



바벨

* 자바스크립트를 보다 더 오래된 환경에서도 동작하는 버전으로 컴파일하는 모듈

* 따라서, 아래의 과정으로 실행하는 것이 큰 그림이다.

  * 바벨 관련 모듈 설치

  * webpack.config.js에 설정 추가 (위 바벨 관련 모듈을 사용하겠다는 설정)

    => 1개 파일 각각에 대해서 바벨을 적용해도 되지만, 궁극적으로는 "웹팩"을 통해 번들링된 파일에 대해 바벨을 적용하는 것이 보다 더 현명할 것이다.

    * 예시

      ```javascript
      const path = require('path');
      
      module.exports = {
        entry: './src/main.js',
        output: {
          filename: 'main.js',
          path: path.resolve(__dirname, 'dist'),
        },
      
        // 💡 추가설정들
        watch: true, // 파일 수정 후 저장시 자동으로 다시 빌드
        experiments: {
          topLevelAwait: true // 모듈 await 가능하도록 (원래는 브라우저상에서만 await 기능을 쓸 수 있었음)
        },
      
        //아래는 바벨 관련 설정
        target: ['web', 'es5'], // ⭐ ES5 이하로 해야 할 시 필요
        module: {
          rules: [
            {
              test: /\.m?js$/,
              exclude: /node_modules/,
              use: {
                loader: 'babel-loader',
                options: {
                  presets: [
                    ['@babel/preset-env', { targets: "ie 11" }]
                  ]
                }
              }
            }
          ]
        }
      };
      ```

  * 빌드하고 결과 확인



### JSDoc

자바스크립트 코드에 주석을 달기 위한 마크업 언어

* 그리고 해당 주석을 활용하여, API 문서를 생성할 수 있다. API 문서를 생성하기 위해 보통 사용한다

* 웬만한 에디터는, JSDoc 기능을 제공하므로, /** 를 치게 되면 JSDoc 기능을 사용할 수 있는 주석 기능을 활용할 수 있다.

  * 해당 주석을 근거로, 에디터에서는 hinting을 제공한다

* 예시

  ```javascript
  /** 
   * 코드의 제목으로 사용될 문자열
   *  
   */
  const TITLE = 'JSDoc 사용하기';
  
  /**
   * 원주율
   * @type {number}
   * @const
   */
  const PI = '3.14';
  
  
  /**
   * 함수 예시
   * 
   * @param {number} x 
   * @param {number} y 
   * @returns {number} 두 수의 합
   */
  const add = (x, y) => x + y;
  
  
  /**
   * 추후 주석에서 PersonObj 객체가 등장하면, 해당 객체가 무엇인지 나타내주는 역할을 수행.
   *  - 주석을 지우게 되더라도, hinting에는 영향이 없다.
   * 
   * @typedef {Object} PersonObj 사람 객체
   * @property {string} name 이름
   * @property {number} age 나이
   * @property {boolean} married 기혼여부
   */
  
  /**
   * 
   * @param {string} name 이름
   * @param {number} age 나이
   * @param {boolean} married 기혼여부
   * @returns {PersonObj}
   */
  function getPersonObj (name, age, married) {
    return {name, age, married}
  }
  
  
  
  /**
   * 사람 객체 생성 함수
   * @constructor 
   * @param {string} name 
   * @param {number} age 
   */
  function Person (name, age) {
    this.name = name;
    this.age = age;
  }
  
  
  /**
   * 새 클래스
   * @class
   */
  class Bird {
    /**
     * @constructs
     * @param {string} name 
     */
    constructor (name) {
      this.name = name;
    }
  }
  
  
  /**
   * 개선사항이 필요할 때, (개발자들이) 활용함
   * @todo 실행 속도 개선 필요
   */
  function slowFunction () {
    console.log('느릿느릿');
  }
  
  
  /**
   * @see {@link https://www.yalco.kr} 얄코사이트 참조
   */
  function yalcoFunc () {
    // ...
  }
  
  /**
   * @readonly
   * @const {string}
   */
  const READONLY = '건들지 마라';
  
  
  /**
   * @deprecated 버전 3부터 안 씀
   */
  function oldFunction () {
    console.warn('왜 실행했어요?');
  }
  
  
  ```

* 이후, jsdoc API 생성 모듈을 다운받은 후, 해당 모듈을 통해 생성된 html 파일을 브라우저에 띄우자

  * 그것이 바로 Jsdoc API 문서라고 할 수 있다.




### 디버깅

일반적으로, 디버깅 설정을 하려면, launch.json을 조작하면 된다. 



launch.json 기본

```javascript
{
  // IntelliSense를 사용하여 가능한 특성에 대해 알아보세요.
  // 기존 특성에 대한 설명을 보려면 가리킵니다.
  // 자세한 내용을 보려면 https://go.microsoft.com/fwlink/?linkid=830387을(를) 방문하세요.
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "localhost에 대해 Chrome 시작",
      "url": "http://localhost:8080",
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

출처 : https://terrorjang.tistory.com/entry/VSCode-Javascript-%EB%94%94%EB%B2%84%EA%B9%85





주요내용 정리

* debug console에서, 중간중간에 x의 값을 변경하여 로직을 진행할 수 있다.

* 디버깅으로, Exception을 체크할 수도 있다. Uncaught Exception 과 Caught Exception 둘 다 체크가 가능하다.

(큰 팝업 화면으로 체크가 됨)

* 조사식(watch)에서, 참고하고자 하는 변수를 활용하여, 식을 만들어서 대입하면, 해당 식의 값을 디버깅 과정에서 관찰할 수 있다.

* 중단점을 구체화하여, 아래와 같이 설정이 가능하다

  * 조건부 중단점, hit count

    => 특정 조건을 만족했을 때에만, 중단되게끔 할 수 있다.

    => 또한, for문 내부에서, 해당 코드가 일정 횟수 이상 반복되면, 해당 코드에 대해 중단되도록 할 수 있다. 





* 브라우저 디버깅은, 새로고침을 함으로서 실행이 되며, 이 때 breakingPoint는 브라우저 자체적으로 기억하는 듯하다. (이 때 line number로서 기억을 하는 듯 하다)
  * 브라우저 상에서 코드를 바꾼 후, 다시 새로고침을 하게 되면, 이전에 지정한 breakingPoint 의 line number 상에 breaking point가 걸려 있는 것을 확인할 수 있다. 





나의 의문사항

* 아래와 같이, export 가 들어가있는 코드는 디버깅이 실행되지 않더라. export를 뺴니까 debugging이 동작하더라.

  * 이유는 정확히 모르겠음..... 다만, 이러한 현상이 있다는 점은 인지하고 있을 것.

  ```javascript
  //디버깅이 동작하지 않음
  export const ppppp =331313131;
  const un = 100;
  
  const pn = 3;
  pn += 5500;
  un += 44000;
  
  console.log(un);
  ```

  

  ```javascript
  //breaking point를 걸면, 디버깅이 동작한다. 
  const un = 100;
  
  const pn = 3;
  pn += 5500;
  un += 44000;
  
  console.log(un);
  ```

  





## 웹페이지에 활용하기

### DOM의 개념

document는 브라우저의 객체이므로, node.js에서는 출력되지 않는다.

=> 브라우저의 콘솔에 출력하면, DOM 관점으로 출력된다.

=> 자바스크립트 상으로는, children (또는 childNodes) 프로퍼티에 자식 요소가 유사배열에 담긴 형태로 DOM 구조가 구현되어 있다.



아래의 코드는, 각 요소의 족보를 확인하는 코드이다.

=> 코드의 대략적인 순서도는 아래와 같다.

* document 자기 자신에 대한 족보를 출력한다.

* document의 모든 자식 요소를 "남김없이" 추출해낸다. 
  * 각각의 자식 요소마다, 해당 요소의 족보를 출력한다.

```javascript
function listAncestors(obj) {
    let parentNode = obj;
    let answer = [];
    while(parentNode){
        answer.push(parentNode.constructor.name);
        parentNode = Object.getPrototypeOf(parentNode);
    }
    
    return answer.join(', ');
}

function printAncestors(node) {
    console.log(listAncestors(node));
    for(child of node.children) {
        printAncestors(child);
    }
}

printAncestors(document);
```







### 요소 선택과 탐색

주요 참고사항

* 변수명 앞에 $를 포함되어 있다면, (관례적으로) 해당 변수에는 html 요소가 포함되어있다는 것을 나타낸다.

* html상에서 라인마다 태그를 쓸 때, 자동으로 발생하는 textNode는 아래의 성질을 지닌다

  * html body 상에서 각 태그의 맨 앞 빈 공간을 의미한다. (textContent를 보면, "\n     "  으로 되어 있음을 알 수 있다.)

    => 이는, 태그를 사용하지 않고 그냥 text를 사용했을 때와 구분하기 위해서이다.

* 자식 노드를 검색할 때, 실제로 빈 공백(`\n` ) 까지 포함하는 노드까지 검색하는 방법이 있다. (childNodes 프로퍼티 활용)

  => 실제로, 위 방법대로 모든 노드를 "정확하게" 찾는다면, 웹 페이지의 구조를 정밀하게 파악할 수 있지 않을까 싶다.

  => 바로 위의 "자동으로 발생하는 textNode" 에 관한 내용을 본다면, 이해가 될 것이다.



document의 메서드와 element의 메서드가 있다.

=> 대게 비슷하나, getElementById()는 document 객체에만 정의된 메서드이다.



nodelist가 htmlcollection 보다 더 많은 타입을 담을 수 있다고 하는데, 구체적으로 어떻게 다양한 타입을 담는지?













`ul.firstChild` 와 `ul.firstElementChild` 의 차이

* 첫번째 노드를 뽑기 위해 전체 Node를 고민할 때, 모든 Node중 첫번째 Node만 선택하는지(`ul.firstChild`) 아니면 첫번째 ElementNode를 선택하는지(`ul.firstElementChild`)의 차이이다.
  * `ul.firstChild` 는 빈 공백의 textNode도 포함하기 때문에, ul의 자식 노드인 li노드를 정확하게 선택하기 위해서는 `ul.firstElementChild` 를 활용하는 것이 맞다.
* 즉, Node의 메서드인지 Element의 메서드인지의 차이이며, return 값도 각각 Node(ElementNode 포함) 와 ElementNode 만이라고 정리할 수 있다.





위에서 보듯, 본질적으로 Element의 메서드인지, Node의 메서드인지로 구분되어진다. 

=> 이를 활용해서, 특정 노드 바로 옆의 Node (또는 ElementNode)와 부모 Node(또는 ElementNode) 역시 각각의 경우에 대해 모두 return받을 수 있다. 

```javascript
const $secondLi = document
.querySelector('section')
.querySelector('li:nth-child(2)');

//Node의 메서드
$secondLi.previousSibling;
$secondLi.nextSibling;
//Node의 메서드
$secondLi.parentNode;

//Element의 메서드
$secondLi.previousElementSibling;
$secondLi.nextElementSibling;
// 💡 역시 Node의 기능 - 부모 노드가 Element일 때만 반환
$secondLi.parentElement;

//부모 노드에 ElementNode만 존재하는 경우, 아래의 결과는 true임을 알 수 있다.
$secondLi.parentNode === $secondLi.parentElement;
```



### 요소 조작

innerText 대신 textContent를 써야 하는 이유는 아래와 같다.

* css와 같이 숨겨진 요소들에 대한 text도 모두 출력
* 출처
  * https://developer.mozilla.org/ko/docs/Web/API/Node/textContent
  * https://velog.io/@kim_unknown_/JavaScript-Difftext



nodeValue의 경우는, 텍스트 노드의 경우에서만 해당 노드의 텍스트값을 반환한다.

* 다른 노드의 경우에는, null값을 반환 (textContent와 가장 큰 차이)

  * li 노드 역시 엄연히 element 노드라, li.nodeValue 의 값은 null이 나온다

    => 따라서, nodeValue를 활용하여 li 노드의 text에 접근하고 싶다면, li.firstChild.nodeValue 로서 접근하면 된다.



className의 경우에는, class에 관해 접근할 수 있다.

=> 이를 활용하여, css 선택자가 먹을 수 있게끔 할 수 있다.

=> 2개 이상의 css 선택자가 적용되도록 할 수도 있다.



classList의 경우는, class 이름을 DOMTokenList라는 유사배열객체에 반환한다.

=> 해당 배열 객체에 요소를 추가하거나 배제해서, css 선택자가 먹을 수 있게끔 할 수 있다.





style은 HTMLElement의 속성이며, 폰트 같은 속성을 적용할 수 있다.

=> 주의해야 할 점은, "인라인으로 정의된 CSS 속성" 에 대해서만 확인/변경이 가능핟.

* html에 css를 입힐 때 3가지 방법이 있으며, 보통 외부 스타일 시트를 사용한다
* HTMLElement의 style 프로퍼티를 활용하여 CSS 속성을 반영하게 되면, HTML 페이지의 태그 내에서도 해당 내용이 반영됨을 확인할 수 있다.
  * 즉, 인라인 스타일로 반영됨을 알 수 있다.
* 출처
  * https://m.blog.naver.com/dahamee/220501535751



=> 따라서, 인라인 외의 방식으로 CSS 속성 정보를 확인하고자 한다면, 아래와 같이 하면 된다.

* window.getComputedStyle(요소) 를 적용 시, 해당 요소에 정의된 CSS 속성 정보가 담긴 객체를 얻을 수 있다.
  * getComputedStyle은 특정 요소의 CSS 속성 정보들을 반환한다.
    * 특정 요소의 속성 정보에서, 그 요소의 font-size나 opacity나 color 등을 조회할 수 있다.
  * 조회만 가능하고, 수정은 불가하다. 
    * (내 생각) 당연한게, CSS를 정의할 수 있는 방법이 3가지인데, 해당 방법에 맞게끔 일일이 수정하기는 힘들것으로 생각된다.







getAttribute, setAttribute 메서드는 요소의 속성을 조회/변경하는 기능을 수행





value와 checked는 input 요소의 기능으로서

* document.querySelctor() 작성 시, 매개변수는 CSS 속성 조회 문법을 따른다. (querySelector 메서드 자체가 CSS 속성 조회 문법을 따른다.) 
  * `document.querySelector('input[name=message]')` 역시 매개변수를 보면, CSS 속성 조회 문법을 따른 것이다.
  * 출처
    * https://duknock.tistory.com/16





(element).innerHTML 은 내부의 자식 요소들을 그대로 HTML 형식으로 옮겨놓은 것이다.

* 따라서, (element).innerHTML = '' 로 지정하면, 내부의 자식 요소들이 모두 삭제된다.

* 출처
  * https://developer.mozilla.org/ko/docs/Web/API/Element/innerHTML









의문

//`$ul.innerHtml=''` 을 활용하여 내부 요소를 삭제하는 것은 왜 비추천 되는지? (removeChild와 innerHtml을 활용하여 삭제하는 방법 모두, 수동으로 제거해야 한다는 결론을 보았음.)







document에 요소를 생성해서 추가하는 방법

1. `document.createElement()` 를 통해서 요소를 생성한다. (section, ul, li 등등)
2. `element.appendChild()` 를 통해서, element 요소 내부에 자식 요소를 추가한다. (맨 끝에)
3. 해당 자식 요소의 속성(textContent, classList 등)을 활용하여, 추가하고자 하는 내용을 입력한다.





참고

* XSS 공격

  * 결국, 사용자의 브라우저에 악성 스크립트 코드가 전달되어 실행되게끔 하는 것이 핵심이다. 

  * 아래의 3가지 방법이 있다. 

    * 웹 서버를 활용하는 방법 

      1. 일반적인 웹 서버에 악성 스크립트를 영구적으로 저장하는 방법(stored XSS)
         * 사용자가 해당 url을 클릭하면 자연스럽게 사용자의 웹 브라우저에 악성 스크립트 실행

      2. 공격자는 사용자에 악성 url을 보내는 방법 (reflected XSS)

         * 해당 url의 쿼리 파라미터에는 악성 스크립트가 작성되어 있다.

         * 사용자가 해당 url을 클릭 시, 서버는 해당 url 쿼리 파라미터를 활용하여 사용자에게 응답하며, 사용자의 웹 브라우저에는 악성 스크립트가 실행됨

    * 웹 서버를 활용하지 않는 방법(DOM based XSS)

      * 서버의 보안과는 상관없이, 웹 브라우저의 취약점을 활용하여 악성 스크립트 실행

        => 즉, 서버로 요청을 보내지 않고, 웹 브라우저의 구조를 변경하는 방식으로 실행된다.

        * 예를 들어, Attacker가 조작된 URL을 순진한 Customer에게 보낸다고 가정하자.

          => 해당 URL은 다음과 같은 구조를 지니게 된다.

          `https://example.com/page#<script>alert('DOM-based XSS!');</script>`

          => 즉, #이후의 부분은 브라우저 자체적으로 반영되는 부분이므로, 해당 부분이 악성 스크립트가 입력되면 서버의 보안이 강력하다고 해도 XSS Attack을 막을 수 없다.

          (서버 입장에서는, #이전 부분까지의 URL만 요청받는다.)

      * reflected XSS와의 가장 큰 차이는, 서버가 XSS Attack에 영향을 끼쳤나의 여부이다.

        * reflected XSS의 경우는 서버의 보안이 취약할 때 발생 가능한 XSS 공격이지만, DOM based XSS의 경우는 서버의 보안과는 관계없이 웹 브라우저의 보안 취약으로 인해 발생 가능한 XSS 공격이다.

        * URL로 XSS Attack 할 때 경우를 예로 들자면, 각각의 XSS 공격에 따라 조작된 URL은 아래와 같이 될 수 있다.

          * reflected XSS

            `https://example.com/search?query=<script>alert('Reflected XSS!');</script>`

          * DOM based XSS

            `https://example.com/page#<script>alert('DOM-based XSS!');</script>`

  * 출처

    * https://maker5587.tistory.com/57
    * https://berr-my.tistory.com/entry/XSS-%EA%B3%B5%EA%B2%A9



### 이벤트



```javascript
const $button2 = document.querySelector('#button2');

let timeout;
let interval;
let countdown;

timeout = 100;

$button2.addEventListener('mouseenter', () => {
  if (timeout) clearTimeout(timeout); //setTimeout으로 실행할 함수가 있다면, 이를 실행하지 않겠다는 의미. (즉, 해당 이벤트를 2번 입력했을 때, setTimeOut으로 실행할 함수는 1번만 실행되도록 함)
  console.log(timeout);
  console.log("----");

  $button2
  .firstElementChild
  .textContent = '💣 치워라, 5초 준다';

  timeout = setTimeout(() => {
    $button2
    .firstElementChild
    .textContent = '🔥🔥🔥🔥🔥🔥🔥🔥🔥';
  }, 5000);
  console.log(timeout);
});

console.log("aaaa")

$button2.addEventListener('mouseleave', () => {
  if (timeout) clearTimeout(timeout); //mouseenter 입력을 받았을 때, 실행되는 setTimeout 의 인자로 받은 함수 실행을 하지 않는다.

  $button2
  .firstElementChild
  .textContent = '올리지 말라고 하면 올리지 마라';
});
```

* addEventListener() 함수는 비동기 함수로서, 첫번째 인자로 주어진 행동이 들어와야 두번째 인자의 함수가 실행이 된다.
* clearTimeOut은, setTimeout의 결과물인 식별자(timeOutID)에 대해서 해당 setTimeout() 함수의 매개인자로 받은 함수의 실행을 취소한다.





어떠한 칸에 내용들을 입력하고 난 후, 엔터를 치면, 해당 내용들을 ul의 자식요소로서 추가하는 코드

```javascript
const $ul = document.querySelector('ul');
const $input2 = document.querySelector('#input2');

$input2.addEventListener('keyup', (e) => {
  if (e.key !== 'Enter') return;

  $newLi = document.createElement('li');
  $newLi.textContent = e.target.value;
  $ul.appendChild($newLi);

  e.target.value = '';
});
```



참고사항

keydown 과 keypress의 차이

* 실행순서는 keydown -> keypress -> keyup 이다.
* keydown은 "물리적인 키 눌림" 에 반응을 한다면, keypress는 "어떤 키가 눌렸는지"에 반응을 한다
  * 따라서, keydown은 shift나 ctrl 키를 눌러도 이벤트로 간주하지만, keypress는 영문자나 한글키를 눌려야 이벤트로 간주한다.
* 출처
  * https://goodteacher.tistory.com/603
  * https://dororongju.tistory.com/91





change 이벤트를 활용해서, 화면에서 (인풋) 요소의 값이 바뀔 때, 이벤트가 변하도록 짤 수 있다.

* 화면상에서, 아무 동작도 하지 않는 버튼을, js코드를 통해서 동작하게끔 할 수 있다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>경주 기록 예제</title>
  <link rel="stylesheet" href="./02.css">
  <script defer src="./02.js"></script>
</head>
<body>

  <h1>달리기 경주 기록</h1>

  <select id="school">
    <option value="">전체 학교</option>
    <option value="근성">근성대</option>
    <option value="복근">복근대</option>
    <option value="박력">박력대</option>
  </select>

  <input type="number" id="grade" value="1" min="1" max="4">
  <label for="sort">학년 이상</label>

  <input type="checkbox" id="sort">
  <label for="sort">기록순 정렬</label>

  <table>
    <thead>
      <th>번호</th>
      <th>학교</th>
      <th>학년</th>
      <th>이름</th>
      <th>기록</th>
    </thead>
    <tbody id="raceTbody">
    </tbody>
  </table>
  
</body>
</html>
```

```javascript
//02.js

let raceData;
getRaceData();

async function getRaceData () {
  const SERVER_URL = 'https://showcases.yalco.kr/javascript/mockserver/';

  // 경주 기록 받기
  const raceResult = await fetch(SERVER_URL + 'race-result')
  .then(result => result.json());
  console.log('1.', raceResult);

  const runners = [];
  const runnerIdxs = raceResult
  .map(itm => itm['runner_idx']);

  // 기록상 주자 번호에 따라 주자들의 정보 받기
  for (const runnerIdx of runnerIdxs) {
    const runner = await fetch(`${SERVER_URL}runners/${runnerIdx}`)
    .then(result => result.json())
    runners.push(runner);
  }
  console.log('2.', runners);

  // 주자들의 학교 번호 중 중복을 거른 뒤 이에 따라 학교 정보 받기
  const schools = [];
  const schoolIdxs = [
    ...new Set(
      runners.map(itm => itm['school_idx'])
    )
  ];
  for (const schoolIdx of schoolIdxs) {
    const school = await fetch(`${SERVER_URL}schools/${schoolIdx}`)
    .then(result => result.json())
    schools.push(school);
  }
  console.log('3.', schools);

  // 세 배열의 객체들을 조인
  raceData = raceResult
  .map(result => {
    const runner = {
      ...runners
      .find(({idx}) => idx === result.runner_idx)
    }

    runner.school = schools
    .find(({idx}) => idx === runner.school_idx)
    .name

    delete runner.school_idx;
    delete runner.idx;

    return {
      ...result,
      ...runner
    }
  });
  console.log('4.', raceData);

  fillRaceTable();
}

function fillRaceTable () {

  // 배열 복사
  let data = [...raceData];

  const _school = document.querySelector('#school').value;
  const _grade = document.querySelector('#grade').value;
  const _sort = document.querySelector('#sort').checked;

  // 인풋 요소의 값들에 따라 필터링 또는 정렬
  if (_school) data = data.filter(({school}) => school.startsWith(_school));
  if (_grade) data = data.filter(({grade}) => grade >= _grade);
  if (_sort) data.sort((a, b) => a.record - b.record);

  // 먼저 tbody 부분을 비움
  const $tbody = document.querySelector('#raceTbody');
  while ($tbody.firstChild) {
    $tbody.removeChild($tbody.firstChild);
  }

  // tbody 채워넣기
  data.forEach(datum => {
    const $newTr = document.createElement('tr');

    ['runner_idx', 'school', 'grade', 'name', 'record']
    .forEach(itm => {
      const $newTd = document.createElement('td');
      $newTd.textContent = datum[itm];
      $newTr.appendChild($newTd);
    });
    $tbody.appendChild($newTr);
  });
}

```



참고할 만한 사항

* 스프레드 문법 적용 시, 아래와 같이 맨 나중의 결과물을 스프레드한다.

```javascript
raceData = raceResult
  .map(result => {
    const runner = {
      ...runners
      .find({idx}) =>( idx === result.runner_idx)
    }
    //...(runners.find({idx} => (idx === result.runner_idx))) 와 동일하다.

    runner.school = schools
    .find(({idx}) => idx === runner.school_idx)
    .name

    delete runner.school_idx;
    delete runner.idx;

    return {
      ...result,
      ...runner
    }
  });
```





기타

* 자바스크립트는 기본적으로 싱글 스레드로 동작하는 것이 원칙이다.

  * 따라서, 일반적으로 비동기적으로 코드를 짜더라도, 동기적인 코드에 비해 실행순서만 차이가 있고 실행 시간에는 큰 차이가 없다.

    => 사실상 싱글 스레드로 운용된다고 볼 수 있다.

  * 그러나, 비동기로 실행되는 함수 중, Web API를 활용하는 함수(fetch 등)의 경우는, 실행 순서 뿐 아니라 실행 시간에도 큰 차이가 있다.

    => fetch 함수의 경우에는, 백그라운드에서 네트워크 통신이 이루어지며, 이와 동시에 메인 스레드는 다른 코드를 처리하기 때문이다.

    => 따라서, Web API를 활용하는 함수의 경우, 멀티 스레드로 동작한다고 말할 수 있다.

