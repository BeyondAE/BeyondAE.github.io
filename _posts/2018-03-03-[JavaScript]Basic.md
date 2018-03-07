---
title : JavaScript 정리
description : 그냥 다시 써보면서 기입
date : 2018-03-06
categories :
- Web
- JavaScript
tags :
- JavaScript
---

# rule

## HTML element는 Script 전에 나열돼야 한다.
```JavaScript
<p id="demo"></p>
<script>
    document.getElementById("demo").innerHTML="First";
</script>
```
innerHTML을 바꿈으로써 HTML element를 변경할 수 있다.

## 스크립트는 ***< head > or < body >*** 에 명시할 수 있다.

## 외부에서 스크립트를 명시해도 된다.

```JavaScript
<p id="demo">A Paragraph.</p>

<button type="button" onclick="myFunction()">Try it</button>

<p>(myFunction is stored in an external file called "myScript.js")</p>

<script src="myScript.js"></script>
```
외부 스크립트의 장점은 다음과 같다.
- HTML 코드와 분리가 된다.
- 명확히 구분됨으로 유지보수에 좋다.
- 별도 파일로 구분될 시 page 로딩 속도가 빨라진다.

### 외부에서 불러오기2
```JavaScript
<p id="demo">aaaa</p>
<button type="button" onclick="myFunction()"> Click me </button>
<p>(called external file)</p>
<script src="https://www.w3schools.com/js/myScript.js"></script>
```

## Semicolons
```JavaScript
var a, b, c;     // Declare 3 variables
a = 5;           // Assign the value 5 to a
b = 6           // Assign the value 6 to b
c = a + b;       // Assign the sum of a and b to c
```
위 처럼 행변환이 된 경우, 세미콜론은 안 붙여도 무방하다.

> a = 5; b = 6; c = a + b;

하지만 위 처럼 한 줄에 구분된 경우, 실행 단위 구분을 위해 세미콜론이 필요하다.

## 공백
```JavaScript
var person = "Hege";
var person="Hege";

var x = y    +    z;
```
위와 같이 공백이 들어가도 된다. 공백을 붙인다면 가독성에 이점있는 코드를 남길 수 있다.

## 행 바꿈
기본적으로 한 라인에 80자가 넘어간다면 행 바꿈을 하는 것을 권고한다.

## 문자열
문자열은 ""나 ''로 묶어도 된다.







---
# 출력
출력은 다음과 같이 가능하다.
- innerHTML을 사용해 HTML element를 변경한다.
- document.write()를 통해
- windows.alert()를 통해 알림창을 띄운다.
- console.log()를 통해 브라우저 콘솔에 출력.

## innerHTML
```JavaScript
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = 5 + 6;
</script>
```
## document.write()
```JavaScript
<script>
document.write(5 + 1313);
</script>
```
해당 스크립트 위치에 element를 생성하고 그곳에 바로 출력을한다.

## window.alert()
```JavaScript
<script>
window.alert(5 + 6);
</script>
```

## console.log()
```JavaScript
<script>
console.log(5 + 6);
</script>
```

---
# Type
데이터 타입에는 다음과 같은 종류가 있다.
```JavaScript
var length = 16;                               // Number
var lastName = "Johnson";                      // String
var x = {firstName:"John", lastName:"Doe"};    // Object
```

서로 다른 데이터 타입을 조합하면 어떻게 될까?
```JavaScript
<script>
var x = 16 + "Volvo";
document.getElementById("demo").innerHTML = x;
</script>
```
> 16Volvo

var x = 16 + 4 + "Volvo"; 이면
> 20Volvo

var x = "Volvo" + 16 + 4; 이면
> Volvo164

연산이 왼쪽에서 오른쪽으로 시작되는 것을 알 수 있다.


# 함수
```JavaScript
function toCelsius(fahrenheit) {
    return (5/9) * (fahrenheit-32);
}
document.getElementById("demo").innerHTML = toCelsius(77);
```
> 25

