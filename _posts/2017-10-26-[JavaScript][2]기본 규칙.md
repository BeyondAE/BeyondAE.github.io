---
title : JavaScript 기본 규칙
description : w3schools를 토대로 빠르게 JavaScript를 학습할 수 있게 글을 구성한다.
date : 2017-10-26
categories :
- JavaScript
tags :
- JavaScript
- w3schools
---

> w3schools의 Tutorial들을 기반으로 개인적인 기식을 부합시켜 이해하기 쉽게 설명합니다.

# JavaScript로 출력해보자.
C를 해본 사람들은 hello word를 다들 한 번씩 찍어볼 것이다. 어떻게?
```c
printf("Hello word");
```
끝, 근데 프로그래밍에서 이런 출력은 무지막지하게 중요하다.
>사족을 들여 좀 더 설명하자면 세상의 모든 시스템은 입력과 출력으로 이뤄져 있다.
(예를 들어 햄버거 가계 주문 시스템은 손님의 주문 내역과 돈을 입력으로 받아 출력으로 주문에 맞는 음식을 내주는 것이다.)
우리가 여러 언어들을 공부하고 난리부리면서 신박한 로직과 알고리즘을 찾는 것도 결국 다 출력하기 위한 것이란 말이다.

JavaScript에서 출력은 어떻게 돼 있을까?
> - 앞 단원에서 본 innerHTML
> -  document.write()
> - window.alert()
> - console.log()

innerHTML은 요렇게~ 소개 단원에서 설명 드렸죠?
```JavaScript
<script>
document.getElementById("demo").innerHTML = 5 + 6;
</script>
```
document.write()는 바로 해당 단락에 '쓰기'를 수행하는 함수에요.
```JavaScript
document.write(5 + 6);
```
window.alert()는 window에 알림창을 띄우는 함수에요. 여기서 window는 브라우저겠죠?
>  window는 "창, 창문"의 의미가 있죠. View라는 의미도 있지만, OS상에 깔려있는 프로그램들을 말해요.

```JavaScript
window.alert(1+1);
```
console.log()는 IDE나 개발자 모드에서 console창으로 확인이 가능해요.
> console은 "제어판, 계기판"등의 의미가 있어요. OS 및 프로그램을 제어하기 위해 Console창을 많이들 사용하죠? 맞아요, 그 검은 창이요. 그것에  log 즉 지정한 형태의 출력을 하겠다는 거에요.

```JavaScript
console.log(5 + 6);
```

# Syntax
기본적으로 사용되는 문법은 모든 언어에서 기본적으로 숙지해야 하는 사항이다. 기존 특정 언어 하나쯤 익혔다면 JavaScript 역시 쉽게 접근이 가능하다.

## 변수 선언
```JavaScript
var x, y, z;
x = 5;
y = 6;
z = x + y;
```
- 모든 변수에 대한 선언은 var 키워드로 진행한다.
  - var는 type에 관계없이 값을 받아 초기화 시에 Type이 결정 됩니다.
- =는 operator로 값을 초기화 한다.
- 각 구문의 상태 구분은 semicolon으로 진행한다.

## 용례

### statement
Statement는 작업 명령이다. 앞서 보여진 것으로 예를 들자면
var x; 는 **'x 변수를 선언해'** 라는 statement 즉 작업 명령이다.

### Literal
Literal은 초기화 등에 사용되는 **'고정 값'** 을 말한다.
var x = 10; 일 때, 10은 Literal이지만 x는 그렇지 않다.

### operator
+,-, x , /, = 등 기본적으로 사용되는 연산자를 말 합니다.

### Expression
값, 변수, 연산자 등을 조합해서 작업 명령을 하고, 우리는 특정 출력을 도출하잖아요?
예를 들어 다음과 같은 작업 명령이 있어요
```JavaScript
var foo = 10;
5 * 10 + foo
```
결과 값은 60이죠? 아, 이걸 말 하려는 게 아니라 5 * 10 + foo 라는 구성을 우리는 표현식이라 말 합니다.

### Comments
주석을 말 합니다.

### 이름 식별자
우리는 변수를 사용하죠. 변수는 되도록이면 각자가 구분이 가능하게 다른 이름을 가지게 합니다. 이 변수 이름을 결정할 때 사용되는 규칙이 이름 식별자 입니다.
간단해요. 첫 문자는 문자, _ , $가 가능하대요. 그러나 숫자는 안 된대요.
```JavaScript
var _hahahaha // ok
var 2hahahahaha // noup
```

#### 카멜 케이스
이름 식별자와 연관 있어요. 우리가 되도록이면 각 변수가 명확히 구분되로록 네이밍을 해야 함을 알고 있어요. 이렇다 보니 네이밍된 이름은 여러 단어의 조합일 수 밖에 없죠.
예를 들어 홈페이지 방문 횟수에 대한 변수를 네이밍 해야한다고 하죠.
```JavaScript
var countofvisitinghomepage;
```
어때요 어지럽죠?그래서 사용되는 것이 **네이밍 표기법** 들인데요. 그 중 많이 사용하는 것이 **카멜 표기법** 입니다. camel case라고도 해요. 한 번 적용해보죠.
```JavaScript
var CountOfVisitingHomepage;
```
어때요 훨씬 구분하기 쉽죠? 웹에선 카멜 케이스 말고도 Underscore 표기법을 쓰기도 해요
```JavaScript
var Count_Visiting_Homepage;
```
이것도 좋죠? 무엇을 쓸지는 여러분의 결정이에요. 그냥 **코딩 스타일** 이죠.
이 표기법들을 사람들은 코딩스타일이라고 부르기도 한답니다.

### charter set
기본적으로 Unicode를 사용합니다. 케릭터 셋에 대한 설명은 다른 포스팅을 통해 설명하도록 할께요. 일단 더 공부하고 싶다면 [이곳](https://www.w3schools.com/charsets/ref_html_utf8.asp)을 참고하세요.

# Statement에 대한 팁
```JavaScript
var person = "Hege";
var person="Hege";
```
위 두 작업 명령 중 위에 것이 더 가독성이 좋다고 하네요.

```JavaScript
document.getElementById("demo").innerHTML =
"Hello Dolly!";
```
JavaScript는 한 라인에 80개의 문자가 있는 것을 피하라고 해요. 보기가 너무 힘들 거든요. 그래서 필요하다면 위와 같이 라인을 내릴 수도 있습니다.

# Keyword
Keyword |	Description
--- | ---
break |	Terminates a switch or a loop
continue | Jumps out of a loop and starts at the top
debugger	| Stops the execution of JavaScript, and calls (if available) the debugging function
do ... while |	Executes a block of statements, and repeats the block, while a condition is true
for |	Marks a block of statements to be executed, as long as a condition is true
function |	Declares a function
if ... else |	Marks a block of statements to be executed, depending on a condition
return |	Exits a function
switch |	Marks a block of statements to be executed, depending on different cases
try ... catch |	Implements error handling to a block of statements
var |	Declares a variable

# 주석
```JavaScript
/*
The code below will change
the heading with id = "myH"
and the paragraph with id = "myP"
in my web page:
*/
// Change heading:
document.getElementById("myH").innerHTML = "My First Page";
```
단일/멀티 라인 주석을 위 처럼 써요.
