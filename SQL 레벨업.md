
DBMS는 버퍼 매니저를 가지고 있는데 성능에 큰 영향을 줌

dbms 버퍼는 보통 데이터 캐시와 로그 버퍼가 있음

**데이터 캐시**는 디스크에 있는 데이터의 일부를 메모리에 유지하기 위해 사용하는 메모리 영역

만약 실행하는 select 구문에서 선택하는 데이터가 데이터 캐시가 들어 있다면, 굉장히 빠르게 응답, 없다면 디스크와 같은 저속 저장소에 접근하여 처리

**로그 버퍼**는 갱신처리(insert, delete, update, merge)와 관련, dbms가 sql구문을 받으면, 곧바로 저장소 데이터 변경이 아닌, 일단 로그 버퍼위에 변경 정보를 보내고 이후 디스크 변경 수행, 갱신처리는 SQL 구문의 실행 시점과 저장소에 갱신하는 시점에 차이가 있는 비동기 처리

왜 로그 버퍼를 둘까 -> 결국 성능 -> 저장소 변경이 끝날때까지 기다리면 사용자는 장기간 대기 -> 갱신 정보 받은 시점에서 사용자에게는 끝났음을 반환 -> 내부적으로는 계속 처리

커밋 시점에 반드시 갱신 정보를 로그파일에 씀 - 동기 처리, 지연 발생 가능성

mysql같은 경우 데이터캐시는 버퍼 풀이라고 명칭하고, 128mb가 기본값이다

갱신 SQL은 로그버퍼에, 검색 SQL은 데이터 캐시에, 일반적으로 검색이 많고, 많은 데이터가 필요하므로 데이터 캐시 사이즈를 늘림

**워킹 메모리**
정렬 또는 해시 관련 처리에 사용되는 작업용 영역

다루려는 데이터양보다 이 영역이 작아지면 저장소를 사용하여 처리함(OS 동작에서 말하는 스왑이 일어남) -> 저장소에 부족할 때 사용하는 임시적인 영역이 있음
, 당연히 느림 -> 메모리 부족해도 처리하려고 노력하는 db, 자바는 oom발생해버림

RDB에서 접근 절차를 결정하는 모듈은 **쿼리 평가 엔진**

흐름

1. 파서 : 구문 분석, 올바른지 검사, FROM 구에 존재하지 않는 테이블 쓰는 경우있는지 등, SQL구문 -> 정형적인 형식으로 변경해 후속 처리를 효율적이게
2. 옵티마이저 : 최적화 진행, 대상은 **데이터 접근법(실행 계획)** 
  - 플랜 생성 : 인덱스 유무, 데이터 분산 또는 편향 정도 등 고려하여 많은 실행 계획 생성
  - 비용 평가 : 가장 낮은 비용을 가진 실행 계획 선택
3. 카탈로그 매니저 : 옵티마이저에 중요한 정보를 제공 - DBMS의 내부 정보를 모아놓은 테이블들로 인덱스의 통계 정보가 저장
4. 플랜평가 : 실행계획을 받아 최적의 실행 결과를 선택하는 것(계획서) 

카탈로그에 통계정보로 옵티마이저는 실행 계획을 만듬, 항상 최적의 플랜이 아닐수 있음

예) 테이블에 데이터 삽입/갱신/제거 수행될 떄 카탈로그 정보가 갱신되지 않는다면, 옵티마이저는 오래된 정보를 바탕으로 실행 계획을 세우게됨

테이블의 데이터가 바뀌면 카탈로그의 통계 정보가 갱신되어야함(ms sql의 경우 갱신 처리가 될 때 자동으로 통계 정보 갱신)

-> 통계 정보 갱신은 실행 비용이 높음(대상 테이블 또는 인덱스의 크기와 수에 따라 수십분, 수시간) -> 갱신 시점을 확시리하게 검토

SQL 실행구문 종류 예시
1. 테이블 풀 스캔의 실행계획
2. 인덱스 스캔의 실행계획
3. 간단한 테이블 결합의 실행 계획

풀스캔(n), 인덱스 스캔(log n)

결합을 수행하는 쿼리의 실행계획에서 지연이 많이일어남

결합 전에 테이블 접근이 일어나는데(당연히) 어떤 테이블에 먼저 접근하지가 굉장히 중요, 같은 중첩 단계는 위에서 아래로

### 6. SELECT 구문

or가 많아질 경우 복잡해질 수 있음
IN을 사용해보기

