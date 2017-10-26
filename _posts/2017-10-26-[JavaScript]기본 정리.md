---
title : GCP 시작하기
description : CP100 GCP시작
date : 2017-10-25
categories :
- JavaScript
tags :
- JavaScript
- w3schools
---

> w3schools의 Tutorial을 정리한다.

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

```html
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
```
