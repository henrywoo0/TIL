# 기말고사와 함께하는 DATABASE (MySQL)

대구소프트웨어마이스터고에서 2021학년도 2학기 기말고사 데이터베이스 과목을 대비하기 위해 정리한 내용입니다.

## 데이터

- `Data(자료)` : 관찰, 검색, 측정을 통해 수집되는 사실이나 값
- `정보` : 자료의 유효한 해석, 지식
- `일괄 처리 시스템` : 데이터를 수집, 분류, 정렬한 다음 **일괄 처리**하는 데이터 처리 방법
- `온라인 처리 시스템` : 데이터가 생성되는 **즉시 전송**, 컴퓨터가 **즉시 처리** (하나의 DB에서 처리)
- `분산 처리 시스템` : **여러 데이터베이스**에서 처리, 통신 네트워크로 공유 (온라인 처리보다 효율적)
- `데이터베이스` : 여러 응용 시스템들이 공용할 수 있도록 **통합 저장된 운영 데이터**

### 데이터베이스 정의 (SISO)

- `저장 데이터` (Stored Data) : 문서 보관이 아닌 **하드디스크**나 **서버**에 저장된 데이터를 의미
- `통합 데이터` (Integrated Data) : 여러 곳에서 사용하던 **데이터를 통합**, 하나의 저장된 데이터를 의미 (데이터 중복)
- `공용 데이터` (Shared Data) : 여러 사용자들이 서로 다른 목적으로 데이터를 공동 이용 (데이터 양 대규모화)
- `운영 데이터` (Operational Data) : **조직의 목적**을 위해 사용되는 데이터를 의미 (임시 데이터는 운영데이터 X)

### 데이터베이스 특성 (RCCC)

- `실시간 접근성` (real-time accessibility) : DB는 **실시간으로 서비스**함. 사용자의 요청에 즉시 응답
- `계속적인 변화` (continuous evolution) : 데이터는 **계속 바뀜**. 삽입과 삭제, 수정 등의 작업으로 바뀐 값 저장
- `동시 공용` (concurrent sharing) : 서로 다른 사용자에게 **동시 공유** (여기서 생기는 문제를 해결하기 위해 종속성, 중복성 해결)
- `내용에 의한 참조` (contents reference) : 주소가 아닌 **데이터 값 참조**. 쿼리를 제시하면 DB는 데이터 검색해서 보내줌

## 파일 시스템 (not DBMS)

- `파일 시스템` : 각각 응용 프로그램이 독립적으로 자료를 **파일 형태로 관리**
- `데이터 중복성` : 시스템 내 자료가 **중복 저장**되어 비용 증가(비효율적). 응용 프로그램마다 별도로 독립된 파일 때문
- `데이터 종속성` : 자료 간의 상호 의존도가 높아서 하나의 파일 변경 시 관련 파일도 변경해야 함

### DBMS의 장점

- 데이터를 공유하기 때문에 **종속성 문제 해결**
- 중복 제거로 데이터 **일관성 유지**
- 데이터 **복구**, **보안**이 쉬움
- 하나의 갱신 작업만 수행하면 되어서 **효율적**

### DBMS의 단점

- DBMS, CPU, 메모리 용량 등 **비용 발생**
- **복잡한** 백업과 회복 (처음부터 잘 해야함)
- 시스템 **취약성** (DB 공격당하면 끝)

### DBMS의 기능

- `데이터 정의` (DDL) : **데이터의 구조** 정의 및 데이터 구조에 대한 삭제, 변경 수행 (CREATE, ALTER, DROP)
- `데이터 조작` (DML) : 데이터의 검색, 삽입, 수정, 삭제 작업 지원 (SELECT, INSERT, DELETE, UPDATE) 
- `데이터 제어` (DCL) : 데이터베이스 사용자 생성, 모니터링, 접근 제어 (백업과 회복, 동시성 제어) (GRANT, REVOKE)

### DBMS 사용자

- `일반 사용자` : 데이터의 검색, 삽입, 수정 작업 하는 사람 (서비스에서 클릭만으로 조회하는 사람)ㅔ
- `응용프로그래머` : 일반 사용자가 사용 가능하도록 **프로그램 만드는 사람** (SQL 번역, DBMS 접근 도와줌)
- `DBA` (DataBase Administrator) : DB 총괄 책임자. 데이터 설계, 구현, 유지보수 전 과정 담당

