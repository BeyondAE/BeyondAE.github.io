---
title : TourAPI 사용에 따른 기획 구조 변경
description : TourAPI 사용에 따른 기획 구조 변경
date : 2017-11-30
categories :
- Angular
tags :
- Angular
---

# 개요
> TourAPI 사용에 따라, 현재 기획에서 논의 돼야하는 부분을 명시한다.
---

# 이슈 발의

## 현재 기획 구조
![](AU_UC_구조)

## Pattern1
>  Pattern1(이하 P1)은 Main Activity로 5개의 카테고리에서 사용자가 원하는 목적은 선택하는 화면이다.

TourAPI를 쓰게 되면 선택지의 폭이 넓어지게 된다.
다음은 TourAPI를 사용한 결과 도출 흐름이다.
![]()

TourAPI를 통해 Pattern2에서 보여질 List는 현재 기반이 될 것이라 생각된다. 현재 End User의 위치를 기반으로 지역관광 정보를 도출하는 흐름은 다음과 같다.
![]()

## Pattern2
> Pattern2(이하 P2)는 P1의 5개의 카테고리 중에서 사용자가 선택한 목적에 부합되는 List를 랭킹(Lank) 순으로 보여주는 화면이다.

 TourAPI를 사용해 보여질 수 있는 P2의 모습은 다음과 같다.
 ![]()
