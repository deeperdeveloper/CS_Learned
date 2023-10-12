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
