# Chapter 09  대규모 테스트 작성

시스템의 모든 부분을 단위 테스트로 수행할 수 없음

억지로 수행하려고 하면, 버그 충분히 찾지 못함. 작성하기 힘듦. 깨지기 쉬움.

- 구성요소가 함께 수행돼야 하는 경우
- 구성요소가 외부 인프라와 통신하는 경우
- 전체 시스템 종단간(E2E) 테스트

## 대규모 테스트 사용 시기

- 개별 클래스 테스트 수행 이후, 전체 동작이 여러 클래스로 구성돼 함께 구동 시 확인하고 싶을 때
- 테스트하려는 클래스가 거대한 아키텍처의 구성요소일 때

### 거대 구성요소에 대한 테스트

- 장바구니, 상품 테스트

### 코드 베이스범위 보다 큰 거대 구성요소 테스트

- CK 테스트 - JDT의 추상구문트리(AST) 기능에 의존. CBO(Coupling Between Objects) 메트릭을 분석하는 테스트
- 앤디 테스트 - 코드 커버리지 테스트

일반적으로 단위 테스트 사용 권장. but, 대규모 테스트가 확신 준다고 믿으면 대규모 테스트 사용.

## 데이터베이스와 SQL 테스트

### SQL에서 테스트 해야하는 것

지금까지 배웠던 테스트 방법론을 적용해봄

- 명세 기반 테스트
- 경계 분석
- 구조적 테스트
- 분기 커버리지
- 조건 + 분기 커버리지
- MC/DC
- 범주-구획 처리
    - 행 검색
    - 행 병합
    - 행 그룹화
    - 행 서브쿼리
    - 값 집계함수 참여
    - 그 외 표현식
- 출력값 검사
- 데이터베이스 제약사항 검사

### SQL 쿼리 자동 테스트

JUnit을 이용한 쿼리 테스트
데이터베이스 연결 설정 -> 데이터베이스 올바른 초깃값 갖도록 설정 -> SQL 쿼리 수행 -> 출력 검사

### SQL 테스트를 위한 인프라 설정

- 데이터베이스 연결 열기
- 트랜잭션 열고 커밋하기 - ex) 커밋하지 않고 테스트 후 롤백
- 데이터베이스의 상태를 재설정 - ex) 테스트 시작전 테이블 모두 지우기 등
- 테스트 코드양을 도와주는 도우미(헬퍼) 메서드 - 코드 재활용할 수 있다면 메서드 추출해서 부모 클래스로 옮겨 상속 받아 사용하기

### 모범 사례

- 테스트 데이터 생성기 사용 - 10장의 테스트 데이터 생성기
- 단언 API를 잘만들어서 재활용 - 여러 테스트에서 필요한 단언문은 캡슐화하는 유틸리티 메서드를 만들기
- 필요한 데이터는 최소화 - 너무 많은 데이터 입력하지 말기
- 스키마의 변화를 고려 - 미래의 스키마 변경이 테스트를 깨뜨릴 것 같다면 변경점 줄이는 방법 고려. 플라이웨이, 리퀴베이스등 마이그레이션 프레임워크 사용.
- 인메모리 DB 고려 - 실제 DB는 너무 costly

## 시스템 테스트

### 셀레늄

-> 셀레늄 IDE 쓰면 어떨까

#### 패턴과 모범사례

- 웹 테스트에 필요한 상태로 시스템을 설정할 수 있는 방법 제공
- 각 테스트가 항상 깨끗한 환경에서 실행되는지 확인
- HTML 요소에 의미있는 이름을 지정
- 여정을 테스트하는 경우에만 여정의 모든 단계 방문
- 단언문은 PO에서 가져온 데이터를 사용해야
- 테스트 스위트에 중요한 설정값을 전달
- 여러 브라우저에서 테스트 수행

## 마지막 논의

### 테스트 수준

- 모든 것을 단위 수준에서 수행 후, 대규모 테스트에서는 가장 중요한 행위 수행

### 비용/이득 분석

- 테스트 작성 비용, 실행 비용, 이득, 잡을 수 있는 버그 등 고려

### 수행은 됐지만 테스트 안 된 메서드 조심

- 의사 테스트 메서드: 테스트 과정에서 수행되지만 전체 구현을 단순하게 대체해도 테스트는 여전히 통과하는 것
- 의사 테스트 메서드에 주의 -> 단위 테스트와 대규모 테스트 모두 옹호

### 적합한 코드 인프라가 핵심

- 통합 테스트와 시스템 테스트는 둘다 적절한 인프라 필요
    - 적절한 인프라 없으면 단언하는 일에 너무 많은 시간 들임

### DSL과 테스트를 작성하는 이해 관계자를 위한 도구

- 로봇 프레임워크
- 큐컴버

### 다른 종류의 웹 시스템에 대한 테스트

- 리액트, 몽고 등 다른 기술의 웹 시스트 테스트 -> 해당 공동체 방문하여 탐색
- 웹 앱 이외 ex) 모바일 앱에 도 마찬가지로 시스템 테스트 적용 가능
