# 프로그래머스 SQL 고득점 Kit
## SELECT
### 핵심
SELECT 열 FROM 테이블 WHERE 조건 ORDER BY 정렬[ASC, DESC] LIMIT 숫자 (몇개까지의 자료를 보여줄지)

<br>

![image](https://user-images.githubusercontent.com/76419721/143208545-dcd4619e-6478-49f1-80d7-b235f5208e50.png)

<br>

### 1) 모든 레코드 조회하기
동물 보호소에 들어온 모든 동물의 정보를 ANIMAL_ID 순으로 조회하는 SQL 문 작성하기

```SQL
SELECT * FROM ANIMAL_INS ORDER BY ANIMAL_ID;
```

### 2) 역순 정렬하기
동물 보호소에 들어온 모든 동물의 정보를 ANIMAL_ID 역순으로 조회하는 SQL 문 작성하기
<br>
역순이기 때문에 ORDER BY 열 DESC 이용

```SQL
SELECT NAME, DATETIME FROM ANIMAL_INS ORDER BY ANIMAL_ID DESC;
```

### 3) 아픈 동물 찾기
동물 보호소에 들어온 모든 동물의 정보를 ANIMAL_ID 순으로 조회하는 SQL 문 작성하기 (조건 : 아픈 동물일 경우)
<br>
조건문 WHERE INTAKE_CONDITION = 'Sick' 이용

```SQL
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION = 'Sick' ORDER BY ANIMAL_ID;
```

### 4) 어린 동물 찾기
동물 보호소에 들어온 동물 중 젊은 동물의 아이디와 이름을 조회하는 SQL 문 작성하기 (조건 : 젊은 동물 + 아이디 순으로 정렬)
<br>
조건문 WHERE INTAKE_CONDITION != 'Aged' 이용, ORDER BY ANIMAL_ID

```SQL
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS WHERE INTAKE_CONDITION != 'Aged' ORDER BY ANIMAL_ID;
```

### 5) 동물의 아이디와 이름
동물 보호소에 들어온 모든 동물의 아이디와 이름을 ANIMAL_ID순으로 조회하는 SQL문 작성하기 (조건 : 아이디 순으로 정렬)
<br>

```SQL
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS ORDER BY ANIMAL_ID;
```

### 6) 여러 기준으로 정렬하기
동물 보호소에 들어온 모든 동물의 아이디와 이름, 보호 시작일을 이름순으로 조회하는 SQL문 작성하기 (조건 : 이름이 같은 동물이 있으면 DATETIME이 늦은 동물을 먼저 보여줘야 함)
<br>
먼저 이름(NAME)으로 조회하고 동일 값 존재할 경우 시간(DATETIME) 순으로 정렬해야 하므로 ORDER BY NAME ASC, DATETIME DESC 이용 

```SQL
SELECT ANIMAL_ID, NAME, DATETIME FROM ANIMAL_INS ORDER BY NAME ASC, DATETIME DESC;
```

### 7) 여러 기준으로 정렬하기
동물 보호소에 가장 먼저 들어온 동물의 이름을 조회하는 SQL 문을 작성하기 (조건 : DATETIME이 가장 빠른 동물을 먼저 보여줘야 함)
<br>
시간(DATETIME) 순으로 정렬해야 하므로 ORDER BY DATETIME, 최상위 1개의 값만 가져와야 하므로 limit 1 이용 

```SQL
SELECT NAME FROM ANIMAL_INS ORDER BY DATETIME limit 1;
```
