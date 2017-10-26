---
title : JavaScript 시작하기
description : w3schools를 토대로 빠르게 JavaScript를 학습할 수 있게 글을 구성한다.
date : 2017-10-26
categories :
- JavaScript
tags :
- JavaScript
- w3schools
---

> w3schools의 Tutorial들을 기반으로 개인적인 기식을 부합시켜 이해하기 쉽게 설명합니다.

# JavaScript 소개
웹 개발의 3가지 주요 언어(HTML, CSS, JavaScript) 중 JavaScript에 대한 기본 사용에 대한 정리이다.

JavaScript는 HTML을 수정할 수 있다.
```JavaScript
document.getElementById("id").innerHTML = "Say Hi";
```
- html의 특정 **id** 를 가진 컨텐츠를 수정한다.

JavaScript는 CSS를 수정할 수 있다.
```JavaScript
document.getElementById("id").style.display = "none";
```
- 특정 컨텐츠의 CSS에 포함된 display 값을 변경한다.
- ""와 ''는 같은 용도로 사용된다.

# 이걸 어디에 넣을까?
HTML 상에서 JavaScript가 실행되려면 꼭 <script></script> 태그 안에 코드를 구성해야 한다.
```JavaScript
<script>
document.getElementById("demo").innerHTML = "My First JavaScript";
</script>
```

위 처럼 특정 동작을 수행하는 JavaScript코드를 보통 함수(Function)으로 구성하여 HTML 내의 event가 호출될 때 동작하게 하는 것이 일반적이다.

이것들은 <head> 혹은 <body> 태그 안에 들어 갈 수도 있다.

<head> 안의 사용 예는 다음과 같다.

{% highlight ruby linenos %}
<!DOCTYPE html>
<html>
<head>
<script>
function myFunction() {
    document.getElementById("demo").innerHTML = "Paragraph changed.";
}
</script>
</head>

<body>

<h1>A Web Page</h1>
<p id="demo">A Paragraph</p>
<button type="button" onclick="myFunction()">Try it</button>

</body>
</html>
{% endhighlight %}

- Try it 버튼을 누르면 myFunction()이 수행되며 **demo** 란 컨텐츠 id를 가진 것의 값을 바꿔준다.

위와 같은 방법으로 <body> 역시 구성이 가능하다.
하지만 간단하고 그렇기에 관리가 편한 코드라면 상관 없겠지만 반대의 경우라면 갈 수록 코드의 유지보수가 힘들어 질 것이다.
그렇기에 대부분의 개발자들은 해당 기능과 관련된 javascript 코드를 파일 단위로 나눠 관리한다.

HTML과 같은 폴더 내에 myScript.js 파일이 있고 내용이 다음과 같은 상태에서
```JavaScript
function myFunction() {
   document.getElementById("demo").innerHTML = "Paragraph changed.";
}
```

다음과 같은 호출을 통해 script를 사용할 수 있다.
{% highlight ruby linenos %}

<!DOCTYPE html>
<html>
<body>
<p id="demo">A Paragraph.</p>

<button type="button" onclick="myFunction()">Try it</button>

<script src="myScript.js"></script>

</body>
</html>
{% endhighlight %}

좋다, 다 좋은데 알아둬야할 사항이 있다. 바로 src의 경로!
- 외부에서 js파일을 불러올 수도 있다! omg
- 특정 폴더를 기준으로 찾아야할 수도 있다.
```JavaScript
<script src="/js/myScript1.js"></script>
```
- 현재 폴더 내의 js파일이라면 그냥 파일명만 입력하면 된다.
