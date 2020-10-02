---
layout: post
title: 프로그래머스 2019 KAKAO 겨울 인턴쉽 징검다리 건너기 해설
categories: Algorithms
---

#[프로그래머스✈][2019 kakao 겨울 인턴쉽] 징검다리 건너기 해설

---

- [문제풀러가기✈](https://programmers.co.kr/learn/courses/30/lessons/64062)

---

## 👓 문제 요약

**"우리 돌다리는 약해유.."**

니니즈 친구들이 라이언 선생님과 함께 가을 소풍을 가는 중에 징검다리를 만났다. 이 징검다리의 돌은 매우 연약하여 여러번 밟으면 부서지고 더이상 사용할 수 없다. 돌마다 내구도가 주어질 때 건널 수 있는 니니즈들의 최대 인원 수를 구하여라.

- 우리 니니즈들은 **반드시** 뛸 수 있는 가장 가까운 돌로 뛰어야한다.
- 니니즈의 인원은 200,000,000 이상이다.
- 선생님은 건너지 않는다.

> 자세한 문제 설명과 제한 사항은 프로그래머스 홈페이지 참고. [문제풀러가기](https://programmers.co.kr/learn/courses/30/lessons/64062)

## 🔑 문제 풀이

우선순위 큐를 잊어버릴 꺼 같아서 사용한다.
우선순위 큐에는 내구도가 가장 낮은 데이터를 top에 저장한다.

> 우선순위 큐에 대한 자세한 정보는 다음을 참고하라 [우선순위큐 설명](https://chanhuiseok.github.io/posts/ds-4/)

top에 저장된 돌의 내구도 만큼 니니즈들이 건너갔다고 가정하고, 오른쪽과 왼쪽의 사용 가능한 돌의 거리를 계산하여 최대 건널 수 있는 거리를 넘어가면 더이상 건너지 못한다고 생각한다.

## 🥽 소스코드 및 소스해석

> 프로그래머스 사이트가 아닌, visual studio 에서 코드를 작성해서 그대로 가져온 것 입니다. 일부 테스트 코드가 존재합니다.

```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

struct STONE {
    int idx;
    int count;
};
struct COMP {
    bool operator()(STONE& a, STONE& b) {
        return a.count > b.count;
    }
};
priority_queue<STONE, deque<STONE>, COMP >myPQ;

int solution(vector<int> stones, int k);
int main() {
    vector<int> stones = { 5,5,5,5,200000000 };
    solution(stones, 4);
}
int solution(vector<int> stones, int k) {
    for (int i = 0; i < stones.size(); i++)
        myPQ.push({ i, stones[i] });

    int jumpCount = 0;
    bool donotJump = false;
    while (!myPQ.empty() && !donotJump) {
        STONE minStone = myPQ.top();
        jumpCount = minStone.count;
        while (myPQ.top().count == jumpCount) {
            STONE tempStone = myPQ.top();
            int rt = tempStone.idx + 1;
            int lt = tempStone.idx - 1;
            while (rt < stones.size() && stones[rt] < jumpCount) rt++;
            while (lt >= 0 && stones[lt] < jumpCount) lt--;
            if (rt - lt > k) {
                donotJump = true;
                break;
            }
            myPQ.pop();
            if (myPQ.empty()) break;
        }
    }
    return jumpCount;
}
```

## 🔨 문제 후기

이제 C++의 STL 없이는 알고리즘 코딩을 할 수 없을 것 같다.
