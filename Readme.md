# ABAP Cloud & SAP BTP Basic

> SAP BTP ABAP Environment에서 ABAP Cloud와 RAP(ABAP RESTful Application Programming Model)의 기본 구조를 학습하고 기록하는 저장소입니다.

이 프로젝트는 Travel/Booking 예제를 기반으로 ABAP Cloud 개발 흐름을 단계별로 익히기 위한 학습용 저장소입니다.  
데이터 테이블 생성부터 CDS View, Behavior Definition, Service Definition/Binding, 테스트 데이터 생성까지 RAP 기반 애플리케이션을 구성하는 주요 객체들을 포함하고 있습니다.

## 목차

1. [Title & Intro](#1-title--intro)
2. [학습 목표 및 Roadmap](#2-학습-목표-및-roadmap)
3. [주요 파일에 대한 설명](#3-주요-파일에-대한-설명)
4. [학습자료](#4-학습자료)

---

## 1. Title & Intro

### 프로젝트 소개

**ABAP Cloud & SAP BTP Basic**은 SAP BTP ABAP Environment에서 ABAP Cloud 개발 방식을 학습하기 위한 포트폴리오 및 학습 기록용 프로젝트입니다.

이 저장소에서는 SAP의 Demo Flight/Travel 데이터를 활용하여 다음과 같은 ABAP Cloud 핵심 요소를 다룹니다.

- ABAP Cloud 개발 환경과 abapGit 기반 소스 관리
- RAP 기반 Travel/Booking 비즈니스 오브젝트 구성
- CDS View Entity를 활용한 데이터 모델링
- Managed Behavior Definition과 Draft 처리
- Service Definition 및 Service Binding을 통한 UI/OData 노출
- 테스트 데이터 생성용 ABAP Class 구현

### 기술 스택

| 구분 | 내용 |
| --- | --- |
| Platform | SAP BTP ABAP Environment |
| Language | ABAP Cloud |
| IDE | Eclipse ADT |
| Architecture | RAP Managed Scenario |
| Source Control | GitHub, abapGit |
| Main Domain | Travel / Booking Sample |

---

## 2. 학습 목표 및 Roadmap

### 학습 목표

- SAP BTP ABAP Environment의 개발 흐름을 이해합니다.
- ABAP Cloud에서 허용되는 개발 방식과 객체 구조를 익힙니다.
- RAP의 기본 구성 요소인 CDS View, Behavior Definition, Service Definition의 역할을 이해합니다.
- Travel과 Booking 간의 Root-Child 관계 및 Composition 구조를 학습합니다.
- Draft, ETag, Lock, Authorization 등 RAP 애플리케이션에서 필요한 기본 개념을 실습합니다.
- abapGit을 통해 ABAP 객체를 GitHub 저장소로 관리하는 흐름을 경험합니다.

### Roadmap

| 단계 | 학습 주제 | 주요 내용 | 상태 |
| --- | --- | --- | --- |
| Week 1 | BTP/ADT 환경 구성 | SAP BTP ABAP Environment, Eclipse ADT, abapGit 연결 | 완료 |
| Week 1 | Dictionary Object 이해 | Table, Domain, Data Element 등 기본 객체 생성 | 완료 |
| Week 1 | ABAP Class 기초 | `IF_OO_ADT_CLASSRUN` 기반 콘솔 실행 클래스 작성 | 완료 |
| Week 2 | CDS View Entity | Interface View와 Projection View 구조 이해 | 진행 중 |
| Week 2 | RAP Behavior | Managed Behavior, Draft, Determination 학습 | 진행 중 |
| Week 3 | Service 구성 | Service Definition/Binding으로 OData 서비스 노출 | 예정 |
| Week 3 | Fiori Elements 연동 | Travel/Booking UI 확인 및 개선 | 예정 |
| Week 4 | 정리 및 확장 | 학습 내용 정리, 예외 처리/Validation/Action 추가 | 예정 |

---

## 3. 주요 파일에 대한 설명

### 루트 설정 파일

| 파일 | 설명 |
| --- | --- |
| `.abapgit.xml` | abapGit 저장소 설정 파일입니다. ABAP 객체를 GitHub와 연동하기 위한 메타 정보를 포함합니다. |
| `Readme.md` | 기존 학습 기록 README입니다. 현재 저장소의 학습 진행 상황을 기록하기 위한 파일입니다. |
| `src/package.devc.xml` | ABAP Package 정의 파일입니다. 저장소 내 개발 객체들이 속한 패키지 정보를 관리합니다. |

### 데이터 테이블

| 파일 | 설명 |
| --- | --- |
| `src/zfe_atrav_000168.tabl.xml` | Travel 데이터를 저장하는 주요 테이블입니다. Travel 비즈니스 오브젝트의 Root Entity에 해당합니다. |
| `src/zfe_abook_000168.tabl.xml` | Booking 데이터를 저장하는 테이블입니다. Travel의 Child Entity로 사용됩니다. |
| `src/zfe_dtrav_000168.tabl.xml` | Travel Draft 데이터를 저장하는 Draft 테이블입니다. |
| `src/zfe_dbook_000168.tabl.xml` | Booking Draft 데이터를 저장하는 Draft 테이블입니다. |
| `src/zfe_acarr_000168.tabl.xml` | 항공사(Carrier) 정보를 저장하는 테이블입니다. |
| `src/zfe_aconn_000168.tabl.xml` | 항공편 연결(Connection) 정보를 저장하는 테이블입니다. |
| `src/zfe_aflig_000168.tabl.xml` | 실제 Flight 정보를 저장하는 테이블입니다. |
| `src/zfe_astat_000168.tabl.xml` | Travel 상태값(Open, Accepted, Rejected 등)을 저장하는 테이블입니다. |

### CDS View Entity

| 파일 | 설명 |
| --- | --- |
| `src/zi_fe_travel_000168.ddls.asddls` | Travel Root Interface View입니다. Travel 테이블을 기반으로 Agency, Customer, Currency, Status, Booking과의 Association/Composition을 정의합니다. |
| `src/zi_fe_booking_000168.ddls.asddls` | Booking Interface View입니다. Booking 테이블을 기반으로 Travel, Carrier, Connection, Flight, Customer 등과 연결됩니다. |
| `src/zc_fe_travel_000168.ddls.asddls` | Travel Projection View입니다. UI 및 서비스 노출을 위한 Consumption 계층 View입니다. |
| `src/zc_fe_booking_000168.ddls.asddls` | Booking Projection View입니다. Travel의 하위 Booking 데이터를 UI/서비스 계층에 노출합니다. |
| `src/zi_fe_carr_000168.ddls.asddls` | Carrier 정보를 조회하기 위한 Interface View입니다. |
| `src/zi_fe_conn_000168.ddls.asddls` | Connection 정보를 조회하기 위한 Interface View입니다. |
| `src/zi_fe_flig_000168.ddls.asddls` | Flight 정보를 조회하기 위한 Interface View입니다. |
| `src/zi_fe_stat_000168.ddls.asddls` | Travel 상태값을 조회하기 위한 Interface View입니다. |
| `src/zi_fe_travel_analytics_000168.ddls.asddls` | Travel 데이터를 분석 시나리오로 확장하기 위한 Analytics View입니다. |
| `src/zi_fe_booking_analytics_000168.ddls.asddls` | Booking 데이터를 분석 시나리오로 확장하기 위한 Analytics View입니다. |

### Behavior Definition

| 파일 | 설명 |
| --- | --- |
| `src/zi_fe_travel_000168.bdef.asbdef` | Travel/Booking의 Managed Behavior를 정의합니다. Create, Update, Delete, Draft Action, Determination, ETag, Lock, Authorization 등을 포함합니다. |
| `src/zc_fe_travel_000168.bdef.asbdef` | Projection Behavior Definition입니다. Interface Behavior에서 정의한 기능을 Projection 계층에서 사용할 수 있도록 노출합니다. |

### Behavior Implementation Class

| 파일 | 설명 |
| --- | --- |
| `src/zfe_bp_r_traveltp_000168.clas.abap` | Travel Behavior 구현 클래스입니다. Travel ID 자동 계산 등 Behavior Definition의 Determination 로직을 담당합니다. |
| `src/zfe_bp_r_bookingtp_000168.clas.abap` | Booking Behavior 구현 클래스입니다. Booking ID 자동 계산 등 Booking 관련 Determination 로직을 담당합니다. |
| `src/zfe_bp_r_traveltp_000168.clas.locals_imp.abap` | Travel Behavior 구현에 필요한 로컬 클래스/로직을 포함합니다. |
| `src/zfe_bp_r_bookingtp_000168.clas.locals_imp.abap` | Booking Behavior 구현에 필요한 로컬 클래스/로직을 포함합니다. |

### Service Definition / Binding

| 파일 | 설명 |
| --- | --- |
| `src/zfe_ui_travel_000168.srvd.srvdsrv` | Travel UI 서비스를 정의합니다. Travel, Booking, Connection, Flight, Airline, Currency, Customer Entity를 OData 서비스로 노출합니다. |
| `src/zfe_ui_travel_o4_000168.srvb.xml` | Travel UI 서비스의 OData V4 Service Binding 설정 파일입니다. |
| `src/zui_fe_booking_000168_o2.srvb.xml` | Booking 관련 OData V2 Service Binding 설정 파일입니다. |
| `src/zfe_booking_analytics_000168.srvd.srvdsrv` | Booking Analytics 시나리오를 위한 Service Definition입니다. |

### 데이터 생성 및 실행 클래스

| 파일 | 설명 |
| --- | --- |
| `src/zfe_data_generator_000168.clas.abap` | `/DMO` 샘플 데이터를 기반으로 Travel, Booking, Carrier, Connection, Flight, Status 데이터를 생성하는 클래스입니다. `IF_OO_ADT_CLASSRUN`으로 실행할 수 있습니다. |
| `src/zcl_8668_hello_world.clas.abap` | ABAP Cloud 환경에서 기본 클래스 실행 방식을 확인하기 위한 Hello World 예제입니다. |

---

## 4. 학습자료

아래 영역은 학습 과정에서 참고한 자료를 정리하기 위한 공간입니다.  
링크는 추후 추가 예정입니다.

| 구분 | 제목 | 링크 | 메모 |
| --- | --- | --- | --- |
| SAP 공식 문서 |  |  |  |
| SAP Learning |  |  |  |
| RAP 튜토리얼 |  |  |  |
| ABAP Cloud 참고자료 |  |  |  |
| 기타 블로그/영상 |  |  |  |

---

## 학습 기록 메모

이 저장소는 완성된 제품보다는 **ABAP Cloud와 SAP BTP 개발 흐름을 학습하며 단계별로 쌓아가는 포트폴리오**에 가깝습니다.  
따라서 각 객체가 어떤 역할을 하는지, RAP 구조 안에서 어떻게 연결되는지를 정리하는 데 초점을 두었습니다.

