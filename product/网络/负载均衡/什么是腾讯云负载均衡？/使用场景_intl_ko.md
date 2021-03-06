CLB는 주로 다음 시나리오에서 적용합니다.

- 응용프로그램 시스템의 서비스 능력을 수평적으로 확장하며 각종 웹 서버와 앱 서버에 적용됩니다.
- 응용프로그램 시스템의 단일 장애점을 제거하며, 일부 CVM 인스턴스가 다운된 뒤에도 응용프로그램 시스템을 정상적으로 작동할 수 있습니다.

다음은 4계층 프로토콜 중(CVM이 공중망에 액세스/클라이언트가 공중망에 액세스) RS 클러스터의 양방향 숨기기의 예제입니다.
![](https://mc.qcloudimg.com/static/img/cd7f959b5cb25840e4bf1207c0c5cfdb/image.png)

CVM(CVM1, CVM2)을 region1의 VPC에 배포하고 공인 IP를 보유하지 않기 때문에 주동적으로 공중망과 통신할 수 없습니다.
- Internet의 리소스가 CVM의 서비스에 접근하였을 때에는 반드시 통일된 CLB 서비스 VIP(115.159.xxx.xxx)를 통해 접근을 진행해야 합니다. 로드밸런서는 모든 요청을 일정한 로드 전략에 따라 RS에 배치되고, Internet이 백 엔드 서버 클러스터에 감지하지 않습니다. RS는 요청을 처리한 뒤, 클라이언트로 반환한 패킷 트래픽도 역시 CLB를 통해 클라이언트에 반환하기 때문에 RS를 효과적으로 숨길 수 있습니다.
- CVM 클러스터가 주동적으로 공중망을 접근해야 할 경우, CLB를 거치지 않습니다. 라우팅 테이블을 구성하고 하나의 Internet 게이트웨이(VM1)로 NAT 포워딩을 진행합니다. Internet 리소스의 경우 요청한 주소는 항상 Internet 게이트웨이의 공인 IP(115.159.111.xxx)이며, Internet의 리소스는 RS 클러스터를 완전히 노출하지 않기 때문에 서버를 숨길 수 있어 백 엔드 서버의 안전성이 향상시킵니다.

## 트래픽 배치
- CLB의 가상 서비스 주소(VIP)와 네트워크 도메인 이름을 설정하여 여러 대의 web 액세스 레이어 서버를 하나의 성능이 좋고 가용성이 높은 액세스 레이어 서비스 풀로 구성합니다. 모든 공중망 요청은 CLB를 통해 진입하면 안전성을 보장하는 동시에 공인 IP 주소를 절약합니다.
- CLB는 모든 요청을 균등하게 각 액세스 레이어 서버로 포워딩합니다. 액세스 레이어 서버는 저렴하고 유사하게 구성된 가상 시스템 또는 Docker 컨테이너로 구성합니다.
![](//mccdn.qcloud.com/static/img/6585e3793ca8a62f369886a0bfb8a95b/image.jpg)

## 수평적으로 확장
- CLB는 Autoscaling 동적 조정 그룹과 결합하여 CVM 인스턴스를 자동으로 생성/릴리스할 수 있습니다. 액세스 레이어 web 서버는 공중망 접근에 대한 스트레스에 따라 조정합니다.
- 전자 상거래 공급업체의 대규모 할인 활동의 경우 웹 방문량은 순간에 10배로 급증하고 불과 몇 시간 동안 지속될 수 있습니다. CLB 및 Autoscaling을 사용하면 IT 비용을 최대적으로 절약할 수 있습니다.
![](//mccdn.qcloud.com/static/img/12c928f0c558e9b5340ae4a6abf6e57c/image.jpg)

## 서비스 분리
- 포럼과 웹사이트 등 전형적인 WEB 서비스의 경우, 웹 개발 및 반복을 쉽게 진행할 수 있도록 , 이미지 서비스, 텍스트 서비스 등 다른 서비스를 분리하는 것을 권장합니다.
- 서비스를 분리한 후, 모든 로드밸런싱 인스턴스 및 백 엔드 관련 서버 그룹은 하나의 독립적인 서비스 클러스터가 됩니다.
- DNS 서비스 제공업체(예: DNSpod)는 여러 개의 A 기록을 추가할 수 있으며 다른 비즈니스 간의 도메인 이름 리디렉션을 실현할 수 있습니다.
- 대형 웹사이트는 일반적으로 수백 개의 비즈니스 서브 모듈을 보유하고 있습니다. CLB 및 DNS 해석을 사용하면 포털 사이트 홈페이지의 접근 주소는 CLB의 1개 공중망 주소 및 자유 도메인 이름 1개로 수렴할 수 있기 때문에 클라이언트의 접근에 도움이 됩니다.
![](//mccdn.qcloud.com/static/img/4ac58aa5cd4385f9316a2099503b911c/image.png)

