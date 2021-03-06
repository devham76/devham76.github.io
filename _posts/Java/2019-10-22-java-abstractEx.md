---
title: "JAVA, 추상 클래스&템플릿 메서드 예제"
date: 2019-10-22 15:20:28 -0400
categories: JAVA
tags : [JAVA,java기본개념]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
- <b>동일한 메서드들을 클래스의 상태에 따라 다르게 구현</b>하게 될때 <b>추상 클래스</b>를 사용한다
- 상위(PlayerLevl) 클래스를 핸들링하면 하위 클래스(BeginnerLevel, AdvancedLevel, SuperLevel)를 모두 핸들링 할 수 있다

![template method pratice](https://user-images.githubusercontent.com/55946791/67280069-4c963780-f507-11e9-871c-97222eb685d3.JPG)

##### MainBoard
```java
package gamelevel;

public class MainBoard {

	public static void main(String[] args) {

		Player player = new Player();
		player.play(1);

		AdvancedLevel aLevel = new AdvancedLevel();
		player.upgradLevel(aLevel);
		player.play(2);

		SuperLevel sLevel = new SuperLevel();
		player.upgradLevel(sLevel);
		player.play(3);

	}
}
```

##### Player
```java
package gamelevel;

public  class Player {

	// !!!level 변수는 여러타입을 가질 수 있으므로 상위 클래스의 타입을 갖는다
	private PlayerLevel level;
	/*
	 * PlayerLevel을 참조 하지 않았다면 : 더러워짐
	 private BeginnerLevel level_1;
	 private AdvancedLevel level_2;
	 private SuperLevel level_3;
	 */

	public Player() {
		// Player가 처음 만들어질때
		level = new BeginnerLevel();
		level.showLevelMessage();
	}

	public PlayerLevel getLevel() {
		return level;
	}

	public void upgradLevel(PlayerLevel level) {
		this.level = level;
		level.showLevelMessage();
	}

	public void play(int count) {
		level.go(count);
	}
}
```

##### PlayerLevel
레벨마다 특징이 다르기 때문에 메서드를 추상화 하였다
```java
package gamelevel;

public abstract class PlayerLevel {

	public abstract void run();
	public abstract void jump();
	public abstract void turn();
	public abstract void showLevelMessage();

	// 템플릿 메서드 ; 전체적인 흐름
	final public void go (int count) {
		run();
		for (int i=0; i<count; i++)
			jump();
		turn();
	}
}
```

##### gamelevel
레벨마다 PlayerLevel을 상속받아 제정의 했다
```java
package gamelevel;

public class BeginnerLevel extends PlayerLevel {

	@Override
	public void run() {
		System.out.println("천천히 달립니다");
	}

	@Override
	public void jump() {
		System.out.println("jump 할 줄 모른다");
	}

	@Override
	public void turn() {
		System.out.println("turm 할 줄 모른다");
	}

	@Override
	public void showLevelMessage() {
		System.out.println("**** 초보자 레벨 입니다 ****");
	}
}
```

#### 결과
![result](https://user-images.githubusercontent.com/55946791/67280280-c9291600-f507-11e9-8a98-2f6121a16681.JPG)

---
## Reference
[인프런 강좌](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9E%85%EB%AC%B8/dashboard)
[Do it! 자바 프로그래밍 입문](http://www.yes24.com/Product/Goods/63020974)
