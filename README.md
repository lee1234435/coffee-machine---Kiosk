# Socket Transport 
네트워크의 소켓은 두 프로그램이 데이터를 송수신할 수 있도록 네트워크 환경에 연결할 수 있게 만들어진 통로(연결부)
 인터넷 소켓(Internet Socket) 혹은 네트워크 소켓(Network Socket) 이라 표현

# Socket 
<img width="518" alt="image" src="https://github.com/lee1234435/Transport/assets/133578714/9159de6b-f053-421c-9eb0-839ef5cd31d7">

- 양방향 통신을 의미한다.
- 클라이언트와 서버 2개로 나뉘게 된다.

<img width="414" alt="image" src="https://github.com/lee1234435/Transport/assets/133578714/ac409452-7ad1-4996-8bbd-59029c9ffc8d">

▸ 양방향 통신 (3 way handshake)
▸TCP를 사용하므로 연결 지향형
▸ 신뢰성 높은 데이터 전송을 보장
▸ 데이터 전송 순서를 보장
▸ UDP보다 느린 속도

<img width="405" alt="image" src="https://github.com/lee1234435/Transport/assets/133578714/605cdaf7-aeca-413e-8971-02dbed6ef53f">


▸ 단방향 통신
▸ UDP를 사용하므로 비연결 지향형
▸ 신뢰성이 낮은 데이터 전송
▸ 데이터 전송 순서가 보장 X
▸ 재전송을 하지 않음
▸ TCP보다 빠른 속도

TCP/IP Socket Communication Order
➪ 클라이언트(Client)  소켓 통신 과정
[1. 소켓 생성]
socket()을 통해 클라이언트 소켓을 생성
 
[2. 소켓 연결]
connect()를 통해 IP주소와 Port Number로 식별되는 서버에 연결 요청
3 way handshake 방식을 사용해 연결
 
[3. 데이터 송수신]
wirte()로 연결된 소켓을 통해 데이터를 송신
read()로 수신
 
받은 데이터 내용을 바로 송신하지 않고
송신용 버퍼 메모리 영역에 저장해두었다가
데이터 크기에 따라 모아서 보내거나 분할하여 보냄
 
[4. 소켓 연결 종료]
close()로 연결 종료
4 way handshake 방식 사용해 종료
 
 
➪ 서버(Server)  소켓 통신 과정
[1. 소켓을 생성]
socket()을 통해 서버 소켓을 생성
 
[2. 소켓을 바인딩]
bind()를 사용해 소켓과 포트 번호를 결합
 
인자로 (서버 소켓, Port Number) 혹은 (IP 주소, Port Number)를 전달
 
지정된 Port Number을 시스템 내에서 사용할 것을 요구
만약 사용 중인 Port Number이라면 에러 반환
 
[3. 연결 요청 대기]
listen()
bind()의 인자가 서버 소켓과 결합이 되었다면
클라이언트의 연결 요청 대기 (클라이언트의 connect())
성공적으로 요청을 수신하면 SUCCESS 반환
 
[4. 연결 허용]
accept()
소켓 사이의 연결 수립
 
클라이언트 소켓과 서버 소켓이 연결되는 것이 아니라
클라이언트 소켓과 accept() API 내부에서 새로 만들어지는 소켓과 연결
 
따라서 서버 소켓은 클라이언트와의 연결 요청을 수신하는 역할
서버 소켓은 다른 연결을 위해 다시 listen()하거나 close()
 
[5. 송수신]
write() & read()
클라이언트의 송수신 과정과 동일
 
[6. 소켓 연결 종료]
close()를 통해 연결 종료
클라이언트와 연결되었던 서버 소켓과 
accept()의 소켓 모두 다 종료해야 함


출처: https://yks-study.tistory.com/34#2. 소켓의 종류-1 [yks_STUDY:티스토리]
