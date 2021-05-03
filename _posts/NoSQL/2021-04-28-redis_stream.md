---
title: "Redis Stream"
date: 2021-04-28 15:05:28 -0400
categories: [Redis]
tags : [Redis]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

# Stream
- Stream은 로그 데이터를 처리하게위해 5.0에서 새로 도입된 데이터 타입입니다.
- 대량의 데이터가 연속적으로 발생할때 처리하기 위해 등장했습니다.
- 기존 데이터를 수정하지 않고 오직 추가로 발생합니다.
- 이런 종류의 데이터를 stream or log데이터라고 합니다.

## XADD : 데이터 추가
```
XADD key ID field value [field2 value2...]

XADD sensor-1234 * temperature 98.7
```

<br>
- ID=* : 명령의 결과를 ID로 리턴한다.

## XLEN : 데이터 길이 조회
- 정확히는 ID개수 조회

```
XLEN sensor-1234
```

## XRANGE : 데이터 조회
```
XRANGE key start end [COUNT count]

XRANGE sensor-1234 - +
1) 1) 1538319053569-0
    2) 1) "temperature"
        2) "98.7"
2) 1) 1538319053569-1
    2) 1) "temperature"
        2) "98.8"


XRANGE key 1538319053569 1538319053569
```
<br>
- start=-, end=+, count로 조회 개수 지정 가능
- start, end에 특정 id지정 가능

## XREAD : 데이터 읽어 오기

```
XREAD [COUNT count] [BLOCK milliseconds] STREAMS key [key ...] ID [ID ...]

XREAD count 1 STREAMS sensor-1234 1538322045065-0
1) 1) "sensor-1234"
    2) 1) 1) 1538322045065-1
        2) 1) "temperature"
            2) "98.8"
```
- count : 읽어올 데이터 개수 지정, 지정하지않으면 모든 데이터를 읽어온다
- ID : 지정한 ID의 다음 데이터를 읽어온다. 처음 데이터 읽으려면 0으로 지정

```
XREAD block 5000 STREAMS sensor-1234 $
```
- Block : 새 데이터가 들어오기를 기다렸다가 들어오면 읽어온다. 이 때는 ID로 특별히 $를 사용한다.


## XDEL, XTRIM : 데이터 삭제
- XDEL
```
XDEL key ID

XDEL sensor-1234 1538322045065-0
```
<br>

- XTRIM

```
XTRIM key MAXLEN [~] count

XTRIM sensor-1234 maxlen 10
```
- sensor-1234에 데이터가 100개 있다면 오래된 순으로 90개를 지우고 최신 데이터 10개를 남긴다.
- `특별 옵션, ~(about)` :  대량의 데이터를 신속히 처리해야하는 스트림에서는 처리 지연이 발생하지 않도록 해야한다.
    - 따라서 짧은 시간에 처리할 수 있을 정도의 데이터를 삭제하는 기능이다.
    - 예) sensor-1234에 100만개의 데이터가 있다면 999,990개를 지우는데 시간이 걸린다. 이때는 데이터를 추가하거나 처리될수 없다. 이때 처리 지연이 발생할 수 있다.


---
### Reference
- http://redisgate.kr/redis/command/streams.php
- https://redis.io/commands#stream