하지만 다음과 같으면 어떤 결과가 나올까?
```JavaScript
<script>
function toCelsius(f) {
    return (5/9) * (f-32);
}
document.getElementById("demo").innerHTML = toCelsius;
</script>
```
> function toCelsius(f) { return (5/9) * (f-32); }

놀랍게도 error가 아닌, 함수 정의를 리턴해 버린다.

# 오브젝트

```JavaScript
<script>
var person = {
    firstName: "John",
    lastName : "Doe",
    id       :  5566
};
document.getElementById("demo").innerHTML =
person.firstName + " " + person.lastName;
</script>
```
person은 오브젝트이며 오브젝트는 ***속성:속성값*** 의 나열로 구성될 수 있다.

오브젝트 속성값에 접근하는 방법은 다음과 같이 2가지가 있다.
>person.lastName;
person["lastName"];

그리고 오브젝트 내의 속성값으로 함수를 둘 수가 있다.
```JavaScript
<script>
var person = {
    firstName: "John",
    lastName : "Doe",
    id       : 5566,
    fullName : function() {
       return this.firstName + " " + this.lastName;
    }
};

document.getElementById("demo").innerHTML = person.fullName();
</script>
```

오브젝트는 위와 같이 객체를 두고 객체의 속성을 구성한다.

코드를 구성하면서 중요한 부분은

String, Number, Boolean 등의 일반 타입은 오브젝트로 구성하지 말한 것이다.
```JavaScript
var x = new String();        // Declares x as a String object
var y = new Number();        // Declares y as a Number object
var z = new Boolean();       // Declares z as a Boolean object
```
일반 타입을 오브젝트로 할당하면 이것들이 무의미 하게 메모리를 더 쓰게 되며 실행속도 역시 낮추게 한다.

# Scope
자바스크립트는 2가지 Scope이 존재한다.
- Local scope
- Global scope

영역의 구분은 다음과 같다.
```JavaScript
var globalCarName = "Volvo";
myFunction();

function myFunction() {
  var localCarName = "Volvo";
    document.getElementById("demo").innerHTML =
    "I can display " + globalCarName;
}
```
간단한 규칙이다.

하지만 몇 가지 알아둬야 할 사항이 있다.
```JavaScript
myFunction();

function myFunction() {
    carName = "Volvo";
}
```
위 처럼 선언하지 않은 변수가 할당되면, 이것은 ***Global Scope*** 를 가진다.

다음, HTML의 전역은 window이며, 모든 전역은 window 객체 안에 속하게 된다.

```JavaScript
<p id="demo"></p>

<script>
var carName = "Volvo";

// code here can use window.carName
document.getElementById("demo").innerHTML = "I can display " + window.carName;
</script>
```
window 객체에 접근하여 전역 변수에 접근하는 것을 볼 수 있다.
이렇다 보니 우리는 전역 변수를 사용하는 것을 지양해야 한다.

> 사용자가 선언한 전역 변수가 기존 전역 변수를 덮을 수 있기에 전역 변수 사용을 최소화 한다.

## Lifetime
지역 변수는 함수가 끝나면 사라지지만, 전역 변수는 브라우저 윈도우(tab)를 종료할 때 소멸된다. 하지만 같은 윈도우 내에서 불러진 page에서는 전역 변수가 살아있다.


# 이벤트
HTML은 HTML element에 자바스크립트 코드를 추가할 수 있게 한다. 다음은 element의 이벤트 속성에 자바스크립트 코드를 넣는 예시 이다.
```JavaScript
<element event='some JavaScript'>
<element event="some JavaScript">
<button onclick="displayDate()">The time is</button>
```
싱글/더블 쿼트의 구분이 상관 없다.

