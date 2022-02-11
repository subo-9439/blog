
Sql공부를 소홀히 한거 같아 프로그래머스에 있는 
<a href="https://programmers.co.kr/learn/challenges?tab=sql_practice_kit">
SQL 고득점 Kit</a> 를 풀어 보았다.

# 테이블 설명
![](1.png)
<br/>
<br/>

# 1. 모든 레코드 조회하기
> 동물 보호소에 들어온 모든 동물의 정보를 ANIMAL_ID순으로 조회하는 SQL문을 작성해주세요.
```SQL
SELECT * 
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID;
```
ORDER BY를 이용하기 ASC(생략 가능)로 순서 표시
<br/><br/>

# 2. 역순 정렬하기
> 동물 보호소에 들어온 모든 동물의 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 ANIMAL_ID 역순으로 보여주세요.

```SQL
SELECT NAME, DATETIME 
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID DESC;
```
ORDER BY를 이용하기 DESC로 순서 표시
<br/><br/>

# 3. 아픈 동물 찾기
> 동물 보호소에 들어온 동물 중 아픈 동물의 아이디와 이름을 조회하는 SQL 문을 작성해주세요.

```SQL
SELECT ANIMAL_ID, NAME 
FROM ANIMAL_INS 
WHERE INTAKE_CONDITION LIKE 'SICK' 
ORDER BY ANIMAL_ID;
```
WHERE COLUMN명 LIKE '조건' 으로 원하는 조건 선택
 
<br/><br/>

# 4. 어린 동물 찾기
> 동물 보호소에 들어온 동물 중 젊은 동물의 아이디와 이름을 조회하는 SQL 문을 작성해주세요. 
```SQL
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS 
WHERE INTAKE_CONDITION NOT IN ('AGED');
```
원하는 속성만 제외 시키는 방법 WHERE COLUMN명 NOT IN ('조건1','조건2','조건3')

<br/><br/>

# 5. 동물의 아이디와 이름
> 동물 보호소에 들어온 모든 동물의 아이디와 이름을 ANIMAL_ID순으로 조회하는 SQL문을 작성해주세요.
```SQL
SELECT ANIMAL_ID, NAME 
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID;
```


<br/><br/>

# 6. 여러 기준으로 정렬하기
> 동물 보호소에 들어온 모든 동물의 아이디와 이름, 보호 시작일을 이름 순으로 조회하는 SQL문을 작성해주세요. 단, 이름이 같은 동물 중에서는 보호를 나중에 시작한 동물을 먼저 보여줘야 합니다.
```SQL
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS 
ORDER BY NAME ASC, DATETIME DESC;
```
<br/><br/>

# 7. 상위 n개 레코드
> 동물 보호소에 가장 먼저 들어온 동물의 이름을 조회하는 SQL 문을 작성해주세요.
```SQL
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1;
```
또는 LIMIT 0, 1 (0 이후부터 1개를 출력) 으로 작성해도 출력가능
```SQL
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 0,1;
``` 
ex) LIMIT 2, 5 (2이후로 5개를 출력)
<br/><br/>