---
title : starting Elasticsearch
description : Elasticsearch 기초 정보
date : 2017-10-23
categories :
- Elasticsearch
tags :
- Elasticsearch
---

> Elasticsearch 기초 진행 정리


# 설치
CentOS7환경에 Elasticsearch를 설치해보겠다.
정확한 참고는 [이곳](https://www.elastic.co/guide/en/elasticsearch/reference/current/rpm.html#install-rpm)이다.
## RPM
/etc/yum.repos.d/에 elasticsearch.repo파일을 만들어 준다.
파일을 vi로 열어 다음의 내용을 기입한다.
```sh
[elasticsearch-5.x]
name=Elasticsearch repository for 5.x packages
baseurl=https://artifacts.elastic.co/packages/5.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
- 버전에 따라 내용 구성이 달라진다. 포스팅 일이 좀 지났다면 참고 링크에서 repo파일 내용을 확인하자.
## yum
다음 install을 진행한다.
```sh
sudo yum install elasticsearch
```
## manually installing Elasticsearch
위와는 다른 방법으로 wget을 이용하겠다면 이 구문을 활용하자.
```sh
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.3.rpm
sha1sum elasticsearch-5.6.3.rpm
sudo rpm --install elasticsearch-5.6.3.rpm
```
## System에 시작 프로그램 등록
위에서 온전히 설치를 했다면 elasticsearch를 시작프로그램으로 등록할 필요가 있다.
```sh
sudo chkconfig --add elasticsearch
```

## 정지와 시작
다음의 구문으로 프로그램을 시작/정지 할 수 있다.
```sh
sudo -i service elasticsearch start
sudo -i service elasticsearch stop
```
- 만약 문제가 생긴다면 /var/log/elasticsearch/ 위치의 log 파일을 확인하자.

## System에 시작 프로그램 등록2
systemd를 사용한다면 다음을 구문으로 부팅시 자동 실행을 등록할 수 있다
```sh
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service
```
그리고 다음의 구문으로 시작/정지를 할 수 있다.
```sh
sudo systemctl start elasticsearch.service
sudo systemctl stop elasticsearch.service
```

## 프로세스 확인하기
```sh
bin/elasticsearch -d
// 또는
ps -ef | grep elasticsearch
```

## Start/Stop 스크립트 만들기
```sh
echo 'bin/elasticsearch -d -p es.pid' > start.sh

echo 'kill `cat es.pid`' > stop.sh

chmod 755 start.sh stop.sh
```

# 구조

## vs RDB
기존 관계형 DB와 비교하면 다음과 같은 구성을 가집니다.
Elasticsearch | Relational DB
--- | ---
Indext | Database
Type | Table
Document | Row
Field | Column
Mapping | Schema

## 함수
사용 가능한 함수는 CRUD와 동일하다.
Elasticsearch | Relational DB | CRUD
--- | --- | ---
GET | SELECT | READ
PUT | UPDATE | UPDATE
POST | INSERT | CREATE
DELETE | DELETE | DELETE
