---
layout: post
title: 프로그래머스 2020 KAKAO 가사 검색 문제 풀이
categories: Algorithms
---

#[프로그래머스✈][2020 kakao] 가사 검색 문제 풀이

---

- 정답률
  - 정확성: 34.4%
  - 효율성: 0.8%
- [문제풀러가기✈](https://programmers.co.kr/learn/courses/30/lessons/42890)

---

## 👓 문제 요약

너 TRIE 자료구조 아냐?

> 자세한 문제 설명과 제한 사항은 프로그래머스 홈페이지 참고. [문제풀러가기](https://programmers.co.kr/learn/courses/30/lessons/42892)

## 🔑 문제 풀이

트리가 아니다 T.R.I.E. 다.
TRIE 자료구조는 단어의 각 글자를 Node 로 보고 자료를 저장하는 자료구조입니다.
자세한건 [🛴 보러가기 ](https://jason9319.tistory.com/129)

Trie를 쓰기만 해서 풀 수 있는게 아니다.?가 등장하면 자료를 검색할 수 없다.
따라서 글자의 길이 마다, 그리고 각 노드에 이 노드를 지나간 놈이 몇명이냐를 저장해서 들어오는 인풋을 양쪽으로 검색할 필요가 있는 아주 미친듯한 문제다.

## 🥽 소스코드 및 소스해석

> 프로그래머스 사이트에서 풀고 직접 가져온 코드 입니다.

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

struct Trie {
    int data;
    Trie *node[26];
};

bool makeTree(string& word, Trie &node, int idx, bool mode); //if exist then true, else false
int findWord(string& word, Trie &node, int idx);
Trie head[10020];
Trie tail[10020];


vector<int> solution(vector<string> words, vector<string> queries) {
    vector<int> answer;

    for (size_t i = 0; i < words.size(); i++)
    {
        int length = words[i].size();
        if (!makeTree(words[i], head[length], 0, true)) {
            head[length].data++;
        }
    }

    for (size_t i = 0; i < words.size(); i++)
    {
        int length = words[i].length();
        if (!makeTree(words[i], tail[length], length - 1, false)) {
            tail[length].data++;
        }
    }
    for (size_t i = 0; i < queries.size(); i++)
    {
        int length = queries[i].size();
        int count = 0;
        while (queries[i][count] == '?') count++;
        if (count == length) {
            answer.push_back(head[count].data);
        }
        else if (queries[i][0] == '?') {
            reverse(queries[i].begin(), queries[i].end());
            answer.push_back(findWord(queries[i], tail[length], 0));
        }
        else {
            answer.push_back(findWord(queries[i], head[length], 0));
        }
    }
    return answer;
}
bool makeTree(string& word, Trie& node, int idx, bool mode){
    //node[alphabet] = 자식
    if (mode && word.length() <= idx) return false;
    if (!mode && idx < 0) return false;
    if (node.node[word[idx] - 'a'] == NULL) {
        node.node[word[idx] - 'a'] = new Trie();
    }
    else if (mode && idx == word.length() - 1 && node.node[word[idx] - 'a'] != NULL) {
        return true;
    }
    else if (!mode && idx == 0 && node.node[word[idx] - 'a'] != NULL) {
        return true;
    }
    if (mode == true) {
        if (!makeTree(word, *node.node[word[idx] - 'a'], idx + 1, mode)) {
            node.node[word[idx] - 'a']->data++;
            return false;
        }
        else {
            return true;
        }
    }
    else {
        if (!makeTree(word, *node.node[word[idx] - 'a'], idx - 1, mode)) {
            node.node[word[idx] - 'a']->data++;
            return false;
        }
        else {
            return true;
        }
    }


    return false;
}
int findWord(string& word, Trie& node, int idx) {

    if (&node == NULL) {
        return 0;
    }
    if (node.node[word[idx] - 'a'] == NULL && idx == word.length() - 1) {
        return node.data;
    }
    else if (node.node[word[idx] - 'a'] == NULL && idx != word.length() - 1) {
        return 0;
    }
    if (word.length() == idx - 1) {
        return node.node[word[idx] - 'a']->data;
    }
    if (word[idx + 1] == '?') {
        return node.node[word[idx] - 'a']->data;
    }
    return findWord(word, *node.node[word[idx] - 'a'], idx + 1);
}
```

## 🔨 문제 후기

제 소스코드 보다 더 잘 만든 사람 많으니 찾아보시는 거 추천합니다. 저도 어려운건 잘 못해요. (●'◡'●)

이 정도 난이도의 문제를 시간내에 풀 수 있다면 당신은 최고의 실력자! 한 번 풀어보고 다시 풀어보자!
