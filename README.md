# library-event-metadata

도서관에서 진행되는 강연 및 행사, 프로그램 메타데이터 스키마

대한민국 서울시에 위치하고 있는 도서관에서 운영하는 강연 및 행사, 프로그램 정보를 체계적으로 관리하고 이용자가 편리하게 검색할 수 있도록 공유하기 위해 작성된 'LIBRARY EVENT(LE)' 메타데이터 스키마 결과물입니다. 메타데이터 국제 표준인 더블린 코어(Dublin Core)를 기반으로 확장 설계되었으며 실제 데이터 레코드 검증이 가능하도록 전체 명세와 코드를 공개합니다.

---

### 메타데이터 스키마 서술
전통적인 공공도서관의 메타데이터 환경은 도서나 간행물 등 인쇄 매체 중심의 서지 제어(MARC) 체계에 갇혀 있었다. 그러나 현대의 공공도서관이 지역 사회의 복합 문화 플랫폼으로 진화함에 따라, 매월 수많은 문화 인문학 강연과 체험 프로그램이 동적으로 생산되기 시작하였다. 기존의 고정된 서지 표준으로는 이처럼 가변적이고 맥락적인 '문화 행사 데이터'를 온전하게 기술할 수 없었기에, 파편화된 정보를 통합 관리할 수 있는 도메인 특화형 메타데이터 스키마 설계가 필연적으로 요구되었다.

### 의도된 사용자
본 스키마의 주 이용자는 자치구 내 여러 도서관의 문화 프로그램을 등록하고 취합해야 하는 **'공공도서관 실무 사서'**와 본인에게 필요한 문화 콘텐츠를 직관적으로 탐색하고자 하는 **'지역 주민(이용자)'**이다. 입력자용 가이드라인과 설계 의도를 친절하게 반영한 스키마 구조를 통해 입력자 간의 데이터 불일치 문제를 원천적으로 예방하고 고품질의 데이터를 유지하도록 돕는다.

### 스키마 개발 노트 및 작동 메커니즘
초기 디자인(Draft 1)에서는 도서관 자체의 일반 현황 데이터를 나열하는 관리자 중심의 설계를 구상하였으나, 이는 단순한 정보 수집에 그칠 위험이 있었다. 이에 이용자 중심의 정보 추구 행태를 반영하여 방향성을 전면 수정하였다. 이용자들은 도서 대출 등의 일상적 서비스는 가까운 도서관을 이용하지만, 문화 프로그램은 거리가 멀더라도 찾아가는 특성을 보인다. 따라서 자치구 내 도서관들의 정보를 한곳에 모아 이용자의 탐색 비용을 줄이고 사서들의 홍보 채널을 일원화하도록 스키마를 고도화하였다. 다양한 도서관의 실제 예외 데이터를 입력해 보면서 누락된 요소를 발견하고, 필수(Required)와 선택(Optional) 속성을 실무 맥락에 맞게 유연하게 재조정하여 최종 버전을 완성하였다.

### 이론적 고려사항과 디지털 전환
본 프로젝트의 근저에는 코로나19 팬데믹을 거치며 확립된 도서관 비대면 인프라의 실효성과 정보 격차(Digital Divide)의 패러다임 변화가 깔려 있다. 이제 대학 및 공공 도메인에서의 정보 격차는 자원의 물리적 접근성이 아닌, 생성형 AI와 디지털 자원을 올바르고 윤리적으로 활용하는 리터러시 차원으로 이동하였다. 따라서 본 스키마는 단순 검색 도구를 넘어 연구 윤리, 저작권, 시공간적 운영 제약을 사서가 선제적으로 통제하고 안내할 수 있도록 유기적인 지식 생태계 구조를 지향한다.

---

## 메타데이터 표준

library-event-metadata 스키마는 시스템 간의 원활한 상호운용성을 확보하기 위해 다음과 같은 기존 메타데이터 표준을 결합하여 구현하였습니다.

