## CCN이란 무엇인가요?
CCN(Cloud Connect Network)은 클라우드 VPC 간, VPC와 로컬 IDC 간의 상호 연결 서비스를 제공합니다. VPC와 직접 연결 게이트웨이 인스턴스를 CCN에 추가하여 단일 포인트 액세스와 전체 네트워크 리소스 상호 연결을 구현할 수 있으며, 간단하고 스마트하며 안전하고 유연한 하이브리드 클라우드 및 전 세계 상호 연결 네트워크를 손쉽게 구축할 수 있습니다.
>?CCN은 현재 내부 테스트 단계에 있기 때문에 [내부 테스트 신청](https://cloud.tencent.com/apply/p/tp2478t9skn)을 제출해야 합니다. 심사를 최대한 빨리 완료하여 메시지와 내부 메시지를 통해 알려 드리겠습니다.

## 제품 구성
CCN은 다음 부분으로 구성됩니다.
- CCN 인스턴스
CCN 인스턴스는 CCN 서비스를 사용하여 네트워크 리소스를 관리하는 데 필수적입니다. 
 상호 연결할 네트워크 인스턴스를 CCN 인스턴스에 연결만 하면 서로 연결을 구현할 수 있습니다. 일일이 설정할 필요가 없습니다.
- 네트워크 인스턴스 
CCN 서비스가 현재 지원하는 네트워크 인스턴스는 VPC와 직접 연결 게이트웨이가 있습니다. 
세부 정보는 [VPC](https://cloud.tencent.com/document/product/215)와 [DC](https://cloud.tencent.com/document/product/216)를 참조하십시오.

## 기능 소개
Tencent Cloud CCN은 다음 기능을 보유하고 있습니다.

**전체 네트워크 상호 연결**

전체 네트워크 멀티 노드, 다중 라우팅의 자동 포워딩 및 학습, 초 단위의 라우팅 수렴을 통해 CCN에서 모든 네트워크 인스턴스 상호 연결을 단번에 구현할 수 있기 때문에 관리가 편합니다.

**스마트 학습과 스케줄링**

CCN은 전체 네트워크 멀티 노드, 링키지 풀 메시 상호 연결에 기반하여 번거로운 라우팅 관리 작업이 필요없습니다. 스마트 스케줄링 시스템은 전체 네트워크 다중 토폴로지, 라우팅, 트래픽에 기반하여 통일적으로 검사하며 로컬 비즈니스 가까운 노드 액세스, 최단 링키지 상호 연결을 지원합니다.

**자동 라우팅 배포**

CCN 다중 라우팅은 자동 학습할 수 있습니다. 네트워크 토폴로지에 변화가 발생하였을 때, 라우팅은 자동 학습 및 업데이트할 수 있기 때문에 구성, 변경 등 번거로운 작업을 진행할 필요가 없어 관리가 간단해 사용자의 네트워크 확장성 및 유지보수 효율을 극대화할 수 있습니다.

## 기능 비교
**피어링 연결/직접 연결 터널과의 차이**

Tencent Cloud CCN을 사용하기 전 여러 개의 VPC를 서로 연결, IDC와 여러 개의 VPC 서로 연결을 실행하고 싶다면, 두개의 VPC 사이에 피어링 연결을 생성하여 IDC부터 모든 VPC까지 직접 연결 터널을 생성해야 합니다. 연결을 생성할 수 없을 수 있으니 각 VPC, IDC의 IP 주소 범위는 중첩되어서는 안 됩니다. 연결 생성 후, 인스턴스별 라우팅 테이블을 관리해야 하며, 라우팅 전략을 수동 추가해야 서로 연결을 구현할 수 있습니다. 

위의 시나리오에서 Tencent Cloud CCN을 사용하여 CCN 인스턴스 1개만 생성하고 상호 연결해야 할 VPC와 IDC를 해당 CCN에 추가하기만 하면 모든 VPC, IDC와 여러 VPC의 서로 연결을 구현할 수 있습니다. CCN의 라우팅은 자동 포워딩 및 학습되어 1회 작업만으로도 인스턴스를 CCN에 추가할 수 있기 때문에 수동으로 구성하지 않아도 인스턴스의 라우팅 테이블을 관리할 수 있습니다.
>?CCN이 적용된 비즈니스 모범 사례에 대한 세부 정보는 [모범 사례](https://cloud.tencent.com/document/product/877/18797)를 참조하십시오.

![](https://main.qcloudimg.com/raw/c9ed2cbd95e6b96e00678a1b07e42c08.png)

