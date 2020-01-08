---
title: "NetWork, TCP 3,4-way HandSaking"
date: 2020-01-08 15:40:28 -0400
categories: [network]
tags : [network, tcp]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---
## TCP 3-way Handshaking
: 상호간에 통신이 되는지 확인하는 기술이며, 데이터가 없다
![3-way handshaking](https://user-images.githubusercontent.com/55946791/71966353-ba1f4d80-3244-11ea-92f9-72283d64fec3.JPG)

### 연결 성립 (connection establishment)
1) 클라이언트는 서버에 접속을 요청하는 <b>SYN(a)</b>패킷을 보낸다.
2) 서버는 클라이언트의 요청인 <b>SYN(a)</b>를 받고, 클라이언트에게 요청을 수락한다는 <b>ACK(a+1)과 SYN(b)</b>이 설정된 패킷을 발송한다.
3) 클라이언트는 서버의 수락 응답인 <b>ACK(a+1)와 SYN(b)</b> 패킷을 받고 <b>ACK(b+1)</b>를 서버로 보내면 <b>연결이 성립(establish)</b>된다.

### 풀어서 설명
<b>1. 나->상대 SYN</b>
- 데이터를 보내기 전에 내가 던진 신호르르 상대방이 받을 수 있는지를 먼저 확인해야 한다.
- SYN 이라는 Packet을 던져서 상대방에게 전달이 되는지를 확인한다.
- 확인용 이므로 데이터 x

<b>2. 상대->나 ACK,SYN </b>
- 상대방이 잘들리는지 답을 주는 신호는 ACK이다
- ACK로 답을 주면서 내 신호도 받을 수 있는지 확인하기 위해 SYN신호를 같이 보낸다.

<b>3. 나->상대 SYN </b>
- 상대방이 준 ACK와SYN을 보고 상대방의 신호를 받을 수 있다면 나는 ACK로 응답만한다. (SYN는 상대방이 이미 잘 받는걸 확인했으니 전송할 필요X )

---

## SYN,ACK 패킷
- SYN : Synchronize Sequence number
- ACK : Acknowledgement
- TCP Header
  - Code Bit(Flag bit)이라는 부분이 존재한다. 총 6Bit이며 각 bit마다 의미가있다
  - URG-ACK-PSH-RST-SYN-FIN
  - SYN : 000010, ACK : 010000

---

## TCP 4-way Handshaking
![4-way handshaking](https://user-images.githubusercontent.com/55946791/71966763-8b55a700-3245-11ea-8aa6-c411b58142f8.JPG)

### 연결 해제 (connection termination)
1) <u>client</u>가 연결을 종료하겠다는 <b>FIN</b>을 전송한다
2) <u>server</u>는 클라이언트의 요청<b>(FIN)</b>을 받고 알겠다는 확인 메세지로 <b>ACK</b>를 보낸다
    - 그리고나서 데이터를 보두 보낼때까지 잠깐 <b>TIME_OUT</b>이 된다
3) 데이터를 모두 보내고 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 <b>FIN</b>을 전송한다.
4) <u>client</u>는 FIN메세지를 확인했다는 <b>ACK</b>메세지를 모낸다
5) 클라이언트의 ACK 메세지를 받은 <u>server</u>는 <b>소켓 연결을 close</b>한다.
6) 클라이언트는 아직 서버로부터 받지 못한 데이터가 있을 것을 대비하여 일정 시간 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거친다. <b>(TIME_WAIT)</b>

---
## ISN이 랜덤숫자 인 이유
<u>( ※ HTTP서비스는 일반적으로 0부텉 시작한다. )</u>
- 처음 client에서 SYN패킷을 보낼때 Seqeunce Number에는 0부터 시작하지 않고 랜덤한 숫자가 담겨진다
- 초기 Seqeunce Number를 ISN이라한다
- Connection을 맺을때 사용하는 포트는 사용하고 시간이 지나면 재사용하기 때문에, 두 통신 호스트가 <u>과거에 사용된 포트 번호 쌍을 사용하는 재사용할 가능성</u>이 있다.
- server측 에서는 패킷의 SYN을 보고 패킷을 구분하는데, <u>순차적 number을 사용하면 이전의 connection으로부터 오는 패킷으로 인식할</u> 수 있다
- 따라사 이런 문제를 예방하기 위해 난수로 ISN을 설정한다

![패킷](https://user-images.githubusercontent.com/55946791/71968367-1f287280-3248-11ea-989a-298af4830ee0.JPG)



---
## Reference
- <https://asfirstalways.tistory.com/356>
- <https://4network.tistory.com/entry/TCPIP20100414?category=286056>