* **Dublin Core (더블린 코어):** 정보 자원 기술의 글로벌 표준으로서 교차 검색과 시스템 간 데이터 교환의 호환성을 보장하기 위해 핵심 골격으로 채택하였습니다. 자원의 식별자(`dc:identifier`), 명칭(`dc:title`), 상세 내용(`dc:description`), 발행처(`dc:publisher`), 주제어(`dc:subject`), 방식(`dc:format`), 형태(`dc:type`) 등을 범용 표준과 그대로 연동하였습니다.
* **DCMI Metadata Terms (DCTERMS):** 시공간적 범위를 보다 정교하게 통제하기 위해 더블린 코어의 확장 표준을 도입하였습니다. 프로그램이 운영되는 전체 날짜 범위를 선언하기 위해 `dcterms:temporal` 요소를 차용하여 데이터의 정형성을 높였습니다.
* **LIBRARY EVENT (LE) 고유 네임스페이스:** 범용 표준이 담지 못하는 도서관 강연 행사만의 동적 맥락(강사명, 신청 기간, 강의 요일, 운영 시간, 타겟 연령 등)을 완벽히 수용하기 위해 고유 네임스페이스(`xmlns:le`)를 자체 정의하여 결합하였습니다.

---

## 어휘 명세 및 데이터 사전

library-event-metadata 스키마를 구성하는 상위 컨테이너 `programRecord`와 하위 핵심 요소들의 데이터 사전 개요는 다음과 같다.

