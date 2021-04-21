---
title: "Study, Object, chapter2&3 presentation"
date: 2021-04-20 15:30:28 -0400
categories: Study
tags : [Study, Object]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
# chapter03. 역할, 책임, 협력
- 객체지향 설계란, 올바른 객체에게 올바른 책임을 할당하면서 낮은 결합도와 높은 응집도를 가진 구조를 창조하는 활동이다.

- `협력`은 기능을 구현하기 위해 메시지를 주고받는 객체들 사이의 상호작용
- `책임`은 다른 객체와 협력하기 위해 수행하는 행동
- `역할`은 대체 가능한 책임의 집합
- `책임이 객체 지향 애플리케이션 전체의 품질을 결정한다.`
    - 적절한 책임이 할당 되지 않으면 원활한 협력을 기대 할수 없으며
    - 역할은 책임의 집합이기 때문이다

# chapter04. 설계 품질과 트레이드 오프

|데이터 중심 설계| 행동 중심 설계|
|------|------|
|객체의 상태에 초점| 객체의 행동(책임)에 초점|
|객체를 단순한 데이터의 집합으로 바라본다| 객체 사이의 상호작용을 중심으로 바라본다|
|독립된 데이터 덩어리| 협력하는 공동체의 일원|
|상태 - 구현에 속한다<br>구현은 불안정하고 변하기 쉽다| 책임 - 인터페이스에 속한다<br>필요한 상태를 캡슐화하여 변경에 안정적인 설계를 얻을수있다|
|`이 객체가 포함해야 하는 데이터가 무엇인가?`| `이 객체가 가져야할 책임은 무엇일까?`|


## 데이터 중심 설계 vs 책임 중심 설계
- 둘을 비교하기 위한 기준 : `캡슐화, 응집도, 결합도`

### 캡슐화
- `변경 가능성이 높은 부분(구현)은 내부에 숨기고, 외부에는 상대적으로 안정적인 부분(인터페이스)만 공개함으로써 변경을 최소화한다.`
- 변경될 수 있는 어떤 것이라도 캡슐화 해야한다.
- 달성방법 : 내부 데이터 반환 `접근자` & 데이터 변경 `수정자` 추가 (get,set메소드)
- `캡슐화의 정도가 응집도와 결합도에 영향을 미친다.`


### 응집도와 결합도
- 좋은 설계란?
    - 오늘의 기능을 수행하면서 내일의 변경을 수용할 수 있는 설계
    - 높은 응집도, 낮은 결합도
- 응집도
    - 내부 요소들이 연관돼 있는 정도
    - 얼마나 관련 높은 책임을 할당했는지를 나타낸다.
    - 응집도가 높을수록 변경의 대상과 범위가 명확해지기 때문에 코드를 변경하기 쉬워진다.
- 결합도
    - 다른 모듈에 대해 얼마나 많이 알고 있는지를 나타내는 척도
    - `한 모듈이 변경되기 위해서 다른 모듈의 변경을 요구하는 정도로 측정할수있다.`

### 코드를 완성한 그 순간부터 코드를 수정할 준비를 해야 한다.


