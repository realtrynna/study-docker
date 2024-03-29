## VPN 가상 전용선을 구축하는 기술
가상 네트워크 환경의 구체적인 예로 VPN(Virtual private Network) 이 있다. 인터넷에 가상 전용선을 구축하고 멀리 떨어진 거점 간에도 회사 내 LAN 을 실현할 수 있다.  

<br>

### VPN
가상 사설망을 구축하는 기술이다. WAN(거점 간 연결하는 네트워크) 의 일종이다. 인터넷에 만들어진 가상 전용선을 통해 멀리 떨어진 거점 간 데이터 통신이라도 마치 동일한 LAN 처럼 네트워크 환경을 구축할 수 있다.  
데이터 교환 시 제3자에게 데이터를 도난당하지 않도록 전용선을 사용해야 했다. 하지만 VPN 을 사용하면 전용선 없이도 인터넷을 통해 데이터를 교환할 수 있고 비용까지 줄일 수 있다.  
  
또한 통신 사업자 등이 준비하는 폐쇄형 네트워크를 이용한 IP-VPN 도 있다. 일반 인터넷 VPN 에 비해 안전하지만 비용이 많이 들어간다.  

<br>

### VPN 원리
오버레이 네트워크의 한 종류로, VPN 에서도 터널링 기술을 사용한다. 멀리 떨어진 거점 간에는 VPN 을 지원하는 라우터로 접속되어 인터넷에 전용 터널을 구축한다.  
이렇게 하면 제3자에게 데이터를 도난당할 위험이 크게 줄어든다.  

VPN 을 사용하면 암호화된 데이터로 터널 내부를 송수신하므로 더욱 안전하게 데이터 통신이 가능하다. 데이터를 암호화하는 기술로는 주로 IPSec 이 사용된다.  
VPN 에서는 라우터뿐만 아니라 PC, 스마트폰 등에서 접속할 수도 있다. 이를 통해 외부에서 회사 LAN 에 연결할 수 있다.
VPN 으로의 접속은 VPN 을 지원하는 라우터나 소프트웨어로의 VPN 접속 설정을 실시하기만 해도 되므로 터널링이나 암호화를 의식하지 않아도 간단하게 이용할 수 있다.  

<br>

#### 요약
- VPN 은 오버레이 네트워크의 한 종류이고 가상 전용선을 구축하는 기술이다.
- VPN 에서는 터널링이나 IPSec 기술이 사용된다.


