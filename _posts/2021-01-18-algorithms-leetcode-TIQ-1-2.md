---
layout: post
title: leetcodd  3sum 문제풀기
categories: Algorithms
---

#[leetcode][📣top interview question] Remove Duplicates from Sorted Array Solution 문제풀기!

---

- [문제풀러가기✈](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/727/)

---

## 👓 문제 요약

정렬된 배열을 하나 줄게!

중복된 숫자 없는 배열을 갖게 해줘!!

> 자세한 문제 설명과 릿코드 홈페이지 참고. [문제풀러가기](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/727/)

## 🔑 문제 풀이

문제를 잘 읽어보면, 다른 배열을 만들어서 사용하지 말고 추가 메모리는 하나만 사용하라고 명시되어있다!.

이 문제는 채점할 때 다음과 같이 하기 때문에 !! 다른 배열을 만들어서 사용하지 말라고 한다. 또한
단 하나의 추가 메모리를 사용하라고 합니다!

    // nums is passed in by reference. (i.e., without making a copy)
    int len = removeDuplicates(nums);

    // any modification to nums in your function would be known by the caller.
    // using the length returned by your function, it prints the first len elements.
    for (int i = 0; i < len; i++) {
        print(nums[i]);
    }

#### 그래서 제가 어떻게 풀었냐면 !!

들어오는 인풋 배열에서 모든 것을 해결했습니다.!

c++ 의 vector 와 같이 특정 원소를 제거하는 연산은 O(n) 의 시간이 들게 됩니다.
배열 구조 특성상 메모리가 이어져야 하기 때문에 뒤에서 앞으로 이어준 후 새로운 배열을 반환하기 때문이라고 합니다.
만약 제거해야하는 원소가 매우 많아진다면 시간적 여유가 없어지겠죠??

> 다만 리스트 관련 자료구조로 특정 원소를 삭제한다면 연산은 O(1) 이 됩니다!

문제는 어렵지 않습니다. !! 손풀기로 갑시다!

## 🥽 소스코드 및 소스해석

```javascript
var removeDuplicates = function (nums) {
  let nowIndex = 0;
  for (let compareIndex = 1; compareIndex <= nums.length; compareIndex++) {
    if (nums[nowIndex] !== nums[compareIndex]) {
      nowIndex++;
      nums[nowIndex] = nums[compareIndex];
    }
  }

  return nowIndex;
};
```

## 🔨 문제 후기

취업관련 코딩테스트 준비를 하다가 찾은 문제집 !! 괜찮은 것 같다!!

하루에 3시간씩 알고리즘 관련 문제를 푸는데, 시간이 남으면 Hard 문제도 도전해야겠다!
