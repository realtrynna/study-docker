

# **Chapter1 Docker 기본**
## **Docker 사용 이유**
어떠한 프로그램의 다운로드 과정을 **_간단하게_** 만들기 위해서 사용한다.

<br>

1. Docker 없이 프로그램을 다운로드하고 실행하는 순서 <br>
1-1. Installer Download <br>
1-2. Installer Execute <br>
1-3. Complete <br>

<br>

하지만 갖고 있는 Server, Package Version, OS 등에 따라 프로그램 과정 중 에러가 발생할 확률이 있으며 과정 자체가 복잡한 경우가 많다.

<br>

## **Docker**
**_Container_** 를 사용하여 Application을 쉽게 만들어 실행하고 배포할 수 있도록 설계된 도구이다. <br>
Container 기반의 오픈소스 **_가상화 Platform_** 이자 **_생태계_** 이다. 

<br>

* Container
하나의 **_독립된 Container_** 안에 Redis, Mysql 등 다양한 프로그램과 실행 환경을 Container로 추상화하고 **_동일한 Interface_** 를 제공한다. <br>
프로그램의 **_관리_** 와 **_배포_** 를 단순하게 해주며 일반 Container의 개념에서 물건을 손쉽게 운송해 주는 거처럼 프로그램을 쉽게 관리할 수 있게 한다. <br> 

<br>

### **Docker Container**
Code와 모든 종속성을 Package 화하여 Application이 한 컴퓨터 환경에서 다른 컴퓨터 환경으로 빠르고 안정적으로 실행되도록 하는 소프트웨어의 표준 단위이다.

<br>

### **Docker Image**
Code, Run Time, System Tool, Library 등 Application 실행을 위해 필요한 모든 걸 포함하고 있는 가볍고 독립적으로 실행 가능한 소프트웨어 패키지이다 .<br>

또한 Image는 **_Run Time_** 에 Container가 되고 Docker Container의 경우 Docker Engine에서 실행될 경우 Image가 Container가 된다. <br>
Linux와 Window 기반 Application에서 모두 사용할 수 있는 Container화된 소프트웨어는 **_인프라_** 에 관계없이 항상 동일하게 실행될 수 있다. <br>
Container는 소프트웨어를 환경으로부터 격리시키고 **_개발_** 과 **_스테이징_** 의 차이에도 불구하고 균일하게 작동하도록 보장한다.

<br>

* Container는 **_Image의 Instance_**
* Docker Image는 Application을 실행하는데 필요한 설정이나 모든 종속성을 갖고 있으며 Image를 이용해 Container를 생성한다. <br>
    생성된 Container에 의해 Application이 실행된다. <br>

<br>

### **Docker 사용 흐름**
1. Docker **_CLI에 Command_** 입력 <Br>
2. Docker Server(Daemon)는 그 Command를 받아 **_Image_** 를 생성 혹은 **_Container_** 실행 <br>

> Docker Client(CLI) => Docker Server(Daemon) 

<br>

### **Docker와 기존의 가상화 기술(VM)의 이해**
* 가상화 기술 등장 전
    하나의 Server를 하나의 용도로만 사용하고 남는 공간은 그대로 방치됐다. <br>
    하나의 Server에 하나의 OS 하나의 Application을 운영함. <br>
    안정적이긴 하나 매우 비효율적이다. <br>

<br>

* Hyper Visor 기반의 가상화 등장
    논리적으로 공간을 분할하여 VM(Virtual Machine)이라는 **_독립적인 가상 환경_** 의 서버를 이용한다. <br>
    Hyper Visor는 Host System에서 다수의 Guest OS를 구동할 수 있게 하는 소프트웨어를 의미한다. <br>
    하드웨어를 가상화하면서 하드웨어와 각각의 VM을 모니터링하는 **_중간 관리자_** 의 역할도 수행한다. <br>

<br>

### **Hyper Visor**
Hyper Visor란 VM을 생성하고 구동하는 소프트웨어이다. <br>
Hyper Visor 운영 체제와 가상 머신의 리소스를 분리해 VM의 생성과 관리를 지원한다. <br>

Hyper Visor로 사용되는 물리 하드웨어를 **_Host_** 라고 하며 리소스를 사용하는 **_여러 VM을 Guest_** 라고 한다. <br>

1. Native Hyper Visor <br>
Hyper Visor가 직접 하드웨어를 제어하므로 자원을 효율적으로 사용할 수 있으며 별도의 Host가 없으므로 OverHead가 적다. <br>
단점으로 여러 하드웨어 Driver를 직접 세팅해야 하므로 설치 비용이 크다. <br>

2. Host Hyper Visor <br>
가장 많이 이용되는 방법으로 일반적인 소프트웨어처럼 Host OS 위에서 실행되고 하드웨어 자원을 VM 내부의 Guest OS에 Emulator 하는 방식으로 OverHead가 크다. <br>
하지만 Guest OS 종류에 대한 **_제약이 없으며_** 구현이 쉽다. <br>