| 요소명 (Element Name) | 네임스페이스 | 데이터 타입 / 제약 조건 | 필수 여부 | 정의 및 실무 지침 |
| :--- | :--- | :--- | :--- | :--- |
| **dc:identifier** | dc | `xs:string` | 필수 (Required) | 국가 표준 6자리 도서관 부호 입력, 도서관부호 조회 사이트: https://librarian.nl.go.kr/LI/contents/L10404000000.do |
| **dc:publisher** | dc | `xs:string` | 필수 (Required) | 도서관 공식 명칭 (예: 은평구립도서관) |
| **dc:title** | dc | `xs:string` | 필수 (Required) | 프로그램, 강연 및 행사 공식 명칭 |
| **dc:description** | dc | `xs:string` | 필수 (Required) | 프로그램의 주요 운영 내용 기술 |
| **le:instructor** | le | `xs:string` | 선택 (Optional) | 프로그램을 진행하는 강사명 또는 단체명 (다중 입력 가능) |
| **le:appPeriod** | le | `xs:string` | 필수 (Required) | ISO 8601 기간 규격 준수(예: 시작일시/종료일시) yyyy-mm-ddThh:mm |
| **le:operatingSchedule** | le | 복합 타입 (Complex) | 필수 (Required) | 프로그램 운영 일정을 포괄하는 상위 컨테이너 |
| **↳ dcterms:temporal** | dcterms | `xs:string` | 필수 (Required) | 프로그램 실제 운영 시작일과 종료일 |
| **↳ le:Days** | le | `le:dayListType` | 필수 (Required) | [통제어휘 목록] 공백으로 다중 입력 가능한 요일 |
| **↳ le:StartTime** | le | `xs:time` | 필수 (Required) | 24시간제 기준 강의 시작 시간 |
| **↳ le:EndTime** | le | `xs:time` | 선택 (Optional) | 24시간제 기준 종료 시간 (유동적일 경우 생략 가능) |
| **le:sessionCount** | le | `xs:integer` | 필수 (Required) | 프로그램 진행 총 회차 수 |
| **le:venue** | le | `xs:string` | 필수 (Required) | 도서관 내부 운영 장소 명칭 (강의실명) |
| **le:targetAge** | le | `le:targetAgeType` | 필수 (Required) | [통제어휘] 영유아(7세 이하), 아동(초등학생), 청소년(중, 고등학생), 청장년(20세 이상 64세 이하, 노년층(65세 이상) 등 |
| **le:capacity** | le | `xs:integer` | 필수 (Required) | 프로그램 총 모집 인원 수 |
| **le:regMethod** | le | `le:regMethodType` | 필수 (Required) | [통제어휘] 홈페이지 접수, 전화 접수, 현장 접수, 자유 관람 |
| **dc:format** | dc | `le:formatType` | 필수 (Required) | [통제어휘] 온라인, 오프라인, 하이브리드 |
| **le:materials** | le | `xs:string` | 선택 (Optional) | 이용자 지참 준비물 목록 (자유 입력) |
| **le:deptName** | le | `xs:string` | 필수 (Required) | 프로그램 운영 담당 부서명 |
| **le:deptPhone** | le | `xs:string` | 필수 (Required) | 담당 부서 공식 유선 전화번호 |
| **dc:subject** | dc | `xs:string` | 필수 (Required) | 태그 브라우징용 핵심 주제 키워드 (쉼표 구분) |
| **dc:type** | dc | `le:typeType` | 필수 (Required) | [통제어휘] 강연, 특강, 정규강좌, 체험, 전시 등 장르 |

---

## XSD 파일 및 직접 URL

library-event-metadata 규칙과 가이드라인을 정의한 XML 스키마(XSD)의 직접 접근 URL은 다음과 같다. 실무자가 데이터 검증 도구(Validator)를 활용할 때 이 직접 URL을 스키마 로케이션으로 찔러 검증을 수행할 수 있습니다. 파일 내부에는 사서들의 입력 편의를 위한 디자인 의도 주석(`<xs:documentation>`)이 정교하게 포함되어 있습니다.

* **XSD 직접 접근 URL:** [https://536ddwkr.github.io/library-event-metadata/programSchema.xsd](https://536ddwkr.github.io/library-event-metadata/programSchema.xsd)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="[http://www.w3.org/2001/XMLSchema](http://www.w3.org/2001/XMLSchema)"
           targetNamespace="[http://www.example.com/le/elements/](http://www.example.com/le/elements/)"
           xmlns:le="[http://www.example.com/le/elements/](http://www.example.com/le/elements/)"
           xmlns:dc="[http://purl.org/dc/elements/1.1/](http://purl.org/dc/elements/1.1/)"
           xmlns:dcterms="[http://purl.org/dc/terms/](http://purl.org/dc/terms/)"
           elementFormDefault="qualified">

  <xs:import namespace="[http://purl.org/dc/elements/1.1/](http://purl.org/dc/elements/1.1/)" 
             schemaLocation="[https://www.dublincore.org/schemas/xmls/qdc/2008/02/11/dc.xsd](https://www.dublincore.org/schemas/xmls/qdc/2008/02/11/dc.xsd)"/>
  <xs:import namespace="[http://purl.org/dc/terms/](http://purl.org/dc/terms/)" 
             schemaLocation="[https://www.dublincore.org/schemas/xmls/qdc/2008/02/11/dcterms.xsd](https://www.dublincore.org/schemas/xmls/qdc/2008/02/11/dcterms.xsd)"/>

  <xs:simpleType name="dayEnum">
    <xs:restriction base="xs:string">
      <xs:enumeration value="월요일"/>
      <xs:enumeration value="화요일"/>
      <xs:enumeration value="수요일"/>
      <xs:enumeration value="목요일"/>
      <xs:enumeration value="금요일"/>
      <xs:enumeration value="토요일"/>
      <xs:enumeration value="일요일"/>
    </xs:restriction>
  </xs:simpleType>
  
  <xs:simpleType name="dayListType">
    <xs:list itemType="le:dayEnum"/>
  </xs:simpleType>

  <xs:simpleType name="targetAgeType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="영유아(7세 이하)"/>
      <xs:enumeration value="아동(초등학생)"/>
      <xs:enumeration value="청소년(중, 고등학생)"/>
      <xs:enumeration value="청장년(20세 이상 64세 이하)"/>
      <xs:enumeration value="노년층(65세 이상)"/>
      <xs:enumeration value="성인"/> 
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="regMethodType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="홈페이지 접수"/>
      <xs:enumeration value="전화 접수"/>
      <xs:enumeration value="현장 접수"/>
      <xs:enumeration value="자유 관람"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="formatType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="온라인"/>
      <xs:enumeration value="오프라인"/>
      <xs:enumeration value="하이브리드"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="typeType">
    <xs:restriction base="xs:string">
      <xs:enumeration value="강연"/>
      <xs:enumeration value="특강"/>
      <xs:enumeration value="정규강좌"/>
      <xs:enumeration value="체험"/>
      <xs:enumeration value="워크숍"/>
      <xs:enumeration value="독서회/동아리"/>
      <xs:enumeration value="공연"/>
      <xs:enumeration value="전시"/>
      <xs:enumeration value="축제/행사"/>
      <xs:enumeration value="대회/공모전"/>
      <xs:enumeration value="멘토링/상담"/>
      <xs:enumeration value="기타"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:element name="programRecord">
    <xs:complexType>
      <xs:sequence>
        
        <xs:element ref="dc:identifier">
          <xs:annotation>
            <xs:documentation>정의: 도서관부호(6자리) / 설명: 도서관부호 조회 사이트: [https://librarian.nl.go.kr/LI/contents/L10404000000.do](https://librarian.nl.go.kr/LI/contents/L10404000000.do)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element ref="dc:publisher">
          <xs:annotation>
            <xs:documentation>정의: 도서관 공식 명칭 / 설명: 도서관 공식 명칭(예: 은평구립도서관)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element ref="dc:title">
          <xs:annotation>
            <xs:documentation>정의: 프로그램, 강연 및 행사 공식 명칭 / 설명: 프로그램 공식 명칭(예: 도서관 길 위의 인문학)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element ref="dc:description">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 주요 내용 작성 / 설명: 프로그램 운영 내용 작성</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="instructor" type="xs:string" minOccurs="0" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 프로그램을 진행하는 강사명 / 설명: 개인명, 단체명 입력 (선택 사항)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="appPeriod" type="xs:string">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 신청 기간 / 설명: ISO 8601 기간 규격 준수(예: 시작일시/종료일시) yyyy-mm-ddThh:mm</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="operatingSchedule">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 운영 기간 / 설명: 프로그램 운영 일정(기간, 요일, 시간)을 포괄하는 상위 그룹 컨테이너</xs:documentation>
          </xs:annotation>
          <xs:complexType>
            <xs:sequence>
              <xs:element ref="dcterms:temporal">
                <xs:annotation>
                  <xs:documentation>정의: 프로그램 시작일과 종료일 / 설명: 프로그램 시작일과 종료일</xs:documentation>
                </xs:annotation>
              </xs:element>
              <xs:element name="Days" type="le:dayListType">
                <xs:annotation>
                  <xs:documentation>정의: 프로그램 진행되는 요일 / 설명: [통제어휘] 별도 '통제어휘 부록' 시트의 요일 지침 참조</xs:documentation>
                </xs:annotation>
              </xs:element>
              <xs:element name="StartTime" type="xs:time">
                <xs:annotation>
                  <xs:documentation>정의: 프로그램 운영 시작 시간 / 설명: 24시간제 기준 시작 시각(예: 19:00)</xs:documentation>
                </xs:annotation>
              </xs:element>
              <xs:element name="EndTime" type="xs:time" minOccurs="0">
                <xs:annotation>
                  <xs:documentation>정의: 프로그램 운영 종료 시간 / 설명: 24시간제 기준 종료 시각(예: 21:00). 종료 시각이 유동적인 강좌의 경우 생략 가능.</xs:documentation>
                </xs:annotation>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        
        <xs:element name="sessionCount" type="xs:integer">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 운영 횟수 / 설명: 프로그램 진행 총 회차 수 (예: 8)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="venue" type="xs:string" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 운영 장소 명칭(강의실명) / 설명: 도서관 강의실 명칭(예: 다목적실)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="targetAge" type="le:targetAgeType" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 운영 대상 / 설명: [통제어휘] 별도 '통제어휘 부록' 시트의 연령대 분류 지침 참조</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="capacity" type="xs:integer">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 모집 인원 / 설명: 프로그램 모집 인원 수(예: 15)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="regMethod" type="le:regMethodType" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 접수 방식 / 설명: [통제어휘] 별도 '통제어휘 부록' 시트의 접수 방식 지침 참조</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element ref="dc:format">
          <xs:annotation>
            <xs:documentation>정의: 강의 진행 방식 / 설명: [통제어휘] 별도 '통제어휘 부록' 시트의 진행 방식 지침 참조</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="materials" type="xs:string" minOccurs="0" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 이용자 준비물 목록 / 설명: 준비물이 없는 경우 생략 가능 (자유 입력, 예: 개인 노트북, 필기도구)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="deptName" type="xs:string">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 운영 부서명 / 설명: 담당 부서명 (예: 사서과 문화홍보팀)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element name="deptPhone" type="xs:string">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 운영 부서 연락처 / 설명: 지역번호를 포함한 공식 유선번호 (예: 02-2133-0241)</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element ref="dc:subject" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 프로그램 핵심 주제 키워드 / 설명: 핵심 주제를 나타내는 키워드를 자유 입력</xs:documentation>
          </xs:annotation>
        </xs:element>
        
        <xs:element ref="dc:type" maxOccurs="unbounded">
          <xs:annotation>
            <xs:documentation>정의: 프로그램의 본질적인 장르/형태 / 설명: [통제어휘] 별도 '통제어휘 부록' 시트의 프로그램 형식 지침 참조</xs:documentation>
          </xs:annotation>
        </xs:element>
        
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>
