## Security > Security Advisor > 개요

Security Advisor는 고객이 생성한 NHN Cloud 조직 및 프로젝트 리소스의 보안 설정 상태를 점검하고 권장 가이드 제시하는 서비스입니다. 안전한 클라우드 환경을 위해 권장 가이드를 활용할 수 있습니다.

## 주요 기능
* NHN Cloud 조직의 거버넌스 설정을 점검하고 권장 조치 방법을 적용하여 클라우드 환경의 안전성을 높일 수 있습니다.
* NHN Cloud 프로젝트에 속한 장기 미사용 계정을 점검하고 권장 조치 방법을 안내합니다.
* Security Groups를 점검하여 인스턴스에 적용된 보안 규칙을 확인할 수 있습니다.
* RDS에 대한 접근 설정을 점검하여 불필요한 접근을 차단할 수 있습니다.
* 주기적인 자동 점검 기능을 제공하고 결과를 이메일로 전송할 수 있습니다.

## 점검 대상 및 서비스 리전
### 선택 점검 항목의 프로젝트 항목 점검 대상 리소스
|구분&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|점검 항목|대상 리소스|비고|
|---|---|---|---|
|프로젝트 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |Security Groups 점검|Instance, Security Groups|Database Instance, NKS 클러스터 제외|
|프로젝트|Database Security Groups 점검|Database Instance(MS-SQL Instance, MySQL Instance, PostgreSQL Instance, CUBIRD Instance, MariaDB Instance, Tibero Instance, Redis Instance), Security Groups|
|프로젝트|RDS 접근제어 점검|RDS for MySQL, RDS for MariaDB, RDS for MS-SQL|RDS for MariaDB, RDS for MS-SQL는 판교 리전에서만 서비스 되므로 판교 리전에서만 점검 가능|

### 선택 점검 리전 별 지원 범위
|구분|지원 리전|
|---|---|
|조직으로 구분 된 점검 항목|한국(판교) 리전한국(평촌) 리전일본(도쿄) 리전미국(캘리포니아) 리전|
|프로젝트로 구분 된 점검 항목|한국(판교) 리전한국(평촌) 리전일본(도쿄) 리전|
