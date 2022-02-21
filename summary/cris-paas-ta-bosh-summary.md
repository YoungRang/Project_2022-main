# Bosh Summary

##  1. Bosh 개념

- 분산 시스템의 배포 및 수명주기 관리를 지원하는 오픈소스 툴
- PaaS를 이루는 VM들을 설치 및 관리하는 도구
- 종류 : Bosh, Direct-VM(micro-bosh), BOSH-lite
- BOSH가 지원하는 IaaS : VMware vSphere, Google Cloud Platform, AWS, OpenStack, MS Azure, VMware vCloud
- PaaS-TA는 VMware vSphere, Google Cloud Platform, AWS, OpenStack, MS Azure 등을 지원함

### 1.1 BOSH1
- BOSH1은 bosh-init을 통하여 bosh를 생성하고 BOSH1 CLI를 통해 PaaS-TA Controller, Container 생성

### 1.2 BOSH2
- bosh-deployment를 이용하여 BOSH 생성 후, paasta-deployment로 PaaS-TA 설치


##  2. Bosh 구성
### 2.1 컴포넌트 구성

+ CLI : Director와 상호작용을 위한 CLI
+ Director : Director가 VM을 생성 또는 수정할 때 설정 정보를 저장
+ NATS : 컴포넌트간 통신을 위한 메시지 채널
+ Registry : VM 생성을 위한 설정정보 저장
+ UAA : Bosh 사용자 인증 인가 처리
+ Agent : VM에 설치되며 , Director 로부터 명령을 받아 개별 작업을 수행

### 2.2 Bosh 구성 요소

+ Release 
  + 가상 머신 또는 인스턴스에 배포하는 방법을 BOSH에 설명하는 데 필요한 전체 소스 코드 및 작업 정의
  + BOSH가 완벽하게 작동하는 Kubernetes 클러스터를 배포하는 데 필요한 모든 패키지 및 세부 정보를 포함
  
+ Stemcell 
  + 버전이 지정된 기본 운영 시스템 이미지이며 BOSH에서 지원하는
    각 CPI를 위해 구축
  + BOSH 에이전트가 사전 배포된 강화된 기본 운영 체제 이미지
  + BOSH는 이 에이전트를 사용하여 인스턴스의 해당 VM에 소프트웨어를 설치하고 수명주기를 관리
  
+ Manifest 
  + BOSH Deployment manifest 는 components 요소 및 배포의 속성을 정의한 YAML 파일


## 3. Bosh 배포

+ BOSH는 일반적으로 단일 가상 머신 또는 인스턴스로 배포됨. 

### 3.1 Bosh 배포

+ NATS
  + BOSH의 다양한 서비스가 상호 작용할 수 있도록 지원하는 메시지 버스를 제공 
  
+ POSTGRESQL
  + 단일 가상 머신 BOSH 배포 내부에 있으며 Postgres에서 제공함
  + 외부 데이터 소스를 사용하도록 이를 수정하여 BOSH 가상 머신을 재구축하고 데이터베이스에 다시 연결하여 지속적인 상태를 다시 로드할 수 있음.
  
+ BLOBSTORE
  + BOSH에 업로드된 각 스템 셀 및 릴리스는 Blobstore에 저장
  + BOSH 배포는 기본적으로 내부 스토어(webdav)를 이용하지만 PostgreSQL 데이터베이스와 마찬
    가지로 외부화할 수 있음.
  
+ 상태 모니터링
  + BOSH에서 배포하는 각 가상 머신은 배포 매니페스트에 정의되어 있는 BOSH 릴리스와 관련하여 작업을 할당 및 배포하기 위해 통신할 수 있는 에이전트가 있어야
     합니다. 

+ CPI
  + CPI는 IaaS에 따라 다른 실행 가능한 바이너리로서 BOSH에서 이를 사용하여 배포 YAML에 정의된 IaaS와 상호 작용

+ UAA
  + BOSH가 SAML 또는 LDAP 백엔드를 통해 작업자를 인증할 수 있도록 사용자 액세스 및 인증을 제공

+ CREDHUB
  + 암호, 인증서, 인증 기관, SSH 키, RSA 키 및 임의 값과 같은 자격 증명을 관리 BOSH는 공개 인증서 및 키와 같은 배포를 위한 주요 자격 증
     명을 생성 및 저장하기 위해 CREDHUB을 활용