## 일반적인 HTML 이벤트
- onchange
- onclick
- onmouseover
- onmouseout
- onkeydown
- onload
- [more HTML dome events](https://www.w3schools.com/jsref/dom_obj_event.asp)

이런 HTML 이벤트 속성들은 자바스크립트 코드를 직접 실행한다.  그래서 이벤트에 고유한 이벤트를 할당할 수도, 그래서 이벤트를 막을 수도 있다.

# 문자열
싱글/더블 쿼트에 대한 구분이 없다.
```JavaScript
<script>

var answer1 = "It's alright";
var answer2 = "He is called 'Johnny'";
var answer3 = 'He is called "Johnny"';

document.getElementById("demo").innerHTML =
answer1 + "<br>" + answer2 + "<br>" + answer3;

</script>
```

> var x = "We are the so-called "Vikings" from the north.";

위와 같이 더블쿼드 안에 더블쿼트가 필요하다면, 다음과 같이 사용하면 된다.

> var x = "We are the so-called \"Vikings\" from the north.";

문자열 내부에서 백슬래시가 쓰고 싶다면 백슬래시 두 번을 통해 사용이 가능하다.

> var x = "The character \\ is called backslash.";

만약 코드 중 문자열이 길어 라인을 넘겨야 하는 경우가 있다면 다음과 같이 해결이 가능하다.

```JavaScript
document.getElementById("demo").innerHTML = "Hello \
Dolly!";

document.getElementById("demo").innerHTML = "Hello " +
"Dolly!";
```

string은 오브젝트 형이 가능합니다.
```JavaScript
<script>
var x = "John";              // x is a string
var y = new String("John");  // y is an object
document.getElementById("demo").innerHTML = (x===y);
</script>
```
> false

new 키워드를 통해 오브젝트가 되면 문자열과는 다른 형이 됩니다.

### 문자열 메소드
문자열을 다루기 위해 기본적으로 제공되는 메소드들이 존재한다.
```JavaScript
var txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
var sln = txt.length; //길이

var str = "Please locate where 'locate' occurs!";
// 첫 번째 발생하는 위치 찾기
var pos = str.indexOf("locate");// 출력 : 7
//마지막에 발생하는 위치 찾기
pos = str.lastIndexOf("locate");//21
//검색 시작위치 지정 후 첫 번째 발생 위치 찾기
pos = str.indexOf("locate",15);//21

// 문자열에서 문자열 찾기
pos = str.search("locate");//7


var str = "Apple, Banana, Kiwi";
// 7~13 사이 추출해 리턴, 원형은 그대로임
var res = str.slice(7, 13);//Banana
// 끝에서 부터 검색
res = str.slice(-12, -6);//Banana
//7자리 이후 다 추출
res = str.slice(7); //Banana, Kiwi
// 뒤에서 12자리 이후 다 추춯
res = str.slice(-12)//Banana, Kiwi

//slice와 흡사하지만 음수 인덱스 사용이 불가능하다는 다른점이 있다.
res = str.substring(7, 13);//Banana

//slice와 흡사하지만, 2번째 인자가 길이를 말한다는 다른 점이 있다.
res = str.substr(7, 6);//Banana


str = "Please visit Microsoft!";
//문자열 교환
var n = str.replace("Microsoft", "W3Schools");

n = str.replace("MICROSOFT", "W3Schools");  // Microsoft는 MICROSOFT와 다른 문자

n = str.replace(/MICROSOFT/i, "W3Schools");// 대소문자 구분을 안 하려면 정규화를 쓰자

var text1 = "Hello World!";       // String
var text2 = text1.toUpperCase();  // 모두 대문자로!
text2 = text1.toLowerCase();// 모두 소문자로!

var text1 = "Hello";
var text2 = "World!";
var text3 = text1.concat(" ",text2);//두 문자열 붙이기!

var text = "Hello" + " " + "World!";// 그냥 +연산자로 붙여도 됨
var text = "Hello".concat(" ", "World!");

var str = "HELLO WORLD";
str.charAt(0);            // returns H
str.charCodeAt(0);         // returns 72(H의 유니코드 인덱스)
var str1 = str[0]; // IE5, IE6, IE7에서 동작안함,
// str[0] = "H"는 동작 안 함.

var txt = "a,b, c, d,e,f";   // String
var txt1 = txt.split(",");          // 콤마 구분으로 자르기, a가 뽑힌다.
txt1 = txt.split(" ");          //  공백 구분, 'a,b,' 가 뽑힌다.
txt1 = txt.split("|");          // 바 구분이 아니기에 "a,b, c, d,e,f" 모두 출력
txt1 = txt.split("");  //구분이 없다면 단일문자 반환
```

# 숫자
다양한 숫자 연산도 가능하다.
```JavaScript
var x = 123e5;    // 12300000
var y = 123e-5;   // 0.00123

//정수는15자리까지 정확하다.
var x = 999999999999999;   // x will be 999999999999999
var y = 9999999999999999;  // y will be 10000000000000000

//십진법은 17자리가 한계지만 소숫점은 항상 100% 정확한 건 아니다.
var x = 0.2 + 0.1;         // x will be 0.30000000000000004
```

## +연산자
+연산자로 숫자와 문자열 연결이 가능하다.
```JavaScript
var x = 10;
var y = "20";
var z = x + y;           // z will be 1020 (a string)

var x = 10;
var y = 20;
var z = "The result is: " + x + y; // The result is:1020

var x = 10;
var y = 20;
var z = "30";
var result = x + y + z;//3030
```

## 숫자 문자열
자바스크립트는 숫자문자열 연산에 대해 문자열을 숫자로 변환하려 한다.
```JavaScript
var x = "100";
var y = "10";
var z = x / y;       // z will be 10

var x = "100";
var y = "10";
var z = x * y;       // z will be 1000

var x = "100";
var y = "10";
var z = x - y;       // z will be 90

var x = "100";
var y = "10";
var z = x + y;       // z will not be 110 (It will be 10010), 덧셈은 좀 다르죠?
```
## NaN
NaN은 숫자가 유효한 숫자가 아님을 나타내는 JavaScript 예약어입니다.
```JavaScript
var x = 100 / "Apple";  // x will be NaN (Not a Number)

var x = 100 / "10";     // x will be 10

var x = 100 / "Apple";
isNaN(x);               // returns true, because x is Not a Number

var x = NaN;
var y = 5;
var z = x + y;         // z will be NaN

var x = NaN;
var y = "5";
var z = x + y;         // z will be NaN5

typeof NaN;            // "number", NaN은 숫자다!
```

## Infinity 예약어
Infinity (또는 -Infinity)는 가능한 가장 큰 숫자 이외의 숫자를 계산할 때 JavaScript가 반환하는 값입니다.

```JavaScript
var myNumber = 2;
while (myNumber != Infinity) {          // Execute until Infinity
    myNumber = myNumber * myNumber;
}
```
> 출력:
4
16
256
65536
4294967296
18446744073709552000
3.402823669209385e+38
1.157920892373162e+77
1.3407807929942597e+154
Infinity

```JavaScript
var x =  2 / 0;          // x will be Infinity
var y = -2 / 0;          // y will be -Infinity

typeof Infinity;        // returns "number"
```

## 16진수
16진수를 0과함께 쓰지마세요. 07로 하면 8진수로 인식합니다.

```JavaScript
var x = 0xFF;           // x will be 255

//기본적으로 10진수이지만, 다음과 같이 진수 변환 출력이 가능하다.
var myNumber = 128;
document.getElementById("demo").innerHTML = "128 = " +
myNumber + " Decimal, " +
myNumber.toString(16) + " Hexadecimal, " +
myNumber.toString(8) + " Octal, " +
myNumber.toString(2) + " Binary."
```
## 숫자 메소드
```JavaScript
var x = 123;
x.toString();            // returns 123 from variable x
(123).toString();        // returns 123 from literal 123
(100 + 23).toString();   // returns 123 from expression 100 + 23

//지수표기
var x = 9.656;
x.toExponential(2);     // returns 9.66e+0, 반올림 됐음!
x.toExponential(4);     // returns 9.6560e+0
x.toExponential(6);     // returns 9.656000e+0

// 자릿수 고정
var x = 9.656;
x.toFixed(0);           // returns 10, 반올림 됨
x.toFixed(2);           // returns 9.66, 반올림 됨
x.toFixed(4);           // returns 9.6560
x.toFixed(6);           // returns 9.656000

// 지정된 길이
var x = 9.656;
x.toPrecision();        // returns 9.656
x.toPrecision(2);       // returns 9.7
x.toPrecision(4);       // returns 9.656
x.toPrecision(6);       // returns 9.65600

// 숫자를 숫자로 반환
var x = 123;
x.valueOf();            // returns 123 from variable x
(123).valueOf();        // returns 123 from literal 123
(100 + 23).valueOf();   // returns 123 from expression 100 + 23
// 모든 타입에는 valueOf과 toString이 있다.

// 숫자로 변환
Number(true);          // returns 1
Number(false);         // returns 0
Number("10");          // returns 10
Number("  10");        // returns 10
Number("10  ");        // returns 10
Number("10 20");       // returns NaN
Number("John");        // returns NaN

Number(new Date("2017-09-30"));    // returns 1506729600000
// 위의 Number () 메서드는 1970.1.1부터의 밀리 초 수를 반환합니다.

// 숫자를 찾아 파싱함, 첫 숫자만 반환됨.
parseInt("10");         // returns 10
parseInt("10.33");      // returns 10
parseInt("10 20 30");   // returns 10
parseInt("10 years");   // returns 10
parseInt("years 10");   // returns NaN

parseFloat("10");        // returns 10
parseFloat("10.33");     // returns 10.33
parseFloat("10 20 30");  // returns 10
parseFloat("10 years");  // returns 10
parseFloat("years 10");  // returns NaN

//숫자 속성
MAX_VALUE	: 자바스크립트에서 가능한 가장 큰 값
MIN_VALUE	: 자바스크립트에서 가능한 가장 작은 값
NEGATIVE_INFINITY	: 음의 무한대, 오버플로에서 사용됨.
NaN	: "Not-a-Number" value
POSITIVE_INFINITY	무한대, 오버플로에서 사용됨.

var x = Number.MAX_VALUE; //1.7976931348623157e+308

var x = 6;
var y = x.MAX_VALUE;    //undefined
```

## 수학 객체
```JavaScript
Math.PI;            // returns 3.141592653589793

// 가장 가까운 정수로 올/내림
Math.round(4.7);    // returns 5
Math.round(4.4);    // returns 4

// 거듭제곱
Math.pow(8, 2);      // returns 64

//  제곱근
Math.sqrt(64);      // returns 8

// 랜덤값
Math.random();              // returns a random number

Math.floor(Math.random() * 10);     // returns a number between 0 and 9

Math.floor(Math.random() * 11);      // returns a number between 0 and 10

Math.floor(Math.random() * 10) + 1;  // returns a number between 1 and 10

Math.floor(Math.random() * 100);     // returns a number between 0 and 99

Math.floor(Math.random() * 101);     // returns a number between 0 and 100

Math.floor(Math.random() * 100) + 1; // returns a number between 1 and 100
```

# 일자
1970.1.1 00:00:00을 기준으로 밀리세컨드 값을 뽑아낸다.
```JavaScript
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML = Date();
</script>
// Tue Mar 06 2018 13:51:37 GMT+0900 (대한민국 표준시)
```

## Date 객체 생성
>new Date()
new Date(milliseconds)
new Date(dateString)
new Date(year, month, day, hours, minutes, seconds, milliseconds)

위와 같은 방법으로 생성이 가능하다.

```JavaScript
<script>
var d = new Date();
document.getElementById("demo").innerHTML = d;
</script>
// Tue Mar 06 2018 13:51:37 GMT+0900 (대한민국 표준시)

<script>
var d = new Date("October 13, 2014 11:13:00");
document.getElementById("demo").innerHTML = d;
</script>


<p>100000000000 milliseconds from Jan 1, 1970, is approximately Mar 3, 1973:</p>
<p id="demo"></p>
<script>
var d = new Date(100000000000);
document.getElementById("demo").innerHTML = d;
</script>
// Sat Mar 03 1973 18:46:40 GMT+0900 (대한민국 표준시)

<script>
var d = new Date(99,5,24,11,33,30,0);
document.getElementById("demo").innerHTML = d;
</script>
// Thu Jun 24 1999 11:33:30 GMT+0900 (대한민국 표준시)

<script>
var d = new Date(99,5,24);
document.getElementById("demo").innerHTML = d;
</script>
// Thu Jun 24 1999 00:00:00 GMT+0900 (대한민국 표준시)

<script>
var d = new Date();
document.getElementById("demo").innerHTML = d.toString();
</script>
// Tue Mar 06 2018 17:06:03 GMT+0900 (대한민국 표준시)

// UTC로 출력
<script>
var d = new Date();
document.getElementById("demo").innerHTML = d.toUTCString();
</script>
// Tue, 06 Mar 2018 08:06:17 GMT

// Date 문자열만 출력
<script>
var d = new Date();
document.getElementById("demo").innerHTML = d.toDateString();
</script>
```
날자를 설정하지 않으면 브라우져 타임을 사용합니다.

## 일자 포맷
>ISO Date :	"2015-03-25" (The International Standard)
Short Date :	"03/25/2015"
Long Date :	"Mar 25 2015" or "25 Mar 2015"
Full Date :	"Wednesday March 25 2015"

ISO date는 자바스크립트 표준이다.

```JavaScript
// ISO date는 시,분,초를 추가할 수 있습니다.
<script>
document.getElementById("demo").innerHTML =
new Date("2015-03-25T12:00:00Z");
// 날짜와 시간은 T로 구분합니다.
// UTC 시간은 Z로 구분합니다.
</script>
```

## 일자 메소드
### Getter
> getDate() :	Get the day as a number (1-31)
getDay() :	Get the weekday as a number (0-6)
getFullYear() :	Get the four digit year (yyyy)
getHours() :	Get the hour (0-23)
getMilliseconds() :	Get the milliseconds (0-999)
getMinutes() :	Get the minutes (0-59)
getMonth() :	Get the month (0-11)
getSeconds() :	Get the seconds (0-59)
getTime()	: Get the time (milliseconds since January 1, 1970)

```JavaScript
// 현재 요일 출력
<script>
var d = new Date();
var days = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];
document.getElementById("demo").innerHTML = days[d.getDay()];
</script>
```
### Setter
>setDate() :	Set the day as a number (1-31)
setFullYear() :	Set the year (optionally month and day)
setHours() :	Set the hour (0-23)
setMilliseconds() :	Set the milliseconds (0-999)
setMinutes() :	Set the minutes (0-59)
setMonth() :	Set the month (0-11)
setSeconds() :	Set the seconds (0-59)
setTime() :	Set the time (milliseconds since January 1, 1970)

```JavaScript
<script>
var d = new Date();
d.setFullYear(2020, 0, 14);
document.getElementById("demo").innerHTML = d;
</script>
// Tue Jan 14 2020 17:19:04 GMT+0900 (대한민국 표준시)

<script>
var d = new Date();
d.setDate(d.getDate() + 50);
document.getElementById("demo").innerHTML = d;
</script>
// Wed Apr 25 2018 17:19:34 GMT+0900 (대한민국 표준시)
// 현재일 : Tue Mar 06 2018 17:19:58 GMT+0900 (대한민국 표준시)
```

### others
```JavaScript
// 유효문자열 존재할 시, 1970.1.1부터 현재까지 밀리세컨드
<script>
var msec = Date.parse("March 21, 2012");
document.getElementById("demo").innerHTML = msec;
</script>
//1332255600000
```
표준시간을 얻는 함수는 다음과 같다.
>getUTCDate() :	Same as getDate(), but returns the UTC date
getUTCDay() :	Same as getDay(), but returns the UTC day
getUTCFullYear() :	Same as getFullYear(), but returns the UTC year
getUTCHours() :	Same as getHours(), but returns the UTC hour
getUTCMilliseconds() :	Same as getMilliseconds(), but returns the UTC milliseconds
getUTCMinutes() :	Same as getMinutes(), but returns the UTC minutes
getUTCMonth() :	Same as getMonth(), but returns the UTC month
getUTCSeconds() :	Same as getSeconds(), but returns the UTC seconds


# 배열
```JavaScript
//생성
var animal = []; //good
var cars = ["Saab", "Volvo", "BMW"]; //good
var cars = new Array("Saab", "Volvo", "BMW"); // 위의 것과 완벽히 동일하다. new연산자 사용은 피하자.
var points = new Array(40, 100); // 40과 100의 element를 가진 배열 객체 생성!
var points = new Array(40); // 40개의 element를 가진 배열 생성!
// new는 혼동을 주니 사용을 피하자.


//접근
document.getElementById("demo").innerHTML = cars;
//Saab,Volvo,BMW
document.getElementById("demo").innerHTML = cars[0];
//Saab

// 루프
var fruits, text, fLen, i;

fruits = ["Banana", "Orange", "Apple", "Mango"];
fLen = fruits.length;
text = "<ul>";
for (i = 0; i < fLen; i++) {
    text += "<li>" + fruits[i] + "</li>";
}
```

자바스크립트의 배열은 특별한 오브젝트 타입이다. 실제 typeof을 통해 확인이 가능하다.
배열은 오브젝트 타입이기에  오브젝트나 함수 등을 가질 수 있다.

```JavaScript
// 요소 추가
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[fruits.length] = "Lemon";     // adds a new element (Lemon) to fruits

// 요소 추가2
<script>
var fruits, text, fLen, i;
fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits[6] = "Lemon";// 6번 요소에 값 추가

fLen = fruits.length;
text = "";
for (i = 0; i < fLen; i++) {
    text += fruits[i] + "<br>";
}
document.getElementById("demo").innerHTML = text;
</script>
/*Banana
Orange
Apple
Mango
undefined    //구멍이 생겼다....
undefined
Lemon*/
```

배열은 숫자로된 인덱스를 가진다.
명명화된 인덱스를 가지게 되면 ***표준 오브젝트*** 가 되며 잘 못된 결과를 가져올 수 있다.
```JavaScript
var person = [];
person[0] = "John";
person[1] = "Doe";
person[2] = 46;
var x = person.length;         // person.length will return 3
var y = person[0];             // person[0] will return "John"

var person = [];
person["firstName"] = "John";
person["lastName"] = "Doe";
person["age"] = 46;
var x = person.length;         // person.length will return 0
var y = person[0];             // person[0] will return undefined

// 배열과 오프젝트... 좀 햇갈릴 여지가 있다.
//배열 확인 방법
var fruits = ["Banana", "Orange", "Apple", "Mango"];
typeof fruits;             // returns object

Array.isArray(fruits);     // returns true

fruits instanceof Array     // returns true
```

## 배열 함수
```JavaScript
<script>
var fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo").innerHTML = fruits.toString();
</script>
// Banana,Orange,Apple,Mango

document.getElementById("demo").innerHTML = fruits;
// Banana,Orange,Apple,Mango

// 구분자를 바꿔 불러올 수 있다.
document.getElementById("demo").innerHTML = fruits.join(" * ");
// Banana * Orange * Apple * Mango

//요소 제거
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.pop();              // Removes the last element ("Mango") from fruits
//Banana,Orange,Apple
fruits.push("Kiwi");
//Banana,Orange,Apple,Kiwi
var banana = fruits.shift();
// Banana
//fruits는 Orange,Apple,Kiwi
fruits.unshift("Lemon");  // return 4(배열 길이)
//Lemon,Orange,Apple,Kiwi
```
