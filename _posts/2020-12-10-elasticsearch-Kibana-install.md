---
layout: post
title: elasticsearch Kibana install !!
categories: elasticsearch
---

#[🌎elasticsearch] Elasticsearch Kibana install (ubuntu 20.04)!!

---
- [Elasticsearch 가이드북 ✈](https://esbo21ok.kimjmin.net/)

- [Elasticsearch 홈페이지 가기 ✈](https://www.elastic.co/kr/what-is/elasticsearch)

---

😁😁  nibana 라는 것을 설치할겁니다!!
이전 포스트에서 정상적으로 ElasticSearch 를 설치하셨다면 
<http://localhost:9200> 에 접속하셨을 때 json 형식의 데이터가 보인다면 준비는 완료된 것입니다.

> 아직 ElasticSearch를 설치 안하셨다면 ?? [🛴Elastic 설치하기!🛴](https://tocktock.github.io/elasticsearch/elasticsearch-install/)


## 👓 먼저 Kibana 는?

ElasticSearch 홈페이지에서는 Kibana 를 Elastic Stack 을 들여다보는 창!! 이라고 강조하며 소개하고 있습니다.!!

여기서 Elastic Stack이란?

- ElasticSearch : Query 담당 !! 
- Logstash : 수집 담당 !! 
- Kibana : 시각화 담당 !!

그 중 Kibana 는 데이터를 표현하고 보여주는 역할을 합니다.
단순히 보여주는게 아니라 분석하고, 정리하고 사람이 보기 쉽게 만들어줍니다!. 
물론 Kibana 에서 SQL 문을 이용하여 데이터를 수집도 가능합니다!!

Elastic Stack 은 위의 세가지를 연동하여 사용하는 Stack 으로 ELK 라고 줄여서도 부릅니다.🥽🥽
아주 훌륭한 분들이 정말 좋은 시스템을 만들어놨군요 ~~

우리는 여기서 Kibana 를 오늘 설치해볼겁니다.!!
LogStash는 다음에 또 알아봅시다~



## 🔑 사실 키바나 설치는 어렵지 않습니다.

> $ sudo apt install kibana

끝 입니다.

다음 명령을 입력해 Kibana 를 실행합시다.

> $ service kibana start

다음 명령을 입력해 kibana 실행 상태를 확인합니다.

> $ service kibana status

정상적으로 Kibana 가 실행중이라면 <http://localhost:5601> 를 통해 앱을 확인하실 수 있습니다.

끝 입니다. 다음에는 Kibana 의 dev tool 을 이용해서 REST API 의 기본인 CRUD 기능을 
배워보겠습니다. ! ! !
커피 한 잔 스윽 타서 준비합시다!!