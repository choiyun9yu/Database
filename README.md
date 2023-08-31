# Database

## 1. MySQL
### 1-1. 계정 관리

	# 로그인
 	MYSQL -h(호스트명) -u(계정명) -p(비밀번호) 

	# 계정 확인
	USE MYSQL; 
	SHOW TABLES;
	SELECT HOST, USER,PASSWORD FORM USER;

	# 계정 생성
	CREATE USER (계정명)@(접속위치) 
	IDENTIFITED BY (비밀번호);

	# 권한 부여
	GRANGT ALL PRIVILEGES ON (DB명).* TO (계정명)@(접속위치) 
	IDENTIFITED BY 비밀번호;

	# 계정 삭제
	DROP USER (계정명)@(접속위치);

### 1-2. 데이터베이스 관리

	# 데이터베이스 조회
	SHOW DATABASES;

	# 데이터베이스 생성
	CRATE DATABASE (DB명);

	# 데이터베이스 삭제
   	DROP DATABASE (DB명);

	# 데이터베이스 접속
    	USE DB;

### 1-3. 테이블 관리
	# 테이블 목록 조회
    	SHOW TABLES;

	# 테이블 스키마 조회
	DESC (테이블명);
	
	# 테이블 출력 길이 조절
	OLUMN (컬럼명) FORMAT (A20);

       
## 2. Oracle
### 2-1. 계정관리

	# 로그인
	SQLPLUS (enter)
	USER-NAME : sys as sysdba (enter)
	PASSWORD : (enter, enter)

	# 계정 확인
	SELECT * FROM ALL_USERS;

	# 계정 생성
    	CREATE USER (계정명) 
    	IDENTIFIED BY (비밀번호);

	# 권한 부여
	GRANT CONNECT, RESOURCE, DBA TO (계정명);
	COMMIT;

	# 계정 삭제
	DROP DATABASE (DB명); 

	# 계정 연결
	conn 유저/비번;  ex)hr/hr

	# 언락(시스템 계정에서)
	ALTER USER USER (계정명) ACCOUNT UNLOCK
	IDENTIFITED BY (비밀번호) // 비밀번호 바꾸는 것

### 2-2. 데이터 베이스 관리

### 2-3. 테이블 관리

	# 테이블 목록 조회
	SELECT * FROM TAB;

	# 테이블 스키마 조회
	DESC (테이블명);
	
	# 테이블 출력 길이 조절
	COLUMN (컬럼명) FORMAT (A20);


## 3. DML
### 3-1. SELECT
	SELECT (조회할 칼럼)
	FROM (조회할 테이블)
	WHERE (조회 조건)
	GROUBP BY ('00별'로 묶을 칼럼)
	HAVING (그룹 바이의 조건)
	ORDER BY (정렬 조건)

	# SELECT
	SELECT 칼럼명 FROM 테이블명;
	// 명령문이나 절 뒤에 숫자가 나오면 데이터로 인식하고, 문자가 오면 컬럼명으로 인식한다.
	// '문자'나 '날짜'로 쓰고 싶으면 반드시 ''(홑따옴표)로 묶어줘야 한다.

	# 별칭설정 : AS
	SELECT 칼럼명 AS 별칭 FROM 테이블명;  // " "(쌍따옴표)로 묵으면 대문자 소분자 포맷 그대로 출력!!

	# 중복제거 : DISTINCT
	SELECT DISTINCT 칼럼명 FORM 테이블명;

	#연결연산자로 'str' 삽입 : || 
	SELECT 칼럼명1 || 'str' || 칼럼명2 FROM 테이블명;
	>> 칼러명1 str 칼럼명2 
------------------------------------------------------------------------------------------------------

