# 🚀 ABAP Cloud & BTP Learning Journey

> SAP BTP 환경에서의 ABAP Cloud 학습 및 프로젝트 기록입니다.

---

## 📅 주차별 학습 현황
| 주차 | 주제 | 상태 |
| :--- | :--- | :--- |
| **Week 1** | BTP 환경 구축 및 기초 Object 생성 | ✅ 완료 |
| **Week 2** | ABAP Cloud 문법 심화 (예정) | ⏳ 진행중 |

---

## 🛠️ 개발 환경 (Environment)
* **IDE:** Eclipse ADT
* **Platform:** SAP BTP ABAP Environment
* **Language Version:** `ABAP Cloud`

## 🔑 이번 주 핵심 요약 (Week 1)
### 1. Dictionary & Objects
* **Database Table:** 클라우드 표준에 맞는 테이블 설계
* **Domain & Data Element:** 재사용성을 고려한 데이터 정의

### 2. ABAP Class 실습
클라우드 환경에서는 `WRITE` 구문 대신 콘솔 출력을 사용합니다.
```abap
CLASS zcl_hello_world DEFINITION PUBLIC FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_oo_adt_classrun.
ENDCLASS.

CLASS zcl_hello_world IMPLEMENTATION.
  METHOD if_oo_adt_classrun~main.
    out->write( 'Hello ABAP Cloud!' ).
  ENDMETHOD.
ENDCLASS.
