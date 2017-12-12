---
title : Firebase Authentication
description :
date : 2017-12-12
categories :
- Firebase
tags :
- Firebase
---

# What's the Firebase?

> 앱 개발에 필요한 도구와 인프라를 제공하기 위해서 구글에서 만든 클라우드 플랫폼

## 쓰면 어떻게 되나?
![fb쓰면]()
엄청난 비용이 필요한 부분을 뚝딱 해결할 수 있게 한다.
그림에서 보듯이 클라이언트가 모든 것을 해버린다.

## 그래, 뭘 지원하길래?
궁금하면 로그인해서 한 번 구경해 보자!
> https://console.firebase.google.com

구성된 도구들은 대충 이렇다.
![fb도구들]()
개발과 그로쓰해킹, 수입에 대해서 크게 나눠 구분이 가능하다.
> - Growth hacking : 개발적인 면에서 고민하고, 상품/서비스의 개선사항을 모니터링하면서 그 상품/서비스를 성장시키는 것

## firebase analytic
firebase에서 가장 멋진 기능은 앱에 대한 수많은 정보를 관리할 수 있다는 것이다.
> 사용자당 평균 수익(ARPU), 활성 사용자 수, 사용자 유지 보고서, 이벤트 수, 기기 유형, 앱 버전, OS 버전 등의 사용자 속성 등등등!!!

