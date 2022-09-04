# 08. 비연결지향형 UDP 프로토콜

## UDP 프로토콜
**User Datagram Protocol** 또는 **Universal Datagram Protocol**
전송 방식이 너무 단순해서 서비스의 신뢰성이 낮고, 데이터그램 도착 순서가 바뀌거나 중복되거나 심지어 누락
따라서 오류의 검사와 수정이 필요없는 프로그램에서 수행할 것으로 가정
![udp_structure](08-비연결지향형_UDP_프로토콜.assets/udp_structure.png)

## UDP 프로토콜을 사용하는 프로그램
* DNS 서버 (도메인 -> IP)
![dns_server](./08-비연결지향형_UDP_프로토콜.assets/dns_server.png)
* tftp 서버 (파일 공유)
![tftp_server](./08-비연결지향형_UDP_프로토콜.assets/tftp_server.png)
* RIP 프로토콜 (라우팅 정보 공유)
![rip_protocol](./08-비연결지향형_UDP_프로토콜.assets/rip_protocol.png)

## 따라하기
* tftpd를 사용하여 데이터 공유하기
* 패킷 캡쳐 및 분석하기
