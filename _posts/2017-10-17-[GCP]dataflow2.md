---
title : CrystalDiskMark
description : CrystalDiskMark라는 게 있어요!
date : 2017-10-17
categories :
- GCP
tags :
- GCP
- dataflow
---

##Beam
 스트리밍 프레임웍이다.
 QPS에 따라 dataflow가 동적으로 증가한다.

##Streaming data
연속되는 데이터,
초기엔 측정함, 현재는 기계학습 알고리즘을 정해 더욱 정교한 분석 수행
1. 스토리지 계층
빠르고 저렴하게 재생가능한 방법으로 읽고 쓸 수 있도록 일관성을 지원
2. 처리 계층
데이터를 사용하고 필요없는 데이터 삭제 등, 알림 등

##프로그래밍 모델
Pipeline input --PCollection--> PTrasform --> ... --> Pileline output --> data result
각 PCollection은 특정 pipeline 객체가 소유함.

###Transform
- 데이터를 변환하는 작업
- 다른 형식, 데이터 그룹화, 필터링, 결합
- input을 하나/여러개 PCollection을 받을 수 있다.
- Core Transform, GCE인스턴스에서 병렬도 실행이 가능하다.

##트리거
처리 중인 데이터를 언제 다음 단계로 넘길지 결정
- 윈도우가 끝나지 않아도 현재 계산값을 다음 Transform으로 넘겨 결과를 볼 수 있다.

1. 타임 트리거
- 일정 시간 주기
2. 엘레멘트 카운트
- 개수 기반
3. Punctuations
- 이벤트 기반

##트리거 결과의 누적
1. Accumulating
2. Discarding


##워터마크
실제 데이터가 시스템에 도착하는 시간 예측
- 예측 시간 앞/뒤로 처리 메커니즘도 제공해야 한다.
