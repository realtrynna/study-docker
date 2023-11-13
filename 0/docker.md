- [Docker](Docker)  
- [기능](####도커 기능)  
- [도커를 이루는 기술](###도커를 이루는 기술)

## Docker
애플리케이션은 하드웨어, OS, 미들웨어 등 인프라 환경에 **_민감하게 반응_** 하는 경우가 많다.  
개발 환경과 테스트 환경에서는 잘 동작했지만 제품(Production) 환경에서는 동작하지 않는 경우도 있다.  
  
도커는 애플리케이션뿐만 아니라 동작에 필요한 시스템 환경을 모아 **_컨테이너_** 로 관리한다.  
이렇게 만들어진 도커 이미지는 도커가 설치된 환경이라면 어디든 똑같이 동작한다. 설치된 운영체제가 Linux, MacOS, Windows 든 상관없고 온 프레미스든 클라우드든 상관없다.  
    
이를 이용해 개발자가 Commit 시 지속적인 통합 툴(CI)에서 해당 소스를 도커 이미지로 빌드하고 이미지 레파지토리에서 이미지를 버전별로 관리할 수 있다.  
해당 이미지를 어느 환경이든 배포만 하면 **_독립적으로 동작_** 하므로 지속적인 딜리버리(CD)가 가능하다.  

도커는 특히 분산 환경을 쉽게 구축할 수 있는 클라우드 서비스와 호환이 좋다. 주요 클라우드 프로바이더들은 모두 컨테이너 환경을 쉽게 관리할 수 있는 서비스를 제공한다.  
또한 각 서비스를 독립적인 배포 단위로 구성해 컨테이너로 배포하는 마이크로 서비스 아키텍처와도 잘 맞는다.  

<br>

### 도커 기능
도커는 컨테이너의 리소스, 파일 시스템, 네트워크를 기존 시스템과 **_격리_** 시키고 도커 이미지를 관리하고 공유하는 기능을 제공한다.    

1. **Build - 이미지 만들기**  
애플리케이션 실행에 필요한 모든 라이브러리, 미들웨어, OS, 네트워크 설정 등 필요한 모든 파일을 모아 도커 이미지로 만든다.  
명령어를 통해 수동으로 만들 수도 있지만 자동으로 빌드와 배포를 하는 CI/CD 환경에서는 **_Dockerfile_** 을 이용해 자동으로 만들 수도 있다.  
보통 이미지에는 하나의 애플리케이션만 넣고 여러 컨테이너를 조합해 서비스를 구축하는 방법을 사용하고 1개의 이미지를 여러 개 같이 사용할 수도 있다.  
예를 들면 CentOS 리눅스 이미지와 Nginx 웹 서버 이미지를 겹쳐 새로운 이미지를 만들 수도 있다.  
  
2. **Ship - 이미지 공유**  
도커 이미지를 업로드해 공유하는 저장소를 도커 레지스트리라고 한다. 대표적으로 도커 허브가 있으며 업체에서 제공하는 공식 이미지를 받을 수 있다.  
Ubuntu, CentOS, MySQL, Redis, OpenJDK, NodeJS 등 플랫폼 이미지도 제공한다.  
베이스 이미지를 활용하면 환경을 빠르고 안전하게 자동으로 구축할 수 있다. 애플리케이션 도한 이미지로 만들어 업로드하고 공유할 수 있다.  
Github 와 같은 형상관리 툴과 연동해 Dockerfile 을 관리하고 도커 이미지를 자동으로 빌드하여 도커 허브로 배포할 수 있다.  
퍼블릭 클라우드에서는 비공개 레지스트리와 CI/CD 를 간단하게 구성할 수 있는 아키텍처를 제공한다.  

3. **Run - 컨테이너 동작**      
도커 이미지를 가지고 컨테이너를 생성해 동작시킨다. 하나의 이미지를 가지고 여러 개의 컨테이너를 만들어 낼 수도 있다.  
실제 업무에서는 보통 1대의 호스트에 모든 컨테이너를 동작시키는 게 아닌 여러 호스트로 분산 환경인 경우가 많다.  
이런 분산 환경에서 여러 노드의 컨테이너를 관리하기 위해 K8S 와 같은 오케스트레이션 툴을 주로 사용한다.  

<br>

### 도커를 이루는 기술
리눅스 커널 기술을 기반으로 컨테이너를 구성한다.  

1. **네임스페이스**  
컨테이너라는 가상의 독립된 환경을 만들기 위해 리눅스 커널의 **_namespace_** 기능을 사용한다. 리눅스 오브젝트에 **_이름표_** 를 붙여 같은 네임스페이스로 관리한다.
   
| 네임스페이스        | 설명                                                                                                    | 
|---------------|-------------------------------------------------------------------------------------------------------| 
| PID namespace | 각 프로세스에 할당된 고유한 ID 인 **_PID_** 를 기준으로 다른 프로세스를 격리, 네임스페이스가 다르면 액세스 불가                                 |
| Network namespace | 네트워크 **_리소스_** (IP Address, Port, Routing table 등)를 네임스페이스마다 독립적으로 가져감, 같은 포트라도 네임스페이스가 다르면 사용 가능     |
| UID namespace | 사용자 **_ID_** (UID) 와 **_그룹_** (GID)을 네임스페이스 별로 구분, 컨테이너에서는 루트 권한을 가지고 있더라도 호스트의 관리 권한을 가질 수 없도록 격리 가능 |
 | MOUNT namespace | 리눅스에서 디바이스를 인식하기 위해 마운트가 필요, 파일 시스템 등 마운트 된 디바이스를 네임스페이별로 격리                                          |
| UTS namespace | 호스트명이나 도메인명을 네임스페이스별로 **_독자적_** 으로 설정 가능                                                                    | 
| IPC namespace | 프로세스 간 통신(**_Inter Process Communication_**)에 필요한 공유 메모리, 세마포어, 메시지 큐 등을 독자적으로 사용 가능                        |

<br>

2. **CGroups**  
리눅스에서 프로그램은 프로세스로 실행되고 프로세스는 1개 이상의 스레드로 이루어져 있다. **_CGroups_**(Control Groups) 은 프로세스와 스레드를 그룹화해서 관리하는 기술이다.  
호스트 OS 의 자원을 그룹별로 할당하거나 제한할 수 있다. 컨테이너에서 사용하는 리소스를 제한함으로써 1개의 컨테이너가 자원을 모두 사용해 다른 컨테이너가 영향을 받지 않도록 할 수 있다.  
또한 그룹에 계층 구조를 적용할 수 있어 체계적으로 리소스를 관리할 수 있다.  

| 항목      | 설명         |
|---------|------------|
| cpu     | CPU 사용량 제한 |
| cpuacct | CPU 사용량 통계 정보 제공 |
| CPUSET  | CPU 나 메모리 배치 제어 | 
| memory  | 메모리나 스왑 사용량 제한 |
| devices | 디바이스에 대한 액세스 제어 |
| freezer | 그룹 내 프로세스 정지 및 재개 | 
| net_cls | 네트워크 제어 |
| blkio   | 블록 디바이스 입출력량 제어 | 
  
<br>

3. **네트워크 구성**  
NIC(Network Interface Controller) 는 네트워크 신호를 주고받을 경우 사용하는 하드웨어 랜 카드다.  
리눅스는 해당 네트워크 장치를 /dev/eth0, /dev/eth1 이런 식으로 인식하며 eth0 은 기본 네트워크 장치라고 볼 수 있다.    
도커 컨테이너가 실행되면 컨테이너에 172.17.0.0/16 이란 Private IP 주소가 eth0 으로 자동 할당하며 **_docker0_** 이라고 한다.  
docker0 은 각 컨테이너 네트워크를 연결해 주는 네트워크 브리지 역할을 하며 각 컨테이너에 eth0 에 docker0 이 만든 가상 NIC 인 veth 를 할당한다.  
또한 외부에서 요청을 컨테이너로 라우팅한다.    
컨테이너가 외부 네트워크와 통신할 경우 **_NAPT_**(Network Address Port Translation) 기술을 사용한다.    
Public IP 주소와 Private IP 주소를 1:1로 변환하는 **_NAT_**(Network Address Translation) 와 달리 NAPT 는 **_포트 정보_** 까지 활용하므로  
하나의 퍼블릭 IP 주소로 **_여러 대_** 의 머신을 동시에 연결할 수 있다.  

<br>

4. **컨테이너 데이터 관리**  
호스트 내에 데이터를 저장하기 위해 3가지 방법을 제공한다.  
- 1. **Volumes**    
    호스트의 파일 시스템 내에 **_특정 영역_**(Linux => /var/lib/docker/volumes)을 도커가 관리한다.  
    도커가 아닌 다른 프로세스에서는 해당 영역에 접근할 수 없으며 가장 추천하는 방식  
- 2. **Bind mounts**    
    호스트의 **_파일 시스템 자체_** 를 사용한다. 중요한 시스템 파일이나 디렉터리도 접근 가능하며 호스트와 컨테이너가 설정 파일을 공유하거나 호스트에서 개발하고 컨테이너로 배포하는 방식으로 사용한다.  
- 3. **tmpfs mounts**    
    호스트의 파일 시스템 대신 **_메모리_** 에 저장하는 방식이다. 파일 시스템에 저장하고 싶지 않을 경우 사용한다.  
  
도커 이미지는 Dockerfile 로 만들어진 여러 레이러로 이루어져 있고 각 레이어는 읽기(Read-only)만 가능하다.  
이미지를 가지고 새로운 컨테이너를 생성하면 읽고 쓸 수 있는 레이어가 추가되는데 이를 **_컨테이너 레이어_** 라고 한다.  
컨테이너를 가지고 작업 수행 시 생기는 변경 사항을 모두 컨테이너 레이어에 저장하고 읽을 경우 도커 이미지에 변경된 사항을 조합해서 데이터를 읽는다.  
컨테이너가 삭제되면 컨테이너 레이어도 사라지고 기존 이미지는 변경되지 않고 유지된다.  

하나의 이미지에서 여러 컨테이너를 만들어서 사용할 수 있으며 만약 컨테이너가 서로 데이터를 공유해야 한다면 도커 볼륨에 저장하고 컨테이너에 마운트 하면 된다.  
도커는 Copy-on-Write 방식으로 파일을 관리합니다. Copy-on-Write 는 효율적으로 파일을 공유하고 복사하는 방법이다.  
파일 또는 디렉터리를 읽기만 할 경우 기존 파일을 참조하도록 하고 수정해야 하는 경우에만 파일을 컨테이너 레이어에 복사해서 수정하는 방법이다.  
따라서 꼭 필요한 경우에만 복사가 되므로 데이터 중복이 없고 효율적으로 사용할 수 있다.    

도커는 이런 방식으로 레이어와 파일을 관리하기 위해 스토리지 드라이버를 사용한다.  
다양한 종류의 스토리지 드라이버를 지원하는데 작동하는 방법이 조금씩 다르며 리눅스 배포판 커널에 따라 다른 드라이버를 사용하게 된다.  
  
| 리눅스 배포판 | 스토리지 드라이버                                                                                |
|----- |------------------------------------------------------------------------------------------|
| Ubuntu | aufs, devicemapper, overlay2(Ubuntu 14.04.4 or later, 16.04 or later), overlay, zfs, vfs |
| Debian | aufs, devicemapper, overlay2(Debian Stretch), overlay, vfs                               |
| CentOS | devicemapper, vfs | 
| Fedora | devicemapper, overlay2(Fedora 26 or later, experimental), overlay(experimental), vfs |




