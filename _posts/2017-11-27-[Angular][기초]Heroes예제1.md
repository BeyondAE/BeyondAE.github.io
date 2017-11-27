---
title : Heroes 예제1
description : Heroes 예제1
date : 2017-11-27
categories :
- Angular
tags :
- Angular
---

# 환경구성

# 프로젝트 생성
> angular-cli를 통한 기본 프로젝트 생성

# 프로젝트 기본 구성

# 따라하기

## app.component.ts
기존 코드를 날려버리고 다음과 같은 코드를 친다.

```TypeScript
import {Component} from '@angular/core'; ///< @angular/core package에서 Component객체를 가져옵니다

export class Hero { ///<  export는 이 class를 다른 파일에서 가져갈(import) 수 있음을 나타냅니다.
  id: number; ///<  :(콜론)이후에 타입을 지정할 수도 있다.
  name: string;
}

@Component({  ///<  컴포넌트 @(데코레이터)를 구성합니다.
  ///<  @angular/core package의Component 객체가 decorator의 역할을 할 수 있게 합니다.
  selector: 'my-app', ///<   html 코드에서 해당 component를 호출할때 사용되는 이름
  template: `
  <h1>{{title}}</h1>
  <h2>{{hero.name}} details!!!!</h2>
  <div><label>id: </label>{{hero.id}}</div>
  <div>
    <label>name: </label>
    <input [(ngModel)]="hero.name" placeholder="name">
  </div>
  ` ///<  template 항목은 해당 component의 html 코드를 문자열로 가집니다.
  ///<  ES2015부터 ``사이의 문자열은 줄바꿈까지 포함합니다.
})
export class AppComponent { ///<  component decorator가 붙어있는 AppComponent class
  ///<   Angular에서 Component들은 class이름끝에 Component를 붙이도록 약속(convention)이 되어있다.
  title = 'Tour of Heroes'; ///<  type을 뺄 수도 있다. but 원치 않는 오타나, 타입의 값이 들어간 경우 오류를 못잡는다.
  hero: Hero = {  ///<  역시 type이 없다면, id를 ID로 했을 시 오류를 못잡는다.
    id: 1,
    name: 'Winstorm'
  };
}
```
주석은 그냥 설명이니 제외해도 무방하다.
### HTML 템플릿 코드
1. {{변수}}를 통해 component class에 정의된 변수값을 가져올 수 있습니다.
2. [(ngModel)]="변수"로 바인딩이 가능해진다.
- hero.name에서 값을 가져와 보여주고
- input에서 수정 시, hero.name의 값이 변경된다!

##app.module.ts
```TypeScript
// src/app/app.module.ts

///<  @angular는 그냥 package이름 입니다.
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule }   from '@angular/forms';
///<   NgModule, BrowserModule, FormsModule 객체를 각각의 package에서 가져오고 있습니다.
import { AppComponent }  from './app.component';
///<  위에서 만든 AppComponent를 불러옵니다. 다른 파일에서 불러오기에 상대주소로 파일 위치를 입력합니다.

@NgModule({ //3
  imports: [  ///<  Module은 요기에!
    BrowserModule,
    FormsModule // <-- import the FormsModule before binding with [(ngModel)]
  ],
  declarations: [ ///<  Component는 요기에!
    AppComponent
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

## index.html
```HTML
<!DOCTYPE html>
<html>
  <head>
    <title>Angular Tour of Heroes</title>
    <script>document.write('<base href="' + document.location + '" />');</script>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="styles.css">

    <!-- Polyfills -->
    <script src="https://unpkg.com/core-js/client/shim.min.js"></script>

    <script src="https://unpkg.com/zone.js@0.8.4?main=browser"></script>
    <script src="https://unpkg.com/systemjs@0.19.39/dist/system.src.js"></script>

    <script src="systemjs.config.js"></script>
    <script>
      System.import('main.js').catch(function(err){ console.error(err); });
    </script>
  </head>

  <body>
    <my-app>Loading...</my-app> <!-- 1 -->
  </body>
</html>
```
1. 1번부분을 보면 알겠지만 우리가 위에서 만든 component를 통해 (my-app 셀렉터를 사용해) 해당 부분을 불러옵니다.