더 많은 정보는 [이곳](https://developers-kr.googleblog.com/2016/06/introducing-firebase-analytics.html)을 참고하자.

# Firebase Development
firebase에서 개발 도구로 제공하는(개발 카테고리에 있는ㅋ) 도구들은 다음과 같다.
![fb메인화면]()

## Firebase for Angular
앵귤러 프로그램에 firebase를 적용해 사용법을 익혀보자.
실습은 [이곳](https://codelabs.developers.google.com/codelabs/firebase-cloud-functions-angular/#1)을 참고로 진행한다.

1. 실습 코드를 다운 받자.
```bash
git clone https://github.com/firebase/friendlychat-web
```
위의 코드를 적당한 폴더에서 실행한다.

```bash
cd cloud-functions-angular-start
```
실습 폴더로 이동한다.

다음, cloud-functions-angular-start 폴더를 사용하는 IDE로 열어 작업 준비를 마친다.

2. 웹 앱에 Firebase 추가
![fb메인화면]()
이곳에서 웹 앱에 Firebase 추가 버튼을 누른다.

- 프로젝트가 없다면 생성 후 진행을 한다.
![fb프로젝트 추가]()

![fb인증코드]()
Javascript 코드가 담긴 창이 나타나는데 Angular에선 저부분만 복사를 한다.

다음, 복사한 코드를 다음의 파일에 붙여넣기 한다.
- src/environments/environment.prod.ts
- src/environments/environment.ts

다음, messageingSenderId의 값을 복사해, 다음의 파일에 존재하는 messageingSenderId의 값으로 붙여넣기 한다.
- src/firebase-messaging-sw.js

다음, 구글 로그인을 허용해야 하는데, firebase 웹콘솔에서 Authentication > 로그인 방법 에서 아래의 작업을 진행한다.
![fb구글계정로그인승인]()

3. 모듈 설치

- 모듈 설치 전에, 위의 git에서 받은 샘플은 버전이 모듈 버전들이 낮기 때문에 package.json을 변경해 줘야한다.
```bash
"dependencies": {
    "@angular/animations": "^5.0.0",
    "@angular/cdk": "~2.0.0-beta.12",
    "@angular/common": "^5.0.0",
    "@angular/compiler": "^5.0.0",
    "@angular/core": "^5.0.0",
    "@angular/forms": "^5.0.0",
    "@angular/http": "^5.0.0",
    "@angular/material": "~2.0.0-beta.12",
    "@angular/platform-browser": "^5.0.0",
    "@angular/platform-browser-dynamic": "^5.0.0",
    "@angular/router": "^5.0.0",
    "@google-cloud/storage": "^1.5.1",
    "@google-cloud/vision": "^0.13.0",
    "angularfire2": "~4.0.0-rc.2",
    "child-process-promise": "^2.2.1",
    "core-js": "^2.4.1",
    "firebase": "~4.4.0",
    "rxjs": "^5.5.2",
    "zone.js": "^0.8.14"
  },
  "devDependencies": {
    "@angular/cli": "^1.6.0",
    "@angular/compiler-cli": "^5.0.0",
    "@angular/language-service": "^5.0.0",
    "@types/jasmine": "~2.5.53",
    "@types/jasminewd2": "~2.0.2",
    "@types/node": "~6.0.60",
    "codelyzer": "^4.0.1",
    "jasmine-core": "~2.6.2",
    "jasmine-spec-reporter": "~4.1.0",
    "karma": "~1.7.0",
    "karma-chrome-launcher": "~2.1.1",
    "karma-cli": "~1.0.1",
    "karma-coverage-istanbul-reporter": "^1.2.1",
    "karma-jasmine": "~1.1.0",
    "karma-jasmine-html-reporter": "^0.2.2",
    "protractor": "~5.1.2",
    "ts-node": "~3.2.0",
    "tslint": "~5.7.0",
    "typescript": "~2.4.2"
  }
```
위의 코드를 복사해 package.json의 dependencies를 수정해 준다.

```bash
npm install
```

다음, cli도 설치해줍니다.
```bash
npm -g install firebase-tools
```

firebase에 로그인 해보죠.
```bash
firebase login
```

다음, 프로젝트를 추가합니다.
```bash
firebase use --add
```

4. deploy
앵귤러를 firebase에 배포합니다.
먼저, 앱을 빌드해줍니다.
```bash
ng build --prod --aot
```

다음, 배포!
```build
firebase deploy --except functions
```
functions는 일단 제외하겠습니다.

배포가 완료되면 다음과 같은 결과를 볼 수 있다.
```bash
i  deploying database, storage, hosting
i  database: checking rules syntax...
✔  database: rules syntax for database areu-firebase-test is valid
i  storage: checking storage.rules for compilation errors...
✔  storage: rules file storage.rules compiled successfully
i  storage: uploading rules storage.rules...
i  hosting: preparing dist directory for upload...
✔  hosting: 17 files uploaded successfully
i  database: releasing rules...
✔  database: rules for database areu-firebase-test released successfully
✔  storage: released rules storage.rules to firebase.storage/areu-firebase-test.appspot.com

✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/areu-firebase-test/overview
Hosting URL: https://areu-firebase-test.firebaseapp.com
```
Hosting URL로 접속해 보자!

5. Cloud functions
Cloud functions를 통해 기본적인 api를 구성해보자.
```bash
cd functions
ls
npm install
```

다음, index.js 파일을 열어 다음의 코드를 복사하자.
```Javascript
/**
 * Copyright 2017 Google Inc. All Rights Reserved.
 * ...
 */

// Import the Firebase SDK for Google Cloud Functions.
const functions = require('firebase-functions');
// Import and initialize the Firebase Admin SDK.
const admin = require('firebase-admin');
admin.initializeApp(functions.config().firebase);

// TODO(DEVELOPER): Write the addWelcomeMessage Function here.
// Adds a message that welcomes new users into the chat.
exports.addWelcomeMessages = functions.auth.user().onCreate((event) => {
  const user = event.data;
  console.log('A new user signed in for the first time.');
  const fullName = user.displayName || 'Anonymous';

  // Saves the new welcome message into the database
  // which then displays it in the FriendlyChat clients.
  return admin.database().ref('messages').push({
    name: 'Firebase Bot',
    photoUrl: '/assets/images/firebase-logo.png', // Firebase logo
    text: `${fullName} signed in for the first time! Welcome!`
  });
});
// TODO(DEVELOPER): Write the blurImages Function here.

// TODO(DEVELOPER): Write the sendNotification Function here.

// (OPTIONAL) TODO(DEVELOPER): Write the annotateMessages Function here.
```
저장 후 Cloud functions를 배포한다.

```bash
firebase deploy --only functions
```
배포가 완료 됐다면 Hosting URL로 접속해 보자.

![fb인증시도]()
인증을 수행하고

![fb인증후에챗]()
welcome메시지와 채팅을 확인할 수 있다.

6. 결과
우리는 앞선 실습으로 firebase의 개발적인 부분에 대해 다뤄봤다.
firebase서버를 구성하고, 웹앱을 생성해 계정을 연동, 그리고 Function을 구성해 배포까지!
firebase는 위의 행위를 통해 사용자가 아주 쉽게 Back-end를 다룰 수 있게 구성했다.

아, 물론 우리가 수행한 데이터 역시 쉽게 확인이 가능하다.

![fb배포]()
우리가 배포한 웹앱에 대한 정보이다.

![fb인증]()
다음, 우리가 인증을 시도한 계정에 대한 정보이다.

![fbRealTime]()
인증 후 수행했던 채팅에 대한 이력이다.

위의 정보는 firebase 콘솔에서 모두 확인이 가능하다. 뿐만 아니라 firebase는 gcp의 인스턴스를 구성해 사용하는 것임으로 gcp 콘솔에서도 확인이 가능하다.


---
# 참조
- [Firebase](https://firebase.google.com/)
- [구글 firebase는 무엇인가? 제공하는 기능은?](http://hanburn.tistory.com/169)
- [Firebase를 실제 모바일 백엔드로 사용하면 일어날 수 있는 일들](https://academy.realm.io/kr/posts/firebase-as-a-real-mobile-backend/)
- [요즘 유행하는 ‘그로스 해킹(Growth Hacking)’이란 무엇인가?](https://alleciel.com/2015/04/29/dentsu-growth-hacking-1/)
