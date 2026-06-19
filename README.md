# 도서관에서 진행되는 강연 및 행사, 프로그램 메타데이터 스키마

대한민국 서울시에 위치하고 있는 도서관에서 운영하는 강연 및 행사, 프로그램 정보를 체계적으로 관리하고 이용자가 편리하게 검색할 수 있도록 공유하기 위해 작성된 'LIBRARY EVENT(LE)' 메타데이터 스키마 결과물입니다. 메타데이터 국제 표준인 더블린 코어(Dublin Core)를 기반으로 확장 설계되었으며 실제 데이터 레코드 검증이 가능하도록 전체 명세와 코드를 공개합니다.

---

### 메타데이터 필요성
도서관의 메타데이터는 전통적으로 인쇄매체 중심의 서지 제어를 위한 MARC 기반 입력 체계를 중심으로 운영되어 왔습니다. 그러나 최근 도서관은 장서를 통한 정보 제공 기능을 넘어 다양한 강연, 행사, 교육 프로그램 등을 운영하며 지역 주민의 방문을 유도하는 복합문화공간으로 자리매김하고 있습니다. 이러한 콘텐츠는 도서관 방문을 유도하는 요소임에도 불구하고 도서관이 개별 웹사이트를 통해 정보를 제공하고 있어 이용자는 여러 기관의 프로그램을 확인하기 위해 각각의 사이트를 방문해야 하는 불편을 겪고 있습니다. 또한 프로그램 정보가 통일된 메타데이터 규격 없이 등록되어 기관별로 상이한 정보 항목과 표현 방식이 사용되고 있으며 이는 프로그램 정보를 통합적으로 수집·관리·제공하는 데 어려움이 있습니다. 도서관에서 운영하는 강연 및 행사, 프로그램 정보를 일관성 있게 기술하고 공유할 수 있는 표준화된 메타데이터 프레임워크 제공을 통해 분산된 도서관 강연 및 행사, 프로그램 정보를 통합적으로 제공할 수 있도록 제작하였습니다.

### 메타데이터 사용자
도서관 강연 및 행사, 프로그램 메타데이터 스키마의 주된 이용자는 자치구 도서관의 강연 및 행사, 프로그램을 홍보하고 이용자를 모집해야 하는 도서관 사서와 본인에게 필요한 콘텐츠를 한 곳에서 직관적으로 탐색하고자 하는 지역 주민(도서관 이용자)입니다. 

---

## 메타데이터 표준

library-event-metadata 스키마는 시스템 간의 원활한 상호운용성을 확보하기 위해 다음과 같은 기존 메타데이터 표준을 결합하여 구현하였습니다.

* **Dublin Core (더블린 코어):** 정보 자원 기술의 글로벌 표준으로서 교차 검색과 시스템 간 데이터 교환의 호환성을 보장하기 위해 핵심 골격으로 채택하였습니다. 자원의 식별자(`dc:identifier`), 명칭(`dc:title`), 상세 내용(`dc:description`), 발행처(`dc:publisher`), 주제어(`dc:subject`), 방식(`dc:format`), 형태(`dc:type`) 등을 범용 표준과 그대로 연동하였습니다.
* **DCMI Metadata Terms (DCTERMS):** 시공간적 범위를 보다 정교하게 통제하기 위해 더블린 코어의 확장 표준을 도입하였습니다. 프로그램이 운영되는 전체 날짜 범위를 선언하기 위해 `dcterms:temporal` 요소를 차용하여 데이터의 정형성을 높였습니다.
* **LIBRARY EVENT (LE) 고유 네임스페이스:** 범용 표준이 담지 못하는 도서관 강연 행사, 프로그램의 데이터(운영 강사명, 신청 기간, 운영 일정, 운영 요일, 운영 시간(시작, 종료), 운영 횟수, 운영 장소, 운영 대상, 모집 인원, 접수 방법, 준비물, 부서명, 부서연락처 등)를 수용하기 위해 고유 네임스페이스(`xmlns:le`)를 자체 정의하여 결합하였습니다.

---

## 어휘 명세 및 데이터 사전

library-event-metadata 스키마를 구성하는 상위 컨테이너 `programRecord`와 하위 핵심 요소들의 데이터 사전 개요는 다음과 같다.

