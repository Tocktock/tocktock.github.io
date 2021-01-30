---
layout: post
title: leetcode Jump Game II 문제풀기
categories: Algorithms
---

#[leetcode][45] Jump Game II 문제풀기!

---

- [문제풀러가기✈](https://leetcode.com/problems/jump-game-ii)

---

## 👓 문제 요약

처음 인덱스에서 마지막 인덱스에 도달하려면 몇 번 점프해야할까?
해당 인덱스에서 최대 얼마나 뛸 수 있는지는 알려줄게!

> 자세한 문제 설명과 릿코드 홈페이지 참고. [문제풀러가기](https://leetcode.com/problems/jump-game-ii)

## 🔑 문제 풀이

주어지는 인풋의 길이가 최대 30,000 이기 때문에 최소 O(nlgn) 기법을 써야 합니다!

저는 탐욕 기법으로 해당 인덱스에서 뛰었을 때 최대로 가는 놈만 골라서 그냥 뛰었습니다!

## 🥽 소스코드 및 소스해석

```javascript
var jump = function (nums) {
  if (nums.length === 1) return 0;
  if (nums[0] >= nums.length - 1) return 1;
  let nowPos = 0;
  let count = 0;
  for (let i = 0; i < nums.length; ) {
    let maxNum = 0;
    for (let dist = 1; dist <= nums[i]; dist++) {
      if (maxNum <= dist + nums[i + dist] || dist + i >= nums.length - 1) {
        maxNum = dist + nums[i + dist];
        nowPos = i + dist;
      }
    }
    i = nowPos;
    count++;
    if (nowPos >= nums.length - 1) {
      break;
    }
  }
  return count;
};
```

## 🔨 문제 후기

왜 hard 난이도 인지 알 수 없는 문제!! 끄앗!!!
