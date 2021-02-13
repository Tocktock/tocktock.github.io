---
layout: post
title: DevTip - UUID vs Auto Increment
categories: DevTip
---

#[DevTip] UUID vs Auto Increment

## 👓 UUID 가 뭐죠

UUID 는 간단하게 범용 고유 식별자라고 생각하면 편할것 같습니다.

예를 들어 내가 뭔가 만들 때마다 식별할 수 있는 고유값을 만들고 싶다면 사용하면 됩니다.

문서를 만들고 문서의 고유 식별자를 만들 때도,
회원가입을 하고 유저의 고유 식별자를 만들 때도

UUID 를 만드는 함수 하나 가져와서 그냥 쓰면 만사 ok.

물론 UUID 는 **유일을 보장** 한다는 것은 아닙니다.. UUID 는 **실질적으로 유일함** 을 목적으로 하고 있고 실제로 대부분의 상황에서 그러합니다.

이게 가능한 이유가 UUID 는 16 바이트의 문자로 이루어집니다. 비교해보자면 c 언어에서 integer 타입은 대략 -21억 ~ 21억 사이로 표현이 가능합니다.
반면 UUID 는 10의 38승까지, 정확히 **340,282,366,920,938,463,463,374,607,431,768,211,456** 개가 생성 가능합니다.

감이오시쥬~??

## 👓 Auto increment primary keys ??

Auto increment primary key 는 프로그램적으로 문제가 없는 한, **유일을 보장** 합니다.

> 다만 너무 많은 id가 생성되면 아닐 보장하지 않을 수도 있습니다. 하지만 우리는 40억개 이상 생성하지 않을꺼야!! 라고 생각하고... 또한 키를 Integer 가 아니라 더 큰 타입으로도 생성할 수 있기 때문에...

단순히 1부터 시작해서 숫자를 늘려가거나, 원하는 숫자의 식별자를 만들어내는 방식입니다.

## 🍗 UUID vs Auto Increment

### 단점 먼저!

#### UUID

- 가장 치명적인 단점은 **성능**에 저하를 일으킨다는 겁니다. 예들들어 각각 primary key 가 3,2,4,1,5 인 데이터를 삽입하고 검색의 효율을 위해 id를 정렬 한다고 칩시다. 그럼 1,2,3,4,5 순서로 저장이 되겠습니다. 자 이제 저 숫자가 16바이트의 엄청 큰 문자열이라고 생각해봅시다. 정렬하는 비용이 생각보다 많이 들 것입니다.
- 사람이 보기 힘듭니다.
- 필요 이상으로 공간을 많이 차지 합니다.

#### Auto Increment

- Auto Increment 방식은 분산 시스템에서 적합하지 않습니다. 게임서버를 예로 들어봅시다. 서버 A와 서버 B 를 통합하려 합니다. 그런데 서버 A와 서버 B를 별개로 두었기 때문에 서버 A 에 있는 Id가 서버 B 에도 존재할 수 있습니다. 통합하려면 상당히 고생해야할지도 모릅니다 ^^;;

### 장점은?

#### UUID

- Auto Increment 와는 반대로 분산 시스템에서 괜찮습니다.
- 개발 환경에 독립적입니다. 어떤 디비를 쓰던 상관 없이 그냥 uuid 생성 함수 가져와서 쓰면 됩니다. 즉 DB를 바꿀 때 그냥 Id 갖다 박으셔도 됩니다.

#### Auto Increment

- 빠릅니다.
- 눈에 보기 쉽습니다. 로그를 분석하는데 "509ca884-67cc-...'" 어쩌고 나오면 갑자기 머리 아파집니다.

사실 id 숫자가 40억개 이상 쓸 일이 없을거야!! 하면 그냥 Auto Increment 쓰셔도 무방합니다.

필요에 따라 UUID 를 쓰세요!! 꼭 UUID 일 필요는 없습니다. 상황에 맞게 쓰시면 될거 같네요!

---

피드백은 항상 환영입니다!!