# 예제1) 데이터 중심의 영화 예매 시스템
- 데이터 중심 설계 시작 첫번째 질문 : `이 객체가 포함해야 하는 데이터가 무엇인가?`
- 객체의 책임을 결정하기 전에, 이 객체가 포함해야 하는 데이터는 무엇인가?를 생각한다.
![image](https://user-images.githubusercontent.com/55946791/115363173-343ad200-a1fd-11eb-9a3e-c2b64cef9662.png)

### 캡슐화 위반
- 오직 메서드를 통해서만 객체의 내부 상태에 접근할 수 있다.
- getFee, setFee 메서드는 내부에 Money 타입의 fee이름의 인스턴스 변수가 존재한다는 것을 드러낸다.
- 객체간의 협력을 고려하지 않았기 때문에, 객체가 사용될 문맥을 추측할 수 밖에 없고 결국 어떤 상황에서도 해당 객체가 사용될 수 있게 많은 접근자 메서드를 추가하게 된다.

```java
public class Movie {
    private Money fee;
    
    public Money getFee(){
        return fee;
    }
    public void setFee(){
        this.fee = fee;
    }
}
```

### 높은 결합도
- 예제
    - ReservationAgency class는 Screening, Reservation, Movie, DiscountCondition 클래스와 결합되어있다.
    - 따라서 시스템 안의 어떤 변경도 ReservationAgency의 변경을 유발한다.
![image](https://user-images.githubusercontent.com/55946791/115386864-e9c54f80-a214-11eb-9f0c-7b505ee232fc.png)

- 데이터 중심의 설계
    - get,set 메소드를 통해 객체 내부 구현을 인터페이스의 일부로 만들기 때문에, 클라이언트가 구현에 강하게 결합된다.(높은 결합도)

### 낮은 응집도
- 새로운 할인 정책이 생긴다면?
![image](https://user-images.githubusercontent.com/55946791/115387420-9dc6da80-a215-11eb-8343-d05232735afd.png)


# 예제2) 스스로 자신의 데이터를 책임지는 객체 - 영화 예매 시스템
- 객체는 단순한 데이터 제공자가 아니다
- 객체 내부에 저장되는 데이터보다 `객체가 협력에 참여하면서 수행할 책을 정의`하는 오퍼레이션이 더 중요하다.
- (데이터 중심 설계)`이 객체가 포함해야 하는 데이터가 무엇인가?` --> ` 이 객체가 어떤 데이터를 포함해야 하는가 & 이 객체가 데이터에 대해 수행해야 하는 오퍼레이션은 무엇인가?`

## DiscountCondition class 예제 (할인 조건 표현 클래스)
```java
/* 할인 조건 표현 class */
public class DiscountCondition {
    private DiscountConditionType type;
    private int sequence;
    private DayOfWeek dayOfWeek;
    private LocalTime startTime;
    private LocalTime endTime;

    public DiscountConditionType getType() {
        return type;
    }

    /* get, set 메소드 밖에 없었던 class에
       이 데이터에 대해 수행할 수 있는 오퍼레이션을 고려하여 메소드를 추가한다.
       두 가지 할인 조건을 판단할 수 있게 두개의 isDiscountable 메소드 추가
    */
    public boolean isDiscountable(DayOfweek dayOfweek, LocalTime time) {
        if (type != DiscountConditionType.PERIOD) {
            throw new IllegalArgumentException();
        }
        ...
    }

    public boolean isDiscountable(int sequence) {
        if (type != DiscountConditionType.PERIOD) {
            throw new IllegalArgumentException();
        }
        ...
    }
}
```

## Movie class 예제
- 첫번째 질문 ) Movie가 어떤 데이터를 포함해야 하는가?
- 두번째 질문 ) 이 데이터를 처리하기 위해 어떤 오퍼레이션이 필요한가?
    - 데이터를 살펴보면, 영화 요금 계산 오퍼레이션, 할인 여부 판단 오퍼레이션이 필요
<br>

![image](https://user-images.githubusercontent.com/55946791/115391244-395a4a00-a21a-11eb-92d9-7b39d5fcc6a3.png)


## 결과
![image](https://user-images.githubusercontent.com/55946791/115393351-8b9c6a80-a21c-11eb-91c5-b0f7d11fe8a1.png)

- ReservationAgency class에 의존성이 몰려있던 첫 번째 설계보다 개선.
- `데이터를 처리하는 데 필요한 메서드를 데이터를 가지고 있는 객체 스스로 구현`하고 있다.

## 한계1 - 내부 구현 캡슐화 실패
- DiscountCondition class의 속성을 변경한다면?
    - 인터페이스/get메소드 통해 외부에 변수 정보 노출 
        - DiscountCondition.isDiscountable(dayOfWeek, localTime)
        - isDiscountable() 메서드 파라미터 수정, 해당 메서드 사용 클라이언트 전부 수정필요.
- Movie class의 내부 구현을 인터페이스에 노출
    - calculateAmountDiscountedFee, calculatePercentDiscountedFee, calculateNoneDiscountedFee 세가지가 존재한다는 것을 드러내고 있음

## 한계2 - 높은 결합도
![image](https://user-images.githubusercontent.com/55946791/115393494-bb4b7280-a21c-11eb-9fb6-db0ec158b782.png)

- DiscountCondition의 종류 변경 or 할인 조건 명칭 변경, Movie class의 isDiscountable() 변경
- DiscountCondition 변경시 Movie변경필요 --> 결합도가 높다
         
---

# 예제3) 책임 중심 설계 - 영화 예매 시스템
- 객체는 다른 객체와 협력하는 사회적인 존재다.
- 객체간의 협력을 위한 커뮤니케이션 수단 : `메시지 전송`
- 메시지를 수신한 객체는 `메서드를 실행해 요청에 응답한다.`
- 객체간의 협력을 위해 수행하는 행동 : `책임`


## 책임 주도 설계
- `책임을 수행하는 데 필요한 정보를 가장 잘 알고 있는 전문가에게 책임을 할당하자.`
- 책임을 할당하는 것만으로도 `상태와 행동을 함께 가지는 자율적인 객체`를 만들 가능성이 높아진다.
- `구현이 아닌 책임에 집중하여` 유연하고 견고한 객체지향 시스템을 만들수있다.

![image](https://user-images.githubusercontent.com/55946791/115484039-f8e7e400-a28c-11eb-91a0-a27cc3b780bf.png)

1. 시스템이 사용자에게 제공해야 할 기능 : 영화를 예매하는 것
2. '예매하라'는 메시지를 처리할 적절한 객체, 영화 예매 관련 정보를 가장 많이 알고 있는 객체 : Screening
3. 영화 예매를 위한 '예매 가격을 계산' 메시지를 처리할 객체, 가격 계산 정보를 가장 많이 알고 있는 객체 : Movie
4. 가격을 계산 하기 위한 '할인 요금 가격 계산' 메시지를 처리할 객체 : DiscountPolicy
    - 할인 요금 계산은 여러 종류의 객체가 참여할 수 있다(AmoutDiscountPolicy, PercentDiscountPolicy)
    - 여러 객체에 응답할수있는 대표 객체(역할)를 만들자 : `중복 코드 제거`
    - 대표 객체를 구현하는 방법 : `추상 클래스와 인터페이스`
    ![image](https://user-images.githubusercontent.com/55946791/115485075-f6868980-a28e-11eb-9c65-6ceed982f3be.png)
    - 대표 객체를 만들면, 새로운 객체를 추가하기 쉽다 (변경에 용이)


## 결과
![image](https://user-images.githubusercontent.com/55946791/115485614-094d8e00-a290-11eb-9bed-94d5ff5a2452.png)


# 햄의 배운점
이 객체가 가지고 있어야 되는 정보가 무엇일까에 집중했었다
겉으로 보아선 클래스와 객체가 있기 때문에 객체 지향 프로그래밍을 했다고 생각했는데
사소한 변경에도 모든 클래스에 변경이 생기는 절차지향프로그래밍을 했음을 알게되었다.

학부생 시절 객체지향 프로그래밍은 == 붕어빵틀이라고 생각하면 된다 라고 가볍게 배웠는데 이제는 반은 맞고 반은 틀리다라는게 실감된다.
이번장에서 인상적이였던건, 이 객체가 가지고 있는 책임이 무엇인지? 이 객체가 하는 일이 무엇인지?를 생각해야 한다는 것이다.
이것을 고려하며 설계하다보면 동일한 책임을 가지는 객체들이 생길수 있고, 이것들을 대표할수있는 클래스를 만들수 있는데, 이것이 추상화이고 상황을 단순하게 만들수있다.

추상화를 하면 외부 객체와의 소통을 위한 인터페이스만 노출시키고, 객체들의 내부 구현은 각각의 객체 안에 숨길수 있으며 이것은 곧 캡슐화이다.
