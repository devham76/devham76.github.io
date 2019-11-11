---
title: "Algorithm, 알고리즘 문제해결 전략, 동적계획법"
date: 2019-11-12 13:00:28 -0400
categories: Algorithm
tags : [Algorithm,  dp, 알고리즘 문제해결 전략]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
### 동적계획법
- 두번 이상 반복 계산되는 부분 문제들의 답을 미리 저장하므로써 속도의 향상을 꾀하는 알고리즘 설계 기법

### 메모제이션
- 함수의 결과를 저장하는 장소를 마련해두고, 한 번 계산한 값을 저장해 뒀다 재활용하는 최적화 기법
---
### 메모제이션 구현 패턴
1. <b>항상 기저 사레를 제일 먼저 처리</b>합니다.
    - 입력이 범위를 벗어난 경우 등을 기저 사례로 처리하면 매우 유용합니다.
2. 함수의 반환 값이 항상 0 이상 이라는 점을 이용해 <b>cache[]를 모두 -1로 초기화</b> 합니다. cache[]의 해당 위치에 적혀 있는 값이 -1이라면 이 값은 계산된 반환 값일리 없습니다.
    - 만약 함수의 반환 값이 음수일 수도 있다면 이 방법은 사용할 수 없습니다.

```c
// 전부 -1로 초기화 해둔다
int cache[2500][2500];
// a와 b는 각각 [0,2500]구간 안의 정수
// 반환 값은 항상 int형 안에 들어가는 음이 아닌 정수
int someObscureFunction( int a, int b){
  // 기저 사례를 처음에 처리한다!
  if(...) return ...;
  // (a,b)에 대한 답을 구한 적이 있으면 곧장 반환 !
  int& ret = cache[a][b];
  if(ret != -1) return ret;

  // 여기에서 답을 계산한다.
  ...
  return ret;
}
int main() {
  // memset()을 이용해 cache 배열을 초기화 한다.
  memset(cache, -1, sizeof(cache));
}
```
---
### 동적 계획법 레시피


---
## Reference
- [문제보러가기](https://www.welcomekakao.com/learn/courses/30/parts/12230)
- 알고리즘 문제해결 전략