#### WHERE
	# ex1 
 	SELECT last_name, 12*salary AS annsal 
	FROM employees 
	WHERE 12*salary >= 120000;  // 조회 됨

	# ex2 
 	SELECT last_name, 12*salary AS annsal 
	FROM employees 
	WHERE annsal >= 120000;  // 조회 안됨
	// 조회 안되는 이유 : FROM > WHERE > SELECT > ORDER BY 순서로 동작해서 SLELECT절 별칭은 WHERE절에서 못쓴다.  

	# 비교 연산자
		부등호 관계 : != , <>
		등호 관계 : =
		대소 관계 : >, <, >=, <= 

	# 비교 조건 연산자
	// BETWEEN A AND B : A이상 B이하 조회
	SELECT 칼럼명 
	ROM 테이블명 
	WHERE 칼럼명 BETWEEN 하한 AND 상한;

	// IN : 나열된 값중 하나라도 포함하면 조회
	SELECT 칼럼명
	FROM 테이블명
	WHERE 칼럼명 IN (A, B, C);

	// LIKE : 문자패턴 조건으로 조회
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 = ' ';  // ' '는 대소문자를 정확히 입력해줘야한다.
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 like 'K%';  // 대문자 'K'로 시작하는 데이터 조회
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 like '%r';  // 소문자 'r'로 끝나는 데이터 조회    
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 like '%o%'; // 중간에 '0'들어간 데이터 조회
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 like '%';   // 전부다 조회
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 like 'K___';  // 언더바는 내가 모르는 1자리 ()	
	SELECT 칼럼명 FROM 테이블명 WHERE 칼럼명 like '_o%';  // 두번째 칸이 'o'인 데이터 조회

	// IS NULL : null 값 검색
	SELECT 칼럼명
	FROM 테이블명
	WHERE 칼럼명 IS NULL;

	// NVL(칼럼명, N) : null이면 N로 출력
	SELECT NVL(칼럼명, N)
	FROM 테이블명;

	// NVL2(칼럼명, M, N) : not null이면 M으로 출력, null이면 N으로 출력
	SELECT NVL2(칼럼명, M, N)
	FROM 테이블명;

	# 논리 조건 연산자(null 값은 연산되지 않는다.)
		AND : 연언
		OR : 선언
		NOT : 부정
			NOT BETWEEN A AND B
			NOT IN
			NOT LIKE
			IS NOT NULL

	// 연산자 우선순위 : NOT > AND > OR  // 범위 좁히는 순서, 만약 먼저하고 싶으면 괄호로 묶으면 된다.
------------------------------------------------------------------------------------------------------

#### GROUBP BY
	# ex
 	SELECT department_id, job_id  
	FROM employees
	GROUBP BY department_id;  // 부서ID별로 조회

	# 집계 함수 : 그룹 당 하나의 결과를 출력, NULL 값은 무시하고 연산한다. 
		합계 : SUM() 
		평균 : AVG()
		최대값 : MAX()
		최소값 : MIN()
		카운트 : COUNT()  // 행의 갯수를 카운트, 뭘 넣어도 상관없어서 count(*) 많이 쓰는펀 (카운트는 *도 카운트)
		분산 : VARIANCE()
		표준편차 : STDDEV()

	# ex 
   	SELEC MIN(salary) 
	FROM (employees) 
	WHERE manager_id IS NOT NULL 
	GROUP BY manager_id 
	HAVING MIN(salary) >= 5000;

	// select절에서 집계함수 적용된 칼럼과 having절 조건 걸린 칼럼이 일치해야한다.
------------------------------------------------------------------------------------------------------

#### ORDER BY

	오름차순 : SELECT 칼럼명 FROM 테이블명 ORDER BY;
	내림차순 : SELECT 칼럼명 FROM 테이블명 ORDER BY DESC;
------------------------------------------------------------------------------------------------------

