---
title : Google Cloud Essentials 2
description : 영구 디스크와 쿠버네티스
date : 2017-11-14
categories :
- GCP
tags :
- GCP
- Qwiklab
---

# Docker

## 도커는?
- build / ship / run 으로 나눠진다.
- 172.10.0.x 대역이 내부적으로 구성된다.
-


# Creating persistant Disk


# Stack Driver
- AWS 계정 연동
- VM 내부의 솔루션의 로그를 상세하게 분석하기 위해선 따로 도구들을 설치 해야함.
- 이메일을 통한 통보, 빈도수를 설정할 수 있다.
- UpTime Check
  - 실시간으로 웹 페이지, 인스턴스 등을 헬스 체크한다.
- 알람
  - 여러가지 설정이 가능하다.
  - 임계치 넘었을 시 메일을 통해 알림을 줄 것인지.
- Incidents
  - 좀 더 중요한 이슈를 설정해 관리한다.
  - 특정 수치 등이 넘었을 때 알람 등으로 받을 수 있다.
  - 사용자가 확인한 것, 처리된 것, 등을 구분해 처리가 가능하다.
- Event Log
  - 생성/시작 등의 대부분의 이벤트 수집


# LoadBalancers
- L3 : IP주소 참조해 스위칭
- L7 : 패킷까지

## Global Forwarding Rule
- 트래픽 IP, 포트 , 프로토콜에 따라 타겟 프로시로 보냄
- 프록시 등이 있다면 백엔드 서비스로 바로 보낸다.

## 과정
1. 인스턴스 템플릿 생성
2. 타겟 풀 생성
- 패킷이 한 곳으로 접속하게 하기 위해선 이곳이 필요.
3. 인스턴스 그룹을 만든다.
4. 로드벨런서 정의
5. 헬스체크
6. 80번 포트 인스턴스 그룹에 맵핑
7. 백엔드 서비스 생성
  - sticky session 설정 등
8. url 맵을 통해 서비스에 따라 세부적인 로드벨런싱이 가능
9. 로드벨런서의 타겟 프록시를 url맵으로 지정


# Deploying Application

## App Engine
- EC2와 비교하면 EC2는 이것저것 할 것이 많다.
- 이건 알아서 서비스가 가능하게 돼 있다.
- Flexible은 Docker 기반으로
- Standard는 SandBox를 기반으로
  - 애초에 구글은 개발자 기반으로 PaaS를 제공했었다.
  - 시작이 이것, Standard
-
