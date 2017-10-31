---
title :  Google Cloud Platform Storage Options
description : Google Cloud Platform Storage Options
date : 2017-10-30
categories :
- GCP
tags :
- GCP
- Qwiklab
---

> CP100 정리, Qwiklab 강의 자료 기반으로 제작됐으며, 무단 배포를 금합니다.

> Google Cloud Platform Storage Options

# Google Cloud Storage
구글의 영구적이고 고사양의 Storage 서비스 입니다.
![Cloud Storage1](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/Cloud%20Storage.png?raw=true)
> - 고성능의 BLOB Storage
> -  간단한 관리
> - 데이터 암호화
> - 4개의 Storage Classes가 사용자에게 유동적으로 주어짐

## 4가지 클래스
그냥 저장소 타입이 4가지란 말이다. 자료 저장소가 다 똑같이 뭐가 4개씩이나 있나? 구글에선 다음과 같이 분류 한다.
![4가지](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/4Classes.png?raw=true)
위 모두는 한 달에 저장된 data의 GB 마다 비용이 지불되며, Coldline 쪽으로 갈 수록 접근 빈도가 낮은 data로 구성하면 된다.
위 지표의 SLA는 개념이 약간 햇갈리는데, 지표가 말하는 것은, 한달을 만 시간이라 했을 때 5시간이 접근되는 비율을 말한 다고 한다. 자주 접근되는 또는 그렇지 않은 데이터에 대한 구분을 지원하기 위한 지표로 사용된다.

클래스에 따른 자세한 가격은 [이곳](https://cloud.google.com/storage/#pricing)을 참고하면 된다.

## Features
자 Cloud Storage가 지원하는 기능들을 살펴 보자.
> - 지역 buckets
> - Versioning
> - Offline import
> - ACLs
> - Object lifecycle
> - import
> - Object change notification

와 필요한 기능 다 있다. 추가적으로 각 기능들을 말하자면
* 지역 과 멀티 지역 버켓을 지원한다. 가능하면 같은 지역을 쓰는게 훨씬 좋지만 일반적으로 그렇지 못한 경우도 있으니 지원한다고 한다.
* 버저닝은 영구 삭제가 따로 존재한다. 안전하게 읽기/수정/쓰기 가 가능하다고 한다. 최대 버저닝 갯수가 가장 큰 이슈인데 안 보이넹..
* ACL은 버켓이나 Object 당 100개가 최대이다. 권한이 할당되지 않은 사용자가 접근하면 403 Error를 맛보게 될 것이다.
* Import는 정말 생각지도 못했다. 더군다나 Off/OnLine을 지원한다! 쿨하게 S3로도 가능하다고 한다.
* 생명주기는 기본적인 규칙이 있다. 365일이 지난 건 지운다. 2013-1-1 이전 생성된 object는 지운다. 버저닝 지정된 것 중 최근 3개를 보관한다.

## Integreation
Cloud Storage는 빈번하게 장기 저장소로 사용되는 저장공간입니다. 그렇기에 다른 GCP 도구들과의 통합이 중요한 요소로 작용되죠.
> -  저장 테이블은 BigQuery로 포팅이 됩니다.
> - 앱 엔진 로그 역시 넘길 수 있습니다.
> - 인스턴스 시작 스크립트, Compute Engine 이미지, Compute Engine 어플리케이션에서 사용되는 object도 저장이 가능합니다.
> - Cloud SQL의 테이블을 받고 넘길 수도 있습니다.

더 자세한 통합 정보는 [이곳](https://cloud.google.com/storage/docs/google-integration)을 참고하세요.

# Google Cloud BigTable
큰 규모의 작업량을 버티는 database service 입니다. 근본적으로 하웁과 호환성이 강조되는 서비스 입니다. 구조화되지 않은 키/값 데이터에 대해 매우 높은 처리량, 확장성을 필요로 하는 프로그램에 이상적입니다. 또 MapReduce 운영, 스트리밍 처리 / 분석, 머신러닝 프로그램을 위한 Storage Engine으로도 뛰어납니다.

어디에 쓰면 좋을까요?
> - 구매 내역, 고객 선호도 등의 마켓팅 data
> - 거래 내역등, 주식, 환률 등의 금융 data
> - IoT data
> - CPU, Memory 사용량 등의 실시간 data

그리고 BigTable은 HBase API를 통해 제공됩니다. 또 이걸 통해 HBase와 BigTable 간의 강력한 이식성을 제공합니다.

## Features
> -  복제 저장소
> - data 암호화
> - ACLs
> - Google Analutics와 Gmail 등의 서비스와 연계

  그리고 BigTable은 Application API나 Streaming, Batch 등을 통해 data 접근을 할 수 있습니다.

## Integration
![BigTable Integration](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/BigTable%20Integration.png?raw=true)
> - dataflow를 사용해 piplines을 구성가능 하다.
> - dataproc를 통해 Hadoop Jobs와도 통합이 가능하다.
> - On-prem 혹은 cloud 기반 hadaoop과도 통합이 가능하다.

# Google Cloud SQL and Google Cloud Spanner

## Google Cloud SQL
일반적인 RDBMS라 생각하면 된다. 일단은 Beta버전이며 Google에선 Beta 버전에 대한 기술지원은 제한하는 편이다.
MySQL과 PostgreSQL을 서비스로 지원하며 자동복제, 백업 관리, 읽기/쓰기에 대한 Vertical scaling, 읽기에 대한 Hrizontal scaling, 보안 등을 지원합니다.
참조 :  
[vertical and horizontal](http://blog.naver.com/wja30/100124946505)
[Scale up/out](https://m.blog.naver.com/PostView.nhn?blogId=islove8587&logNo=220548900044&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)
## Integration
![integration](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/Cloud%20SQL%20Integration.png?raw=true)
> - 앱엔진과 연동
> - Compute Engine 인스턴스 인증 사용(외부 IP만 가능)
> - 외부 어플리케이션과 연동

## Cloud Spanner
Cloud Spanner는 horizontal-scalable이고 강력하게 일련된 관계형 database이다.
> - 자동 복구
> - 강력한 전역 일관성
> - 인스턴스 관리
> - SQL(ANSI 2011)
> - 2TB를 초과하는 Database
> - Many IOPS(초당 수만건의 읽기/쓰기)

더 많은 정보는 [이곳](https://cloudplatform.googleblog.com/2017/02/inside-Cloud-Spanner-and-the-CAP-Theorem.html)을 참고하세요.

## Comparing Storage Options
Storage 서비스가 분류돼 있으니 뭘 선택해야하는지 고민이군요.
구분을 위한 상세한 표를 준비했습니다.
![comparing details](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/comparing%20details.png?raw=true)
> - BigTable은 관계형 db가 아닙니다. 1TB 이하의 작은양에는 사용하지 마세요.
> - online transaction processing(OLTP) 시스템을 제공해야 한다면, Cloud SQL과 Spanner를 고려하세요. 특히 Spanner는 2TB이상의 db에 적합합니다.
> - online analytical processing(OLAP)이라면 당연히 BigQuery
> - 10MB이상의 영구 저장소가 필요하다면 Cloud Storage
> - 저장에 고도화된 구조의 object가 들어간다면 ACID 트렌젝션과 SQL 같은 query가 필요할 겁니다. 그럼 Cloud Datastore를 고려하세요.