#### LIMMIT
limit 절 <> rownum (서브쿼리로 오덜바이 해주고 rownum)  
LIMIT는 쿼리가 ORDER BY 절까지 모두 실행 후 해당 결과에서 원하는 행의 데이터를 가져오는 것이며, ROWNUM은 쿼리가 완전히 수행되지 않은 원 데이터의 정렬순서대로 번호를 매기기 때문에 전혀 다른 결과가 출력된다.  
오라클에서 LIMIT와 동일한 결과를 얻기 위해서는 SELECT절로 한번 감싼후에 ROWNUM으로 조건을 주면 LIMIT와 동일한 결과가 출력된다.

	select name
	from (select * from animal_ins order by datetime)
	where rownum=1;



	SELECT o.ANIMAL_ID, o.ANIMAL_TYPE, o.NAME 
	from ANIMAL_INS i, ANIMAL_OUTS o 
	where i.ANIMAL_ID = o.ANIMAL_ID
	and i.SEX_UPON_INTAKE like in('Intact%') 
	and (o.SEX_UPON_OUTCOME like in('Spayed%') or o.SEX_UPON_OUTCOME like ('Neutered%'));


	select i.NAME, i.DATETIME from (SELECT i.NAME, i.DATETIME, o.DATETIME 
	from ANIMAL_INS i, ANIMAL_OUTS o 
	where i.ANIMAL_ID = o.ANIMAL_ID(+) order by 2)
	where rownum =1;
-----------------------------------------------------------------------------------------------------------

### 3-2. INSERT
	INSERT INTO 테이블명 VALUES('데이터1', '데이터2', '데이터3');  //  COLUMNS 명시안하면 전체 칼럼에 값 입력해줘야함
	INSERT INTO 테이블명 COLUMNS(칼럼명1, 칼럼명3) VALUES(데이터1, 데이터3);
	INSERT INTO 테이블명 select문;  // 조회 데이터를 삽입 (단, 칼럼수가 같아야 한다)
----------------------------------------------------------------------------------------------------------
### 3-3. UPDATE

	UPDATE 테이블명
	SET 칼럼명 = 데이터
	WHERE절;  // 조건 입력 안하면 테이블 전체가 다 수정되니 수정할 조건을 입력해줘야한다.


    병행제어
	-로킹
	-타임스탬프
	-낙관적 병행제어
	-다중버전 병행제어
	  (연쇄복귀?) : 두개 이상의 Transaction이 수행되던중 한개의 Transaction이 취소될 때 나머지 다른 Transaction도 연쇄적으로 취소되는 현상
	  두 트랜잭션이 동일한 데이터 내용을 접근할 때 발생
	  한 트랜잭션이 데이터를 갱신한 다음 실패하여 Rollback 연산을 수행하는 과정에서 갱신과 Rollback 연산을 실행하고 있는 사이에 
	  해당 데이터를 읽어서 사용할 때 발생할 수 있는 문제
	  같은 자원을 사용하는 두개의 트랜잭션 중 한 개의 트랜잭션이 성공적으로 일을 수행하였다 하더라도 
	  다른 트랜잭션이 처리하는 과정에서 실패하게 되면 두 개의 트랜잭션 모두가 복귀되는 현상
----------------------------------------------------------------------------------------------------------
### 3-4. DELETE

	DELETE 테이블명
	WHERE절;  // 조건 입력 안하면 테이블 전체가 다 삭제되니 삭제할 조건을 입력해줘야한다.