||SQL 언어|프로그래밍 언어|DBMS 지식|데이터 구성|
|-|-------|-------------|---------|----------|
|일반 사용자|X|X|X|X|
|응용프로그래머|O|X|O|O|
|DBA|O|O|O|O|

## 스키마 (Schema)

- `스키마` : 데이터베이스 구조와 제약 조건에 관해 명세
- `내부 스키마` : 물리적 저장 위치에 데이터베이스의 저장 위치 명세
- `개념 스키마` : 전체 데이터베이스의 정의. (하나만 존재)
- `외부 스키마` : 각 사용자, 응용프로그래머가 각자 필요한 논리적 구조 정의 (=뷰)

## 릴레이션 (Relation)

- `릴레이션` : 테이블(표)
- `릴레이션 스키마` : 속성들의 집합
- `릴레이션 인스턴스` : 데이터들의 집합
- `차수` : 속성(애트리뷰트)의 개수
- `카디널리티` : 튜플의 개수
- `도메인` : 속성들이 가질 수 있는 값들의 집합

![image](https://user-images.githubusercontent.com/80818534/144735896-c1769a7a-4070-4406-8406-9978a6ec71aa.png)

## 키 (Key)

- `Key` : 키를 이용해 특정 튜플을 식별할 때 사용하는 속성
- `Super Key` (슈퍼키) : 튜플을 유일하게 식별할 수 있는 속성 집합
- `Candidate Key` (후보키) : 튜플을 유일하게 식별할 수 있는 속성의 **최소 집합**
- `Primary Key` (기본키) : 여러 후보키 중 하나를 선정하여 사용하는 대표키
- `Alternate Key` (대체키) : 기본키를 제외한 나머지 후보키
- `Foreign Key` (외래키) : 다른 릴레이션 참조 시 참조하는 기본키

### 기본키 (Primary Key)

- 후보키 중 하나 선택 (신중하게 선택해야 함)
- 튜플을 식별할 수 있는 고유한 값
- NULL값 허용하지 않음
- 키 값 변동 X
- 최대한 적은 수의 속성을 가진 것

## 무결성 제약조건

- `도메인 무결성 제약조건` : 각 애트리뷰트들의 도메인에 지정된 값만을 가져야 한다는 조건. Type, Null, Default, Check 등을 사용하여 지정
- `개체 무결성 제약조건` : 기본키의 조건을 지켜야 한다는 제약 조건 (튜플 식별 가능한 고유값, NULL X, 값 변동 X, 최대한 적은 수의 속성)
- `참조 무결성 제약조건` : 외래키의 조건을 지켜야 한다는 제약 조건 (부모 릴레이션 기본키 그대로 사용. 다른 값을 삽입, 수정할 때 거부)
- 참조 무결성 제약조건에서 옵션 붙음 (RESTRICTED(거부), CASCADE(연쇄), DEFAULT(초깃값), NULL)

|구분|도메인 무결성 제약조건|개체 무결성 제약조건|참조 무결성 제약조건|
|---|---------------------|------------------|-------------------|
|제약 대상|속성|튜플|속성과 튜플|
|같은 용어|도메인 제약|기본키 제약|외래키 제약|
|해당 키|-|기본키|외래키|
|NULL값 허용 여부|허용|불가|허용|
|릴레이션 내 제약조건의 개수|속성 개수와 동일|1개|0~여러 개|
|기타|튜플 삽입/수정 시 제약 사항 우선 확인|튜플 삽입/수정 시 제약 사항 우선 확인|튜플 삽입/수정 시 제약 사항 우선 확인|

## 관계대수

- `관계대수` : 관계형 DB 내에서 원하는 정보를 어떻게 찾아낼지 기술하는 절차적 언어
- `셀렉트(σ)` : 릴레이션에서 주어진 조건에 만족하는 튜플 찾는 연산자 (시그마라고도 읽음) (NULL 결과값은 나타내지 않음)
- `프로젝트(π)` : 필요한 속성들만 추출하는 연산 (중복 제거!)
- `디비전(÷)` : 2개의 릴레이션에서 피연산 릴레이션의 속성값을 모두 가진 연산 릴레이션의 속성을 제외한 속성만을 구하는 연산
- `합집합(∪)` : 두 릴레이션을 합하여 하나의 릴레이션으로 반환 (중복 제거!)
- `교집합(∩)` : 두 릴레이션에 모두 속한 튜플들로 이루어진 릴레이션
- `차집합(-)` : 피연산 릴레이션에 속하지 않은 튜플들로 이루어진 릴레이션
- `카티션 프로덕트(X)` : 연산 릴레이션과 피연산 릴레이션 곱하는 것 (중복 허용)

![image](https://user-images.githubusercontent.com/80818534/144736342-107d3eb3-9c0f-4f2c-b820-b72ea713faed.png)
![image](https://user-images.githubusercontent.com/80818534/144736412-84da0d7a-bc8b-4f58-a6da-fdc02cee085e.png)
![image](https://user-images.githubusercontent.com/80818534/144736826-cdf0caaf-39fd-4d60-b9f6-dee0df27f156.png)
![image](https://user-images.githubusercontent.com/80818534/144736847-62dadf00-adf1-4994-aea5-5881d22720b2.png)
![image](https://user-images.githubusercontent.com/80818534/144736888-aa8a6047-d86f-4ab4-98f3-4e813767b574.png)
![image](https://user-images.githubusercontent.com/80818534/144736935-5adfc403-db67-40e2-b2ba-f175dd698cd7.png)
![image](https://user-images.githubusercontent.com/80818534/144736963-bdb9c0e5-c8a6-4237-9330-365983f613c2.png)

- 카티션 프로덕트를 하면 매우 많은 튜플 생성. 그러므로 필요한 자료만 보기 위해 `조인` 사용
- `동등조인(⋈)` : 양쪽 테이블에서 조인 조건(=)이 일치하는 행만 조인
- `자연조인(⋈N)` : 동등 조인 결과로 얻어진 불필요한 애트리뷰트 제외한 조인 (중복 애트리뷰트 제거)
- `세타조인(⋈θ)` : 조인 연산 시 조건이 붙는 조인 (<, >, =, <>, <=, >=)
- `세미조인` : 자연조인 후, 두 릴레이션 중 한쪽 릴레이션 결과만 반환 (기호가 닫힌 쪽 튜플만)
- `외부조인` : 조인 연산 시 외부조인 하는 릴레이션의 정보를 버리지 않고 보여줌 (꼭 필요한 정보를 남겨두기 위해 사용, 없는 곳은 NULL 처리)

![image](https://user-images.githubusercontent.com/80818534/144737051-f1451e9e-fcdc-45e2-9cd2-086be69694da.png)
![image](https://user-images.githubusercontent.com/80818534/144737012-b5ad38ca-2bf3-42ce-bc5f-89b29d66400e.png)
![image](https://user-images.githubusercontent.com/80818534/144737463-e4ce5944-5361-4765-a10d-457c60468c6d.png)
![image](https://user-images.githubusercontent.com/80818534/144737524-24f9a107-275d-457f-8bbf-7d8386f7e120.png)
![image](https://user-images.githubusercontent.com/80818534/144737528-f313252d-93b5-42b2-aa64-745e3773d386.png)

## MySQL의 자료형

- `INT` : 정수형 4byte
- `BIGINT` : 정수형 8byte
- `FLOAT` : 실수형 4byte
- `DOUBLE` : 실수형 8byte
- `CHAR` : 고정 길이 문자열 (~255개)
- `VARCHAR` : 가변 길이 문자열 (~255개)

![image](https://user-images.githubusercontent.com/80818534/144737614-dbb6756a-f9f6-4d80-b135-4e9d90405111.png)

## DDL (Data Definition Language)

- `CREATE` : 테이블 생성
- `ALTER` : 테이블 수정
- `DROP` : 테이블 삭제

아래는 CREATE문의 예제이다.
```sql
CREATE TABLE user (
  id bigint(20) NOT NULL,
  email varchar(40) NOT NULL,
  username varchar(15) NOT NULL,
  password varchar(100) NOT NULL,
  PRIMARY KEY (id)
);
```

- `ALTER`을 활용하여 테이블을 수정할 수 있다.
- 애트리뷰트 자료형 수정 : `ALTER TABLE user MODIFY username varchar(100)`
- 애트리뷰트 추가 : `ALTER TABLE user ADD birthday datetime`
- 애트리뷰트 맨앞에 추가 : `ALTER TABLE user ADD birthday datetime first`
- 애트리뷰트 이름 변경 : `ALTER TABLE user CHANGE birthday birthdate datetime`
- 애트리뷰트 제거 : `ALTER TABLE user drop birthdate`

아래는 DROP문으로 테이블을 삭제하는 예제이다.
```sql
DROP TABLE user;
```

## Foreign Key

- Foreign key(외래키) 조건이 붙는 이유 : 변경/삭제 시 문제점 발견
- 아래는 Foreign key(외래키) 조건 사용법
- REFERENCES 테이블 이름(애트리뷰트)
- `ON DELETE` : 삭제 시 조건
- `ON UPDATE` : 수정 시 조건
- 아래는 위 조건문에 들어갈 키워드이다.
- `RESTRICT` : 변경/삭제 경우 연산 취소
- `CASCADE` : 변경/삭제 경우 함께 변경/삭제
- `NO ACTION` : restrict와 동일하게 동작
- `SET NULL` : 부모 릴레이션에서 값 변경/삭제 시 자식 릴레이션 값 NULL로 세팅

```sql
FOREIGN KEY 고객번호 REFERENCES 고객(고객번호) ON DELETE SET NULL ON UPDATE CASCADE
```

![image](https://user-images.githubusercontent.com/80818534/144737956-434dd056-6ae9-4b9b-acf4-ba21cfe32ea3.png)

## DML (Data Manipulation Language)

- `SELECT` : 데이터 조회 (from, where, group by, having, order by)
- `INSERT` : 데이터 삽입
- `UPDATE` : 데이터 수정
- `DELETE` : 데이터 삭제

SELECT 조회 예시
```sql
SELECT * FROM reservation WHERE name = '홍길동';
```

SELECT 중복 제거 예시
```sql
SELECT DISTINCT name FROM reservation;
```

SELECT 내림차순 예시
```sql
SELECT * FROM reservation ORDER BY reservationdate DESC;
```

SELECT 별칭 부여 예시 (AS는 생략 가능)
```sql
SELECT reservationdate, CONCAT(RoomNum, ':', Name) AS ReserveInfo FROM reservation;
```
INSERT 예시
```sql
INSERT INTO reservation(ID, Name) VALUES (6, '김유신');
```

UPDATE 예시
```sql
UPDATE reservation SET RoomNum = 2002 WHERE Name = '홍길동';
```

DELETE 예시
```sql
DELETE FROM reservation WHERE Name = '홍길동';
```

- `Having` : WHERE과 비슷한 개념이지만, 집계 함수에 대해서 조건을 제한하는 것 (꼭 GROUP BY 다음에 나와야 함)
- `ROLLUP` : 총합 또는 중간 합계가 필요할 경우 사용. GROUP BY 절과 함께 `WITH ROLLUP`문 사용

![image](https://user-images.githubusercontent.com/80818534/144738472-39514e6a-8b25-4188-ab9b-1e854fb6b997.png)

## JOIN

INNER JOIN 방법
```sql
SELECT 애트리뷰트명 FROM 테이블명 INNER JOIN 조인할 테이블 ON 조인에 사용될 애트리뷰트 조건;
```

NATURAL JOIN 사용 방법
```sql
SELECT 애트리뷰트명 FROM 테이블명 NATURAL JOIN 조인할 테이블;
```

- 자연 조인 시 조인에 참여하는 애트리뷰트 중 **이름이 같은 모든 애트리뷰트**를 활용하여 조인
- 동등조인과 차이점은 **중복 애트리뷰트 하나만 출력**한다는 점
- 조인에 사용될 애트리뷰트를 미리 확인해야 함 (조건이 없음)

OUTER JOIN 사용 방법
```sql
SELECT 애트리뷰트명 FROM 테이블명 OUTER JOIN 조인할 테이블 ON 애트리뷰트=애트리뷰트;
```

- 조인 연산 시 외부조인하는 릴레이션의 정보를 버리지 않고 보여줌
- 꼭 필요한 정보를 남겨두기 위해 사용
- 해당 정보가 없는 곳은 `NULL`값 채움
- 외부 조인 시 조건 꼭 명시

LEFT OUTER JOIN 예제
```sql
SELECT * FROM aaa LEFT OUTER JOIN bbb ON aaa.b = bbb.B;
```

RIGHT OUTER JOIN 예제
```sql
SELECT * FROM aaa RIGHT OUTER JOIN bbb ON aaa.b = bbb.B;
```

- MySQL에서 FULL OUTER JOIN은 작동하지 않음.
- FULL OUTER JOIN 사용하려면 UNION 활용하기



