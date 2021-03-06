---
title: "Algorithm, DP"
date: 2019-10-17 14:00:28 -0400
categories: Algorithm
tags : [Algorithm, dp]
---
### DP(다이나믹 프로그래밍)
- <b>주어진 문제를 여러 개의 부분문제들로 나누어 푼 다음, 그 결과들로 주어진 문제를 푼다</b>
- <b>dp는 겹치는 문제가 발생하기 때문에</b> 메모제이션 등이 필요하다
- 메모제이션 : 함수의 결과를 저장하는 장소를 마련해두고, 한 번 계산한 값을 저장해 뒀다 재활용하는 최적화 기법.
<br>
<b>[예시]</b><br>
피보나치 수열을 구현해 보자.
![fibonacci](https://user-images.githubusercontent.com/55946791/66978437-eb283000-f0e4-11e9-8245-7768867a23fe.png)

```java
static int org_fibonacci(int n) {
	call[n]++;
	if(n==0) return 0;
	if(n==1) return 1;
	return fibonacci(n-2) + fibonacci(n-1);
}
```
- 문제점 : n이 30을 넘어가서 40정도의 수치가 되면 컴퓨터는 바로 답을 구하지 못한다.
- 분석 : n이 작은 함수 호출로 갈수록 그 횟수가 점점 증가한다.
 ![비보나치 결과](https://user-images.githubusercontent.com/55946791/66978729-034c7f00-f0e6-11e9-90ac-050cabb93467.JPG)
 이를 그림으로 그려보면 이러하다.
 ![피보나치2](https://user-images.githubusercontent.com/55946791/66978794-40187600-f0e6-11e9-84cd-d27dee1f5f9e.JPG)
그림의 두 부분을 살펴보면 구조가 완전히 동일하고 당연히 f(3)의 값도 같다.
즉, <u>한번 계산하면 충분할 값을 호출할 때마다 계속 부르고 있어 불필요한 시간낭비</u>를 하고 있다는 것이다.

---
### 해결방법
- 메모제이션(memoization) 기법을 사용한다
- <b>계산한 적이 있다면</b> 추가 재귀 호출 없이 <b>그 값을 바로 리턴</b>해준다

#### 1. 탑다운 형식
```java
static int fibonacci(int n) {
	if(n==0) return 0;
	if(n==1) return 1;
	// 이미 값을 계산한 적이 있다면 그 값을 바로 리턴
	if(dp[n] != -1) return dp[n];
	// 아니라면 계산해서 dp리스트에 넣어 보존
	dp[n] = fibonacci(n-2) + fibonacci(n-1);
	return dp[n];
}
```

### 2. 바텀업 형식
```java
static void fibonacci2(int n) {
	Arrays.fill(dp, 0);
	dp[1] = 1;
	for (int i=2; i<=n; i++)
		dp[i] = dp[i-1]+dp[i-2];
	System.out.println(dp[n]);
}
```

```
---
## Reference
[DP 설명](https://kks227.blog.me/220777103650)