## 4. DDL
#### 데이터 베이스 객체 종류
- TABLE
- VIEW
- SEQUENCE
----------------------------------------------------------------------------------------------------------
#### 데이터 타입 
- char : 들어오는 데이터의 개수가 일정할 때 사용
- varchar : 들어오는 데이터의 크기가 가변적일 때 사용  // char보다 느리지만 저장공간 아낄 수 있음
- varchar2 : 2는 메모리 성능을 조금 더 보완한 데이터 타입
----------------------------------------------------------------------------------------------------------
### 4-1. 테이블, 뷰 관리
	# 테이블 생성
		CREATE TABLE 테이블명(
			컬럼명1 데이터타입(데이터크기), 
			컬럼명2 테이터타입(데이터크기)
			)

	# 테이블 생성2 (AS 사용)
		CREATE TABLE 테이블명
		AS
		SELECT문;  // 조회되는 내용으로 테이블 생성

	# 테이블 수정
		- 추가 : ALTER TABLE 
				ADD (칼럼명 데이터타입(데이터크기));

		- 수정 : ALTER TABLE
				MODIFY (컬럼명 데이터타입(데이터크기));

		- 삭제 : ALTER TABLE
				DROP COLUMN 컬럼명;

	# 테이블 삭제
		DROP TABLE 테이블명;
	
	# 테이블 초기화
		TRUNCATE TABLE 테이블명;  // DDL로 테이블 지우면 롤백 불가능

	# 테이브 제약조건
		- PK(primary key)
		- FK(foreign key)
		- UK(unique) : 중복을 방지한다
		- NN(not null) 

		(ex1) 테이블 레벨 단위에서 제약조건 설정
			  CREATE TABLE 테이블명(
			  	칼럼명1 VARCHAR(10),
			  	칼럼명2 VARCHAR(10,
			   	칼럼명3 VARCHAR(10),
			  	칼럼명4 NUMBER(10),
			  	CONSTRAINT 제약조건명 PRIMARY KEY(칼럼명1),
				CONSTRAINT FOREGIN KEY(칼럼명3)
				REFERENCES 참조할테이블명(칼럼명)
			    )

		(ex2) 컬럼레벨 단위에서 제약조건 설정  // not null은 컬럼 레벨에서만 가능
			  CREATE TABLE 테이블명(
			  	칼럼명1 VARCHAR(10) CONSTRAINT 제약조건명 PRIMARY KEY,
			  	칼럼명2 VARCHAR(10 CHECK (조건),  // 조건에 맞아야 데이터 삽입 가능
			   	칼럼명3 VARCHAR(10) NOT NULL,
			  	칼럼명4 NUMBER(10) REFERENCES 참조할테이블명(칼럼명),
			    )

	# 제약조건2 : 밖에서 외래키 설정한는 방법
		ALTER TABLE 테이블명
			ADD CONSTRAINT 외래키명 FOREIGN KEY (칼럼명)
			REFERENCES 테이블명 (칼럼명);

   *TABLE 자리에 VIEW입력하면 뷰에 대한 쿼리문이 된다.
----------------------------------------------------------------------------------------------------------
### 4-2. 시퀀스 관리 
	CREATE SEQUENCE 시퀀스명
	MINVALUE -- 시퀀스가 시작되는 최초의 숫자
	MAXVALUE --시퀀스가 끝나는 최대 숫자
	INCREMENT BY -- 시퀀스가 증가되는 단위
	START WITH -- 시퀀스 생성이 시작되는 값
	NOCACHE  -- 캐시를 사용하지 않음
	NOORDER  --요청되는 순서대로 값을 생성하지 않음
	NOCYCLE  --초기값부터 다시 시작하지 않음

	(ex) CREATE SEQUENCE mem_ID_SEQ
			START WITH 100
			INCREMENT BY 1
			MINVALUE 100
			MAXVALUE 9999
			NOCYCLE;

## 5. DCL
#### 기본 개념
- Transaction : DB의 작업 단위, 일괄처리의 기준
- Commit : 트랜잭션이 정상적으로 수행되었을 때 트랙잭션의 수행내용 전체르 한번에 물리적으로 DB에 저장
- Rollback : 트랜잭션이 비정상적으로 수행되었을 때 이전 커밋(save point) 시점으로 회귀
- DML : INSERT/UDPATE/DELETE 은 연속된 작업이면 합쳐서 트랜잭션 1개
- DCL : CREATE/DROP/ALTER 는 작업 각각이 개별 트랜잭션
- Auto commit : 이전 트랜잭션이 완료되지 않아도 다음 트랜잭션이 시작하면 자동으로 커밋

