---
layout: post
title: leetcode Longest Valid Parentheses 문제풀기
categories: Algorithms
---

#[leetcode][32] Longest Valid Parentheses 문제풀기

---

- [문제풀러가기✈](https://leetcode.com/problems/longest-valid-parentheses)

---

## 👓 문제 요약

"(" 또는 ")" 로만 구성되어 있는 문자열을 줄거야!!
유효한 괄호들의 가장 긴 길이를 구해줘!

> 자세한 문제 설명과 릿코드 홈페이지 참고. [문제풀러가기](https://leetcode.com/problems/longest-valid-parentheses)

## 🔑 문제 풀이

유효한 괄호의 조건은 ")" 가 나왔을 때 "(" 의 개수와 대조해보면 된다!!

- "()()" -> 유효하다!
- "(()" -> 유효하지 않다!
- ")()" -> 유효하지 않다!
- "()((()))" -> 유효하다!

**즉**, 괄호가 유효한 조건을 확인하는 방법은,

"(" 가 나왔을 때는 입의 방향 기준으로 rightCount를 1 더해주고
")" 가 나왔을 때는 rightCount 가 0이 아니라면 rightCount 를 1 빼주고 또한 유효하다고 할 수 있다!!

이 문제는 문자열 전체가 유효한지 아닌지가 아니라 부분집합중 유효한 길이의 최대를 구하는 것이다!

#### 그래서 제가 어떻게 풀었냐면 !!

이 문제의 해결법은 Dynamic Programming, Brute Force, Stack 등 여러 방법이 있다.

나는 Dynamic Programming 기법을 이용해 풀었다.

이전에 무엇이 나오던간에 ")" 가 나온 부분이 유효하다면 유효한 괄호의 길이는 2 이상이라는 것을 보장한다.
즉 유효한 ")" 가 연속으로 나온다면 길이가 2씩 늘어난다는 것을 보장한다!

만약 아래와 같은 상황이라면

    ) ( ( ) )
    1 2 3 4 5    : 인덱스 번호

인덱스 4번까지 검사한다면 길이가 2, 5번까지 검사한다면 4 라는 것을 보장할 수 있다.
아래와 같은 상황이면 어떻게 해야할까?

    ( ) ( ( ) )
    1 2 3 4 5 6

인덱스 2번, 5번, 6번에서는 각각 길이가 2, 2, 4 라는 것을 보장할 수 있다.
**하지만 답은 6이지 않은가 !!**

이를 해결하기 위해서 5번 검사할 때 유효한 길이 인 2만큼 전의 인덱스 즉 3번의 인덱스에서 보장한 값이 무엇인지 확인해야한다.
**어랏 0이네?** 그럼 5번에서는 2까지만 보장한다.

6번을 검사할 때는 유효한길이인 4만큼 전의 인덱스 즉 2번을 보면 2의 길이를 보장한다. !!
즉 2번에서 보장한 2의 길이와 원래 6에서 보장한 길이 4 더한 6의 길이만큼을 다시 6번에서 보장할 수 있다 뚜둔!!!

즉, 만약 유효한 괄호가 계속 유지가 된다면 원래 유효한 길이 바로 전에도 유효해야 한다는 것이다.

우리가 구하려는 인덱스를 i 라고 하자 (0 부터 시작하자)

**dp[i]** 는

- i - 1 이 유효하다면 dp[i - 1] + 2 를 해준다.
- 다시 dp[i - dp[i]] 를 더해준다.

이제 보니 별로 어렵진 않지 않은가?

## 🥽 소스코드 및 소스해석

```javascript
var longestValidParentheses = function (s) {
  let answer = 0;
  let dp = new Array(s.length);
  dp.fill(0);
  // agari direction
  let rightCount = 0;
  if (s[0] === "(") {
    rightCount++;
  }
  for (let i = 1; i < s.length; i++) {
    if (s[i] === "(") {
      dp[i] = 0;
      rightCount++;
    } else {
      if (rightCount === 0) {
        dp[i] = 0;
      } else {
        dp[i] = dp[i - 1] + 2;
        if (i - dp[i] > 0) {
          dp[i] += dp[i - dp[i]];
        }
        rightCount--;
      }
    }
    answer = Math.max(answer, dp[i]);
  }
  return answer;
};
```

## 🔨 문제 후기

구현 능력 자체는 어렵지 않으나, 어떻게 풀지를 생각하는데 조금 오래 걸린 문제다.

stack 으로 푸는 방법도 있길래 봤는데 정말 나는 멀었다고 생각한다.
이 방법으로도 풀어봐야겠다.
