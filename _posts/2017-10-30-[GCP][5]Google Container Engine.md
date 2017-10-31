---
title : 5. Google Container Engine
description : Google Container Engine
date : 2017-10-30
categories :
- GCP
tags :
- GCP
- Qwiklab
---

> CP100 정리, Qwiklab 강의 자료 기반으로 제작됐으며, 무단 배포를 금합니다.

> Google Container Engine

# Introduction to Containers

## 컨테이너란?
![container](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/container.png?raw=true)
> - OS 단에 대한 가상화
> - 의존성 코드들
> - 각 프로세스 격리

## 왜 컨테이너를 쓰나?
> - 개발, 테스팅 그리고 제품 환경에 대한 연속성을 제공
> - OS와 application의 의존성을 줄이기 위해
> - on-prem과 cloud env 간의 마이그레이션
> - 에자일 지원

# Kubernetes
> - 오픈 소스 기반의 컨테이너 오케스트레이션 시스템
    - 자동 배포, 스케일링
> - 구글에서 10년간의 경험이 녹아있다.
> - Multi-zone Clouster
> - Load Balancing
> - Maintenance application


# Google Container Engine
Cloud Container Builder는 어플리케이션 소스 코드를 담은 Cloud Storage에 대한 도커 이미지를 생성할 수 있다. 이 이미지는 카동으로 Container Registry에 저장이 된다. 이것을 통해 배포가 가능하다.

## App Engine vs Container Engine
![App Engine vs Container Engine](https://github.com/beyondat/beyondat.github.io/blob/master/images/2017-10/App%20Engine%20vs%20Container%20Engine.png?raw=true)
