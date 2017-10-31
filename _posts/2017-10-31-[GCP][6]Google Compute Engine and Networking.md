---
title : Google Compute Engine and Networking
description : Google Compute Engine and Networking
date : 2017-10-31
categories :
- GCP
tags :
- GCP
- Qwiklab
---

> CP100 정리, Qwiklab 강의 자료 기반으로 제작됐으며, 무단 배포를 금합니다.

> Google Compute Engine and Networking

# Google Compute Engine Overview
Compute Engine에 대해 알아보도록 하자.

## managed VMs
컴퓨트 엔진은 vm을 구글 인프라에 생성해줍니다. 다음의 hw 특징이 있습니다.
> -  고사양의 CPU, memory, standard 등을 지원
> - standard, ssd, local ssd 등의 영구 디스크
> - 리전 단위로 네트워크 묶음

스케일과 퍼포먼스 성정 그리고 컴퓨트 클러스터를 쉽게 구성할 수 있게 합니다. 서비스를 구성할 때 기업은 초기 투자 비용 없이 하이 인프라를 구성할 수 있습니다. 사용할 때 마다 비용이 나가는 것은 당연한 거겟지만..

이 VM은 GCP Console이나 gcloud 툴로도 생성이 가능합니다. 이미지는 Linux 서버나 Windows 서버 그리고 버전도 알아서 고르면 되는 거죠.

