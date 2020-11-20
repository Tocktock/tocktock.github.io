---
layout: post
title: 지킬을 이용하여 깃허브 블로그 만들기
categories: Jekyll
---

안녕하세요 만냥이의 하루 입니다.

저를 포함해서 많은 개발자 분들이 깃허브 블로그를 만드는데 지킬을 사용하고 계시는데 오늘은 그 방법에 대해서 글을 써보려고 합니다.

---

## 목차

- **당신에게 먼저 필요한 것 !!**
- **지킬이 뭐에요??**
- **지킬 테마 선택**
- **깃허브 페이지로 배포하기**
- **첫 블로그 글 써보기**
- **마무리**

---

## **당신에게 먼저 필요한 것 !!**

1. 당연하게도 깃허브 아이디가 필요합니다.!! [🚗깃허브로!](https://github.com/)
2. Git에 대한 기본적인 이해 [🚗깃허브 기본!!](https://medium.com/webeveloper/%EA%B9%83%ED%97%88%EB%B8%8C-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95-github-tutorials-4a63f31bb6a5)
3. 마크다운 언어에 대한 기본적인 이해 (블로그 글작성을 위해 필요합니다.) [🚗마크다운 언어 배우기](https://gist.github.com/ihoneymon/652be052a0727ad59601)
4. 개발할 수 있는 환경이 필요합니다. 저는 VSCode 를 사용했습니다. [🚗VSCode 다운받기](https://code.visualstudio.com/)
5. 루비 언어 설치! [🚗설치하는법!](https://jekyllrb.com/docs/installation/windows/)
6. **끈기와 인내심(가장중요😊)**

---

## 지킬이 뭐에요 ??

[🚗지킬 사이트로 가보기 !!](https://jekyllrb.com/)

지킬은 마크다운, 리퀴드, HTML & CSS 를 사용할 수 있는 정적인 웹페이지를 배포 할 수 있도록 도와주는 프레임워크라고 생각하시면 됩니다.

루비 언어로 만들어진 지킬은 복잡한 데이터베이스나 업데이트 구조가 필요 없고 이미 다른 누군가가 만들어 놓은 지킬 테마를 이용하면 자신만의 블로그를 배포할 수 있습니다.

**어렵다구요?? 사용하면서 알아갑시다!!**

## 지킬 테마 선택

### 테마 고르는 사이트

> 테마를 고르실 때에는 원하는 디자인뿐만 아니라 그리고 원하는 기능의 제공 여부(카테고리, 태그 기능 등)를 체크하세요!!
> [🚗지킬 top 10 테마 추천!!🚗](https://jekyll-themes.com/blog/top-jekyll-themes/)

- [jamstackthemes.dev](https://jamstackthemes.dev)
- jekyllthemes.org
- jekyllthemes.io

저는 두 번째 사이트인 jekyllthemes.org 를 기준으로 말씀 드리겠습니다.

원하는 테마를 고른 후 누르시면 다음과 같은 페이지가 나옵니다.

<img class="post-image-center" src="/assets/img/pick_themes.png" width="70%" alt="테마선택"/>

저는 지금 제 블로그에서도 사용중이고 기본적인 기능에 충실한 Lanyon 테마를 선택했습니다.
테마를 선택하는 3가지 사이트 모두 테마를 선택하게 되면 깃허브로 이어지는 버튼이 있습니다.
위의 경우는 Hompage라고 되어 있군요. 클릭해줍니다.

## 깃허브 페이지로 배포하기

> Lanyon 테마는 자체적으로 카테고리, 태그 기능을 제공하지 않습니다. 후에 추가 설정 및 코드를 작성해야만 해당 기능을 사용하실 수 있습니다.

깃허브 페이지가 나오면 아래 README 문서를 잘 읽어보고 자신이 원하는 기능과 디자인에 적합한 테마인지 한번 더 훑어봅시다 !!

그리고 오른쪽 중간에 보면 fork 라는 버튼이 있습니다.**(로그인 필요)**

<img class="post-image-center" src="/assets/img/forklButton.png" width="70%" alt="fork 버튼 위치"/>
Fork 버튼을 누르게 되면 로그인 된 내 계정의 Repository 로 해당 깃허브 소스가 모두 복사가 됩니다.

<img class="post-image-center" src="/assets/img/forked.png" width="70%" alt="레포지토리 이름"/>

> (사진의 경우 제 깃허브에서 가져온 것이라 Repository 이름이 tocktock.github.io 보입니다.)

Fork를 하게 되면 자신의 계정에 Repository가 생성 됩니다.
위 사진에서 **"/"** 왼쪽에 있는 것이 자신의 계정 닉네임이고 오른쪽이 Repository 이름 입니다.

Repository 는 자신이 Fork 한 Repository 의 이름으로 생성됩니다.
깃허브 블로그를 만들기 위해서는 이 Repository 를 (자신의 계정 닉네임).github.io 라는 형식으로 바꾸어 주어야 합니다.

<img class="post-image-center" src="/assets/img/setting.png" width="70%" alt="세팅위치"/>

화면의 중앙 즈음 보면 Settings 라는 태그가 보입니다. (누르고 들어가라는 뜻 입니다..)

Setting 페이지의 Repository name 을 (자신의 계정 닉네임).github.io 로 바꾸어줍니다. **🛑자신의 계정 닉네임을 반드시 소문자로 해주세요🛑**

새로고침 하고 내리다 보면 Github Page 라는 문구가 보입니다.
<img class="post-image-center" src="/assets/img/deployed.png" width="70%" alt="깃허브페이지정보"/>

위와 같이 **Your site published at 어쩌구 저쩌구** 라고 되어있으면 성공입니다.

> 깃허브 페이지 자체는 반드시 (자신의 계정 닉네임).github.io 일 필요는 없습니다. 원하면 바꿀 수 있습니다

해당 하는 Repository 는 깃허브 자체에서 파일을 작성하고 커밋해도 되지만 플러그인, 빌드 과정에서 필요한 소스가 설치가 안되어있는 경우도 있기도 하고 개별환경의 편의성을 위해서 이 Repository 를 자신의 컴퓨터에 Clone 해줍니다.

> GitHub Clone 방법은 Github Desktop을 사용하는 방법과 커맨드 창에서 git clone "repository 주소" 를 입력하는 방법이 있습니다.

vscode를 기준으로

해당하는 폴더를 vscode 로 열고 좌측 상단의 Terminal 탭을 눌러 New Terminal 을 클릭해줍니다.

<img class="post-image-center" src="/assets/img/terminal.png" width="70%" alt="vscode 에서 terminal"/>

- 지킬과 번들러 gems를 설치하려고 합니다. 터미널에서 다음을 입력합니다.

  > gem install jekyll bundler

- 해당 하는 사이트를 빌드하기 위해 다음을 입력한다.
  > jekyll build
- 빌드된 사이트를 로컬에서 실행해보기 위해 다음을 입력한다.
  > jekyll serve

모든 과정이 순탄하게 진행되었다면 http://localhost:4000 에서 빌드된 자신의 사이트를 볼 수 있다.

이 상태로 GitHub 로 push 하게 되면 깃허브 페이지에서 자신의 블로그를 볼 수 있다.

## 첫 블로그 글 써보기

\_posts 아래의 폴더에 다음과 같은 형식의 파일을 만든다.
(년도)-(월)-(일)-페이지의주소가될곳.md

> 예시 : 2020-10-03-this-is-my-url.md

해당하는 파일에 아래와 같은 글을 적습니다.

<img class="post-image-center" src="/assets/img/firstpost.png" width="70%" alt="첫 글 사진"/>

터미널에서 jekyll serve 를 입력하여 로컬에서 정상적으로 작동하는지 확인합니다.

> 이미 jekyll serve 가 실해중이라면 저장하는 것만으로 해당 사이트에 반영됩니다.

<img class="post-image-center" src="/assets/img/firstpost-insite.png" width="70%" alt="첫 글"/>

정상적으로 포스트가 등록 되었다면 GitHub에 push를 해줍니다!.

와 첫글이다!!

> 원치 않은 오류가 발생하여 정상적으로 작동 안한다면 google 에 빌드 실패이유를 검색하시거나 파일명이 제대로 작성되었는지 확인해주세요!

# 마무리

지킬은 잘 만들어지고 사용하기 간편한 프레임워크이지만 자신의 블로그를 자신의 손맛대로 조금씩 변형하려면 조금 더 자세하게 알 필요가 있습니다.

다음 시간에는 config.yml 파일을 건드리는 것과 간단하게 카테고리를 생성하는 법을 알아 보도록 하겠습니다.

고생하셨습니다. ❤❤❤❤
