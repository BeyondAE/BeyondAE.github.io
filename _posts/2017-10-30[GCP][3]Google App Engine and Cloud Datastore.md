---
title : [3]GCP App engine and datastore
description : Google App engine and Cloud Datastore
date : 2017-10-30
categories :
- GCP
tags :
- GCP
- Qwiklab
---

> CP100 정리, Qwiklab 강의 자료 기반으로 제작됐으며, 무단 배포를 금합니다.


# Google App Engine and Google Cloud Datastore

## Overview and Customer Stories

### Google app engine 이란?
> - 웹 어플리케이션과 모바일 백엔드를 유동적으로 빌딩하기 위한 플랫폼이다.
> - 배포, 유지보수를 쉽게 도와준다.
> - 서비스 탑제와 NoSQL datastore, 메모리 캐시, 로드 밸런싱, 핼스 체크, 어플리케이션 로그, 사용자 인증 등에 대한 API를 제공한다.
> - 요청되는 트레픽에 맞게 필요한 인프라적 요소가 자동으로 scaling된다.
> - 자동으로 web 취약점을 잡아낸다.
> - Eclipse, IntelliJ, Maven, Git, Jenkins, PyCharm 등의 도구들과 함꼐 사용이 가능하다.

### IaaS와 PaaS
GCP에서 IaaS와 PaaS에 대한 구분은 다음과 같습니다.
![IaaS and PaaS](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/IaaS와%20PaaS.png?raw=true)

#### IaaS
낮은 레벨의 컴퓨팅 HW를 구성하는 것을 말합니다.

#### PaaS
컴퓨팅은 구성된 상태에서 특정 언어에 맞는 런타임을 구성하여 서비스를 제공하는 것을 말 합니다.

## Google App Engine Standard Environment
앱 엔진 표준 환경은 인스턴스 컨테이너 위에서 돌아갑니다. 이 인스턴스는 여러 런타임을 미리 구성해 놓고 있는데요 대표적으로 Java7, Python2.7, go, PHP가 되겠습니다. 각 런타임은 앱 엔진을 지원하는 API를 미리 포함하고 있습니다.
어플리케이션을 쉽게 빌드하고 배포하는데 집중할 수 있게 도와주는 앱엔진은 다음과 같은 특징을 가지고 있습니다.
> - 쿼리, 정렬, 트렌젝션에 대한 연속된 스토레이지
> - 자동 로드 벨런싱
> - 비동기 작업 큐
> - 작업 스케쥴
> - Google Cloud Service와 APIs에 대한 통합

### 요구사항
Java, Python, PHP, Go 언어의 특정 버전을 지원합니다.
샌드박스 제약을 따라야 합니다.
> - 로컬 파일 시스템에 쓰기 불가
> - 60초가 지난 요청은 버립니다.
> - 서드 파티 SW는 설치가 불가 합니다.

### Web application 작업 흐름
정확하게 어떤 흐름으로 사용되는지 알아보도록 하죠.

![workflow](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/workflow.png?raw=true)
1. 개발 및 테스트를 진행합니다.
2. SDK를 통해 앱 엔진으로 배포합니다.
3. 앱 엔진은 알아서 스케일을 조정합니다.

앱 엔진 표준환경에선 많은 서비스를 사용할 수 있습니다.
[이곳](https://cloud.google.com/appengine/docs/standard/#index_of_features)을 참고하세요.

앱 엔진 표준 어플리케이션이 서비스를 쓰기 위해선 다음의 보편적인 방법을 참고하면 되겠습니다.

#### User API
앱렌진 표준 환경 어플리케이션은 인증을 위해 Google Account 또는 보유한 Google Apps domains을 사용합니다. 어플리케이션은 현재 사용자가 인증이 됐는지 확인하는 것이죠.

#### Modules API
큰 사이즈의 어필리케이션이 안정적인 방식으로 저장 서비스를 공유하고 통신할 수 있도록 사용됩니다.

#### Task Queque API
필요한 백그라운드 작업등을 설정할 때 사용합니다.

#### Socket API
앱 엔진 표준 환경은 모든 런타인에서 사용할 아웃 바운드 소켓을 지원합니다.

#### Search API
특정 구조적 데이터에 대한 인덱싱을 지원합니다.

#### Memcache API
읽은 작업을 캐싱해둘 수 있는 API입니다. 공유 Memcache는 무료 형태로 지원이 됩니다. 물론 범위가 한정 돼 있겠죠. 반대로 고정 사이즈를 두고 Memcachea를 지원할 수도 있는데요. gb/hour로 캐시사이즈 마다 별도로 가격이 책정돼 제공되고 있습니다.

#### Mail API

## Google App Engine Flexible Environment
앱 엔진은 유동적으로 사용이 가능합니다. 앞서 언급된 것처럼 특정 런타임을 표준으로 지원하긴 하지만 HTTP만 지원된다면 어떤 언어도 상관이 없습니다.(자바8이나 Jetty 9 etc.) 그리고 개발자는 원하는 구성의 Docker 이미지 역시 사용할 수 있습니다.
인프라에 대한 커스텀 역시 가능합니다.

표준과 유동적인 환경의 차이를 보죠.
![vs](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/vs.png?raw=true)

## Google Cloud Endpoints
