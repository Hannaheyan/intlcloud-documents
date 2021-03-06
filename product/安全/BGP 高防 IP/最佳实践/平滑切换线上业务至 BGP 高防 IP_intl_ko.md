

## 사용자 요구
이미 런칭한 비즈니스는 비교적 많은 특정 설정과 제한 조건이 존재할 수 있고, 또한 비즈니스 중단의 영향이 클 수 있습니다. 그렇기 때문에 사용자는 이미 런칭한 비즈니스를 이 제품으로 전환하기 전 가능한 리스크를 피할 수 있도록 본 문서의 관련 권장 사항을 참고하여 적합한 전환 방식을 취하는 것이 좋습니다.

## 권장 사항
>다음 권장 사항은 Tencent Cloud 과거의 온라인 비즈니스 전환 사례에 기초하여 요약한 관련 경험으로서 사용자는 자신의 실제 비즈니스 상황과 결합하여 필요에 따라 보완하고 전환 과정 중 발생할 수 있는 리스크를 최대한 피하십시오.

### 기술 차원
1.	hosts 파일 로컬 수정으로 DNS A 레코드 직접 수정을 대체합니다. 테스트 담당자가 로컬에서 비즈니스를 테스트하며 가용성을 검증하고 대기 시간 등 관련 지표를 테스트합니다.
2.	이미 지능 도메인 이름을 사용하여 제품을 해석했다면, 일부 ISP 또는 지역을 기초로 하여 DNS A 레코드를 수정할 수 있습니다. 우선 일부 트래픽을 Anti-DDoS Advanced IP로 리디렉션하여 베타 테스트를 수행한 뒤 점차적으로 전체 비즈니스 전환 절차를 완료합니다.
3.	DNS의 TTL을 감소합니다. 문제가 발생하면 빠르게 되돌릴 수 있습니다.
4.	롤백 방안을 사전 준비합니다. 문제가 발생하면 롤백 방안에 따라 순서대로 조작할 수 있습니다.

### 비즈니스 차원
1. 백업 비즈니스, 비중요 비즈니스, 비관건 비즈니스를 우선 마이그레이션합니다.
2. 비즈니스가 작은 시간대를 선택해 마이그레이션합니다.

