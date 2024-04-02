# 이것이 자바다 - Part04 - Chapter19 네트워크 입출력

## 목차
- [19.1 네트워크 기초](#191-네트워크-기초)
- [19.2 IP 주소 얻기](#192-ip-주소-얻기)

## `19.1 네트워크 기초`

<img src="./image/network.JPG" width="400" height="300"/>

- 네트워크는 여러 컴퓨터들을 통신 회선으로 연결한 것
- LAN (Local Area Network)은 가정, 회사, 건물, 특정 영역에 존재하는 컴퓨터를 연결한 것
- `WAN (Wide Area Network)`은 LAN을 연결한 것으로 우리가 흔히 말하는 Internet

### 서버와 클라이언트
- 네트워크에서 유무선으로 컴퓨터가 연결되어 있다면 실제로 데이터를 주고받는 행위는 프로그램들이 한다.
- 서비스를 제공하는 프로그램을 일반적으로 `server`, 서비스를 요청하는 프로그램을 일반적으로 `client`
- 인터넷에서 두 프로그램이 통신하기 위해서 클라이언트가 먼저 서버에게 요청을 보내고 서버는 요청을 처리한 결과를 응답으로 제공해준다.

<img src="./image/server.JPG" width="400" height="300"/>

### IP 주소
- 우리 집에 고유한 주소가 있어 우편물이나 택배가 정확하게 우리 집에 도착하는 것처럼 `컴퓨터에도 고유한 주소가 있다.`
- 이러한 주소를 `IP (Internet Protocol)`주소라고 한다.
- IP주소는 `네트워크 어댑터(LAN 카드)`마다 할당된다. 예를 들어 두 개의 네트워크 어댑터가 컴퓨터에 존재하면 그 컴퓨터는 두개의 IP주소를 할당받을 수 있다.
- 네트워크 어댑터에 어떤 IP주소가 부여되어 있는지 확인하는 명령어는 window는 ipconfig, 맥OS는 ifconfig
- IP주소는 xxx.xxx.xxx.xxx와 같은 형식이며 xxx는 부호 없는 0~255 사이의 정수이다.
- 연결할 상대방의 IP주소를 모른다면 프로그램들은 통신할 수 없다. 우리가 전화번호를 모를 때 114로 문의 하듯이 프로그램은 `DNS (Domain Name System)`를 이용해 컴퓨터의 IP주소를 검색한다.
- DNS는 도메인 이름으로, IP를 등록하는 저장소이다. 대중에게 서비스를 제공하는 대부분의 컴퓨터는 다음과 같이 도메인 이름으로 IP를 DNS에 미리 등록해 놓는다.
```
  도메인 이름    :      IP주소
------------------------------
www.naver.com : 222.122.295.5
```
- `웹 브라우저는 웹 서버와 통신하는 클라이언트`로, 사용자가 입력한 도메인 이름을 DNS에서 검색하여 해당 IP주소를 얻어낸 다음 웹 서버와 연결해서 웹 페이지를 받는다.

### Port 번호
- 한 대의 컴퓨터에는 다양한 서버 프로그램들이 실행 가능. 예를 들어 웹 서버, DBMS, FTP 서버 등이 하나의 IP주소를 갖는 컴퓨터에서 동시에 실행될 수 있다.
- 이 경우 클라이언트는 어떤 서버와 통신할지 Port 번호를 통해 결정할 수 있다.
- IP는 컴퓨터의 네트워크 어댑터 까지만 갈 수 있는 정보이고 이 컴퓨터 내부에서 실행되는 서버와 연결하기 위해서는 추가적인 Port 번호가 필요하다.
- `Port`는 OS가 관리하는 서버 프로그램의 연결 번호이며, 서버는 시작할 때 특정 Port 번호에 바인딩한다.
- 예를 들어 웹 서버는 80, DBMS는 1521번으로 바인딩할 수 있다.

<img src="./image/port.JPG" width="400" height="300"/>

- 클라이언트도 서버에서 보낸 정보를 받기 위해 Port번호가 필요하며 OS가 자동으로 부여하는 번호를 사용한다. 이 번호는 클라이언트가 서버로 요청할 때 함께 전송되어 서버가 클라이언트로 데이터를 보낼 때 사용된다.
- 전체 Port번호의 범위는 0~65535이며, 다음과 같이 사용 목적에 따라 세 가지 범위를 가진다.

| 구분명 | 범위 |설명|
|:---:|:---:|:---:|
|Well Known Port Numbers|0~1023|국제인터넷주소관리기구(ICANN)가 특정<br>애플리케이션용으로 미리 예약한 Port|
|Registered Port Numbers|1024~49151|회사에서 등록해서 사용할 수 있는 Port|
|Dynamic Or Private Port Numbers|49152~65535|OS가 부여하는 동적 Port 또는<br>개인적인 목적으로 사용할 수 있는 Port|


## `19.2 IP 주소 얻기`
- 자바는 IP 주소를 java.net 패키지의 InetAddress로 표현한다.
- InetAddress를 이용해 로컬 컴퓨터의 IP 주소를 얻을 수 있고, 도메인 이름으로 DNS에서 검색한 후 IP 주소를 가져올 수도 있다.
- 로컬 컴퓨터와 Naver의 IP주소 출력하기

  ```java
  import java.net.InetAddress;

  public class InetAddressExample {
    public static void main(String[] args) {
      try{
        InetAddress local = InetAddress.getLocalHost();
        System.out.println("내 컴퓨터 IP 주소 : " + local.getHostAddress());

        InetAddress[] isArr = InetAddress.getAllByName("www.naver.com");
        for(InetAddress remote : isArr){
          System.out.println("www.naver.com IP 주소: " + remote.getHostAddress());
        }
      }catch(Exception e){
        e.printStackTrace();
      }
    }
  }
  ```
  ```
  결과 

  내 컴퓨터 IP 주소 : 127.0.0.1
  www.naver.com IP 주소: 223.130.192.247
  www.naver.com IP 주소: 223.130.192.248
  www.naver.com IP 주소: 223.130.200.219
  www.naver.com IP 주소: 223.130.200.236
  ```
- InetAddress의 getLocalHost() static method를 이용하여 로컬 컴퓨터의 InetAddress를 얻을 수 있다.
- 또한 InetAddress의 getHostAddress() instance method를 이용하여 IP주소를 출력할 수 있다.
- 만약 컴퓨터의 도메인 이름을 알고 있따면 다음 두 개의 메소드를 사용하여 InetAddress 객체를 얻을 수 있다.
```java
InetAddress ia = InetAddress.getByName("www.naver.com");
InetAddress[] isArr = InetAddress.getAllByName("www.naver.com");
```
> getByName()은 하나의 InetAddress 객체를 가져오고 getAllByName()는 하나의 도메인 이름으로 여러 IP가 등록되어 있는 경우
> 여러 개의 InetAddress 객체들을 가져온다. 여러 IP가 등록되어 있는 이유는 서버의 부하를 나누기 위해서이다.