| 요소명 (Element Name) | 네임스페이스 | 레이블 (Label) | 데이터 타입 / 제약 조건 | 필수 여부 | 반복 여부 | 정의 및 실무 지침 (통제어휘 부록 통합) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **dc:identifier** | dc | 도서관부호 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 국가 표준 6자리 도서관 부호 입력<br>*(도서관부호 조회 사이트: https://librarian.nl.go.kr/LI/contents/L10404000000.do)* |
| **dc:publisher** | dc | 도서관명 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 도서관 공식 명칭 입력 (예: 은평구립도서관) |
| **dc:title** | dc | 프로그램명 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램, 강연 및 행사 공식 명칭 (예: 도서관 길 위의 인문학) |
| **dc:description** | dc | 운영 내용 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램 주요 운영 내용 및 개요 작성 |
| **le:instructor** | le | 운영 강사 | `xs:string` | 선택 (Optional) | 반복 가능 (Repeatable) | 프로그램을 진행하는 강사명 또는 단체명 입력 (개인명, 단체명 입력 가능) |
| **le:appPeriod** | le | 신청 기간 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | ISO 8601 기간 규격 준수 (예: 시작일시/종료일시) `yyyy-mm-ddThh:mm` |
| **le:operatingSchedule** | le | 운영 일정 (Wrapper) | 복합 타입 (Complex) | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램 운영 일정(기간, 요일, 시간)을 포괄하는 상위 그룹 컨테이너 |
| **↳ dcterms:temporal** | dcterms | 운영 기간 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램 실제 운영 시작일과 종료일 입력 |
| **↳ le:Days** | le | 운영 요일 | `le:dayListType` | 필수 (Required) | 반복 불가 (Non-Repeatable) | **[통제어휘]** 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일 중 선택<br>*(주 2회 이상 강좌일 경우 공백으로 다중 입력 가능)* |
| **↳ le:StartTime** | le | 운영 시작 시간 | `xs:time` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 24시간제 기준 강의 시작 시각 입력 (예: `13:00:00`) |
| **↳ le:EndTime** | le | 운영 종료 시간 | `xs:time` | 선택 (Optional) | 반복 불가 (Non-Repeatable) | 24시간제 기준 강의 종료 시각 입력 (예: `17:00:00`) ※ 유동적인 강좌는 생략 가능 |
| **le:sessionCount** | le | 운영 횟수 | `xs:integer` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램 진행 총 회차 수 입력 (예: `4`) |
| **le:venue** | le | 운영 장소 | `xs:string` | 필수 (Required) | 반복 가능 (Repeatable) | 도서관 내부 운영 장소 명칭 및 강의실명 입력 (예: 지하 1층 다목적실) |
| **le:targetAge** | le | 운영 대상 | `le:targetAgeType` | 필수 (Required) | 반복 가능 (Repeatable) | **[통제어휘]** 아래 항목 중 선택하여 입력 (필요시 중복 입력 가능)<br>• `영유아(7세 이하)`, `아동(초등학생)`, `청소년(중, 고등학생)`, `청장년(20세 이상 64세 이하)`, `노년층(65세 이상)` *(실무 실습 시 `성인` 허용)* |
| **le:capacity** | le | 모집 인원 | `xs:integer` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램 총 모집 인원 수 입력 (예: `20`) |
| **le:regMethod** | le | 접수 방법 | `le:regMethodType` | 필수 (Required) | 반복 가능 (Repeatable) | **[통제어휘]** 아래 항목 중 선택하여 입력 (필요시 중복 입력 가능)<br>• `홈페이지 접수`, `전화 접수`, `현장 접수`, `자유 관람` |
| **dc:format** | dc | 진행 방식 | `le:formatType` | 필수 (Required) | 반복 불가 (Non-Repeatable) | **[통제어휘]** 아래 항목 중 단일 선택 입력<br>• `온라인`, `오프라인`, `하이브리드` |
| **le:materials** | le | 준비물 | `xs:string` | 선택 (Optional) | 반복 가능 (Repeatable) | 이용자가 직접 지참해야 하는 준비물 목록 자유 입력 (준비물이 없으면 생략 가능) |
| **le:deptName** | le | 부서명 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 프로그램 운영 담당 부서명 입력 (예: 스마트리움, 문화홍보팀) |
| **le:deptPhone** | le | 부서연락처 | `xs:string` | 필수 (Required) | 반복 불가 (Non-Repeatable) | 담당 부서 공식 유선 전화번호 입력 (예: `02-385-1671`) |
| **dc:subject** | dc | 주제어(키워드) | `xs:string` | 필수 (Required) | 반복 가능 (Repeatable) | 태그 브라우징용 핵심 주제 키워드를 쉼표(,)로 구분하여 자유 입력 (예: 인공지능, 자격증, 드론) |
| **dc:type** | dc | 형식 | `le:typeType` | 필수 (Required) | 반복 가능 (Repeatable) | **[통제어휘]** 아래 항목 중 선택 입력 (필요시 중복 선택 가능)<br>• `강연`, `특강`, `정규강좌`, `체험`, `워크숍`, `독서회/동아리`, `공연`, `전시`, `축제/행사`, `대회/공모전`, `멘토링/상담`, `기타` |

---

## XSD 파일 및 직접 URL

library-event-metadata 규칙과 가이드라인을 정의한 XML 스키마(XSD)의 직접 접근 URL은 다음과 같습니다. 실무자가 데이터 검증 도구를 활용할 때 이 직접 URL을 스키마 로케이션으로 찔러 검증을 수행할 수 있습니다. 파일 내부에는 사서들의 입력 편의를 위한 디자인 의도 주석(`<xs:documentation>`)이 정교하게 포함되어 있습니다.

* **XSD 직접 접근 URL:** [https://536ddwkr.github.io/library-event-metadata/programSchema.xsd](https://536ddwkr.github.io/library-event-metadata/programSchema.xsd)

