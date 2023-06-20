---
layout: post
title: "추억 점수"
date: 2023-06-19
last_modified_at: 2023-06-19
categories: [Algorithm]
---

프로그래머스 Lv.1 문제

obj를 만들어 key : value 형식의 일종의 사전을 만들어서

key값을 호출해서 값을 더하는 방식으로 풀었다.

그런데, 의도한 대로 값은 제대로 호출되나

배열의 첫번째로 들어오는 값을 제외하고는 전부 null로 뜨는 오류가 있다.

문제점을 못 찾아서 보류해 둔 문제

```js
function solution(name, yearning, photo) {
  var answer = [];
  let obj = {};
  name.map((name, index) => {
    obj[`${name}`] = yearning[index];
  });

  photo.map((x) => {
    let point = 0;
    for (let i = 0; i < x.length; i++) {
      if (x[i] !== undefined) {
        point = point + obj[x[i]];
      }
    }
    answer.push(point);
  });

  return answer;
}
```

## 해결

for문 사용 & null인 부분 제외하고 push하기로 변경했더니 잘 된다.

```js
function solution(name, yearning, photo) {
  var answer = [];
  let obj = {};
  name.map((name, index) => {
    obj[`${name}`] = yearning[index];
  });

  for (let i = 0; i < photo.length; i++) {
    let point = 0;
    for (let j = 0; j < photo[i].length; j++) {
      if (obj[photo[i][j]] != null) {
        point = point + obj[photo[i][j]];
      }
    }
    answer.push(point);
  }

  return answer;
}
```
