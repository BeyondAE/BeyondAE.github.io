---
title : GCP 시작하기
description : CP100 GCP시작
date : 2017-10-25
categories :
- GCP
tags :
- GCP
- Qwicklab
---

> CP100 정리, Qwicklab 강의 자료 기반으로 제작됐으며, 무단 배포를 금합니다.


# GCP 프로젝트

## 프로젝트 리소스 구성
모든 GCP 리소스는 프로젝트에 속해 있다. 프로젝트 생성이 GCP 시작의 가장 처음이란 말이다.

그리고 프로젝트 내에서 모든 서비스가 허용/비허용 되는 구조이다. 그렇기에 모든 프로젝트나 리소스는 명확하게 구분되며 이에 따른 빌링(billing) 역시 그렇다.

프로젝트는 정책으로 다른 권한, 분할된 사용자 접근을 지정할 수 있으며 빌링과 관리도 그렇다.

## 프로젝트 구분
프로젝트를 구분하는 속성은 3가지 이다.
> - 프로젝트 이름
> - 프로젝트 번호
> - 프로젝트 ID

GCP는 구조적인 리소스 컨테이너와 프로젝트를 제공한다. 이것은 앞서 언급된 대로 그룹화, 계층적인 조직화를 통해 리소스 접근이 제공된다. 이것들은 관리자 Console 외에도 Resource Manager API를 통해 프로그래밍 적으로도 구성이 가능하다.

그렇다면 Resource Manager API를 통해 뭘할 수 있을까?
> - 계정과 관련된 모든 프로젝트 리스트 얻기.
> - 프로젝트 생성
> - 기존 프로젝트 업데이트
> - 프로젝트 삭제
> - 실수로 삭제한 프로젝트 복구!

관련된 API 정보는 다음을 참고하자.
> - [RPC API](https://cloud.google.com/resource-manager/reference/rpc/index)
> - [REST API](https://cloud.google.com/resource-manager/reference/rest/index)


# IAM(Identity and Access Management)

## IAM
IAM의 구조는 다음과 같다.
![IAM](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/IAM-2-1.png?raw=true)
'can do what'에 대한 부분은 IAM의 역할을 명시하는 부분이다. 이 역할은 간단하게 권한들의 묶음이다. 예를 들어 프로젝트의 인스턴스의 생성, 삭제, 시작, 중지 등의 행위를 위해서 역할을 명시해야 하며 이에 맞게 하나 이상의 권한을 줘야한다.

'who'는 누구에게 역할을 수행가능하게 할 것이가를 명시하는 부분이다.

## IAM 선언전의 기본 역할 구조
기본적인 역할 구조는 다음과 같다.
![Role](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/role2-2.png?raw=true)

각자를 구분해서 설명하자면
> - Owner : 프로젝트에 멤버 추가 및 프로젝트 삭제 등의 강력한 권한을 가진 최고 관리자. Editor를 추가할 수 있다.
> - Editor : application 수정/배포가 가능한 사용자. Viewer를 추가할 수 있다.
> - Viewer : 읽기만 가능한 사용자.
> - Billing administrator : 결제 관리자.

추가적으로 위의 모든 역할은 여러명으로 설정이 가능하다.

## IAM에서의 역할
Cloud IAM을 통해 제공되는 역할을 2가지 종류가 있다.
> - 기본적인 역할 : Owner, Editor, Viewer 등의 위에서 설명한 구조이다.
> - 조직적인 역할 : 이건 새로 추가된 IAM 역할인데 좀 더 섬세한 접근을 다룰 수 있게 한다. 다른 섹션에서 좀 더 다루기로 한다.

멤버에게 역할을 주기 위해 관리자 콘솔을 사용하면 된다.
Owner가 멤버를 추가할 시엔 email 주소(gmail)를 사용해 추가하면 되고, 멤버는 초대에 수락하기만 하면 된다.

## Curated roles
조직적인 역할(Curated role)은 그룹단위로 면밀하게 권한을 주는 것이다. Google Group으로 관리되는 멤버들에게 권한 묶음을 건네주고 프로젝트를 관리할 수 있게 하는 것인데, 이것은 **기본적인 역할** 의 구조를 탈피해 전략적으로 역할을 부여할 수 있게 한다.
![curated role](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/cp100-2-3.png?raw=true)

## IAM 리소스 계층
계층에 대한 예시는 다음과 같다.
![hierachy](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/cp100-2-4.png?raw=true)
Cloud Platform의 리소스는 계층적으로 조직화할 수 있다. 위의 세 단계로 조직화가 가능한데 각각에 대한 설명은 다음과 같다.
> - Organization : 회사/조직을 대표하는 level이다. 이곳에서 결정된 역할은 하위로 계승되게 된다.
> - Project : 상속받는 역할을 프로젝트 단위로 신뢰 경계를 결정하는 것을 대표한다. 프로젝트 내 하위 리소스들에 대한 범위를 잘 생각하고 결정해야 한다. 예를 들어 App Engine이 storage buckets에 접근 가능하게 말이다. 여기서 결정된 역할은 하위로 계승될 것이다.
> - Resource : 각 리소스에 대한 정책을 설정한다. 당연하게도 리소스 level에서 결정된 정책은 상위 보다 강력하기 떄문에 리소스 사용 시 여기서 결정된 정책을 따르게 된다.



# Interacting with GCP
