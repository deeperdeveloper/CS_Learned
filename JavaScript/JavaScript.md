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