```
-> OR 이용
SELECT name, address from Address
WHERE address = '서울시'
   OR address = '부산시'
   OR address = '인천시';
   
-> IN 이용
SELECT name, address from Address
WHERE address IN ('서울시','부산시','인천시);
```

NULL 찾을때는 IS NULL 이나 IS NOT NULL 이용 =NULL은 안됨

WHERE구가 '레코드'에 조건을 지정, HAVING구는 '집합'에 조건을 지정

```
SELECT address, COUNT(*)
FROM Address
GROUP BY address
HAVING COUNT(*) = 1;

address | count
속초시   | 1
서귀포시 | 1
```

**뷰**는 SELECT 구문을 데이터베이스 안에 저장한다는것, 사용방법은 테이블과 같고 내부에는 데이터를 보유하지 않는다는 점이 테이블과다름

**서브쿼리** FROM 구에 직접 지정하는 SELECT 구문

```
IN내부에서 서브쿼리 예제

SELECT name
  FROM Address
  WHERE name IN (SELECT name FROM Address2);
  
실제 전개되면
SELECT name
  FROM Address
  WHERE name IN ('인성', '민', '준서', '지연', '서준', '중진');
  
```
**검색 CASE 식**

조건분기를 위한 식
WHEN구의 평가식이라는 것은 필드=값 처럼 조건을 지정하는 식
```
SELECT name, address,
  CASE WHEN address ='서울시' THEN '경기'
  CASE WHEN address ='인천시' THEN '경기'
  ELSE NULL END AS disitrict
FROM Address;


실행결과

name | address | district
인성  | 서울시  | 경기
하진  | 서울시  | 경기
...
```

합집합 구하기 

UNION

모든 필드가 똑같은 레코드 겹치면 중복 제거 -> 제외싫다면 UNION ALL사용 INTERSECT와 EXCEPT도 맘찬가지

교집합 구하기

INTERSECT

차집합 구하기

EXCEPT


윈도우 함수는 GROUP BY와 같지만 집약하지 않음
```
group by에 count를 하면
속초 시 5
서울 시 2
이렇게 출력

PARTITION BY하면
속초 시 5
속초 시 5
속초 시 5
... 
이런식으로
```

윈도우 전용함수로 RANK 또는 ROW_NUMBER
ROW_NUMBER 는 동일한 순위를 배제하기 위해 유니크한 순위를 정한다. 

```
나이 많은 수로 랭크 구하기

SELECT name,
       age,
       RANK() OVER(ORDER BY age DESC) AS rnk
  FROM Address;
  
name | age | rnk
하린  | 55 | 1
준    | 45 | 2
기주  | 32 | 3
민    | 32 | 3
인성  | 30  | 5
...

32살이 두명이면 둘 다 3등으로 기록되고, 4등을 건너뛰고 5등부터 시작됨, 4등부터 시작되길 원하면 DENSE_RANK

```


### 8강
조건분기 시 UNION을 테이블에 접근하는 횟수가 많아져서 I/O 비용이 크게늘어남 -> 신중히해야됨 -> CASE사용


### 9강

CASE식 SUM에도 사용방법
SELECT prefecture,
      SUM(CASE WHEN sex ='1' THEN pop ELSE 0 END) AS pop_men,
      SUM(CASE WHEN sex ='2' THEN pop ELSE 0 END) AS pop_wom,
     FROM Population
     GROUP BY prefecture


union을 사용할때는 SELECT 구문들에서 사용하는 테이블이 다른 경우가 


집약함수 : 여러개의 레코드를 한 개의 레코드로 집약하는 기능(COUNT, SUM, AVG, MAX, MIN)

GROUP BY로 구로 집약했을 때 SELECT구에 입력할 수 있는 것 세가지
1. 상수
2. GROUP BY 구에서 사용안 집약 키
3. 집약 함수

GROUP BY는 정렬이나 해시를 하는데(최근에는 해시) 모두 메모리를 사용 -> 워킹 메모리가 확보되지 않으면 스왑 발생 -> 일시 영역을 사용하게됨 (TEMP 탈락) -> 연산 대상 레코드 수가 많을 경우 GROUP BY 충분히 

GROUP BY의 집약과 자르기

반복계 : 쿼리를 반복하며 사용하는 것 -> 계속 commit됨 도중에 실패해도 중간부터, 반복계는 X, 실행계획단순, 그러나 SQL 오버헤드(네트워크, SQL구문 파스, 실행계획생성)
포장계 : 한 번의 쿼리로 여러개 insert