이렇게 생성된 vm 인스턴스는 각자 네트워크를 가지고 인터넷과 통신할 수 있습니다. 일반 서버처럼 네트워크 영역을 나눌 수도 방화벽을 사용해 접근을 제한할 수도 또 고정 라우팅을 통해 트래픽을 포워딩할 수도 있죠.
서브넷 구성은 [이곳](https://cloud.google.com/compute/docs/vpc/)을 참고하세요.

##  innovative pricing
GCP는 분당과금으로 유명하다. 하지만 지금은 [초당과금 정책](https://cloudplatform.googleblog.com/2017/09/extending-per-second-billing-in-google.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+ClPlBl+%28Cloud+Platform+Blog%29)으로 바뀌었다. 공식 page를 가보면 알겠지만  최소 분당 and 초당 과금 정책으로 바뀐 것을 알 수 있다.
Compute Engine은 높은 throughput을 제공한다. 추가 금액 없이! 물론 hw 스펙을 높이면 금액이 붙기는 하겠지만.. 사용에 대해선 최대한 할인을 결정해서 과금이 진행이 된다.
[Preemptible instances](https://cloud.google.com/compute/docs/instances/preemptible)를 제공하는데 vm이 언제 꺼져도 상관없는 서비스면 맞는 인스턴스라고 한다.
[Custom Machine Type](https://cloud.google.com/compute/docs/instances/creating-instance-with-custom-machine-type)도 지원하지만, predefined machine type을 사용하는 것을 추천한다.

# Google Cloud Networking
Google Cloud Virtual Network, Google Cloud Interconnect, Google Cloud DNS, Google Cloud Load Balancing, and Google Cloud CDN 등에 대한 설명이 주를 이룬다.

## Cloud Virtual Network
네트워킹을 기능적으로 리소스 처럼 관리하기 위해 사용합니다. GCP 리소스와 연결된 각 독립적인 VPC(Virtual Private Cloud)에 제공됩니다.
싱글 글로벌 IP와 subnetwork를 구성해 생성할 수 있습니다.(물론 같은 resion) subnet network는 auto와 custom 모드가 있다는 군요. subnet의 크기는 [CIDR](http://www.terms.co.kr/CIDR.htm)에 따라 동적으로 증가가 가능하다 합니다.

## Cloud Virtual Network’s internetworking features
> - Fine-grained networking policies
> - Granular IP address range
> - selection
> - Routes
 - 다른 인스턴스로 포워딩된 트래픽은 외부 IP가 필요없다.
> - Firewalls
 - 인스턴스 접근을 전역적으로 조절 할 수 있다.
> - Virtual Private Network (VPN)
 - IPsec 기반의 안전한 연결
> - Cloud Router
 - CEN과 non-Google Network 사이에 BGP(Border Gateway Protocol) 라우트를 동적으로  업데이트한다.

## Google Cloud Interconnect
 Google Cloud Interconnect는 기업급의 연결을 GCP 고객에게 고가용성과 낮은 지연율로(기존 인터넷 연결보다) 허용하고 있다.
 제공되는 연결 방식들은 3가지 이다.

* Carrier Interconnect : 기업급의 연결은 이것으로 제공된다.
 * Direct Peering : Google과의 직접적인 연결은 이것
 * CDN Interconnect : 선택된 CDN 공급자와 직접적인 연결 구성을 허용하고 있다.

## Google Cloud DNS
- domain을 IP로 바꿔준다.
- add, edit, delete DNS 기록하는 관리 존을 생성할 수 있다.
 - Anycast 네임 서버를 사용한다.

## Google Cloud Load Balancing: HTTP(s)
- 여러 Compute Engine과의 트래픽을 조절해준다.
- 전역, 외부 IP 트레픽을 라우트 해준다.
- pre-warming 없이 탄력적인 제공, fault tolerance 적용

## Google Cloud Load Balancing: TCP/SSL, UDP
[forwarding rules](https://cloud.google.com/compute/docs/reference/latest/forwardingRules/)과 [target pools](https://cloud.google.com/compute/docs/reference/latest/targetPools/)를 사용해 네트워크 로드 벨런싱을 진행한다. 여기선 위와 다르게 TCP/SSL, UDP 기반의 로드 벨런싱을 말하는 것이다. [firewall rule](https://cloud.google.com/compute/docs/load-balancing/network/example#configure_compute_engine)에 따라 443을 허용하거나 인스턴스를 등록하 거나 등이 가능하다.

## Google Cloud CDN (Content Delivery Network)
구글의 globally distributed edge 캐시들을 이용해 인스턴스와 보다 가깝고 로드 벨런싱 된 HTTP를 캐시해 둘 수 있다.

# Google's Network Internal
우리는 이미 구글이 전 세계적으로 Datacenter를 보유하고 있고 이 모든 것은 해저광 케이블로 이어진 것을 알고 있다. 구글은 자신들이 생각하는 네트워크 서비스를 상용 제품들의 구성으론 해결할 수 없음을 일찍(10년 전부터)느끼고 자체 네트워크를 구성하기 시작했다.

![](https://www.cisco.com/web/KR/about/news/images/traffic_4.jpg)
현재 시대의 IP 트래픽은 상상을 초월한다. 2014년 월 59.9EB에 달했던 세계 IP 트래픽이 오는 2019년에넌 월 168EB를 기록할 것으로 보인다고 한다. 이것은 1984~2013년 까지의 트레픽 총향과 맞먹는 다고 하니 현재의 인터넷 서비스는 그야 말로 방대한 컨텐츠를 빠르게 다루고 있다고 볼 수 있다.[참고](https://www.cisco.com/c/ko_kr/about/press/2015/may-aug-2015/0601.html)

이 시대에 필요한 것은 네트워크 처리이다. 기존과는 획기적으로 달라야 기하급수 적으로 치솟는 인터넷 사용량을 효율적으로 처리할 수 있다. 시대의 니즈에 맞게 예전 이더넷 스위치 + 라우터의 구조에 클라이언트 + 서버 중심 디자인이 모바일 기기와 트레픽의 급증으로 구조가 점차 바뀌고 있다.

## SDN (Software Defined Network)
변화의 요구에 맞게 나타난 것이 바로 SDN이다. sw프로그래밍을 통해 네트워크 경로 설정과 제어 등의 복잡한 운용관리를 편하게 처리할 수 있는 차세대 기술이다. 과거 각 네트워크 장비에서 제어 기능을 분리할 수 없었던 것에 반해 SDN에서는 분리가 가능한 구조로 변모했다. 미리 준비된 프로세스를 장비에 탑재 시켜 네트워크를 프로비저닝한다. 즉 어플라이언스를 도입해 네트워크 탭을 구성하는 것이 아닌 탭 구축을 네트워크 프로그래밍을 통해 한다는 말이다.

## Google Espresso architecture
![](http://image.zdnet.co.kr/2017/04/11/yong2_qc1nj2xWdPxnxp.jpg)
에스프레소는 구글의 새로운 SDN 전략이라 보면된다. 이것은 피어링 엣지 아키텍쳐로 2년 이상 적용되어 전체 트래픽의 20% 이상을 소화하고 있다. 하나의 요청이 엣지단에 붙고 여기서 효율적인 처리가 가능한 데이터센터로 붙어 처리 후 필요시 다른 클러스터로 넘어가 작업을 하고 가장 최선을 모두 수행 후 사용자에게 다시 돌아가게 된다.
아민 바다트는 질의 하나를 실시간으로 처리하기 위해 수십개의 인터넷 인터넷 라우터가 작동하고 수천대 컴퓨터가 동원된다고 했다. 이것은 1초 미만으로 이뤄 져야한다. 라고 했다. 이것이 구글의 자체 인프라 구성의 주된이유라 할 수 있다.

참고 :
* [SDN 정의](http://www.bloter.net/archives/267815)
* [SDN, NV, NFV 차이점 이해하기](http://www.itworld.co.kr/news/86025?page=0,0)
* [구글을 빠르게 할 신기술 에스프레소](http://www.zdnet.co.kr/news/news_view.asp?artice_id=20170411135431)
* [구글 클라우드 데이를 다녀와서](http://brainbackdoor.tistory.com/32)
