---
layout: post
title: elasticsearch Search 기능 !! Full Text Search !!
categories: elasticsearch
---

#[🌎elasticsearch] Elasticsearch CRUD 기본사용법 (feat. Kibana)

---

- [Elasticsearch 가이드북 ✈](https://esbook.kimjmin.net/)

- [Elasticsearch 홈페이지 가기 ✈](https://www.elastic.co/kr/what-is/elasticsearch)

---

## ElasticSearch 의 진정한 기능 Full Text Search!!

이번에는 ElasticSearch 를 쓰는 이유중 하나인 전문검색 (Full Text Search) 의 간단한 기능을 알아보고자 합니다.
이 부분에 대해서는 내용이 워낙 방대하다보니 제 글은 맛보기 용으로 생각해주시고 [Elasticsearch 가이드북](https://esbook.kimjmin.net/) 을 더 참고해주시면 감사하겠습니다.!

### 전문검색?

전문검색은 간단한 예시로 네이버의 검색, 구글의 검색 기능을 생각하시면 편합니다.
데이터베이스의 특징인 특정 단어의 포함 여부, 조건문의 기능과 유사하지만 특정 단어와의 상관관계에 대한 색인기능이 추가되어 있다고 생각하시면 됩니다.

글로만 읽어도 엄청 복잡합니다. 바로 예시 들어가겠습니다.
