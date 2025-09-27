# SQL_BASIC 4주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_4th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**4주차 과제부터는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_4th

### 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-4. 오류를 잘 디버깅하는 방법



## 섹션 5. 데이터 탐색 - 변환

### 4-1. INTRO

### 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)

### 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

### 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 3-4. 오류를 디버깅하는 방법

~~~
✅ 학습 목표 :
* 오류의 정의에 대해 설명할 수 있다. 
* 오류 메시지를 보고 디버깅이라는 과정을 수행할 수 있다. 
~~~


~~~
✅ 학습 목표 :
* 데이터 타입의 종류를 설명할 수 있다. 
* 데이터 타입을 변환하는 방법을 설명할 수 있다. 
~~~

1. SELECT  list must not be emty at [10:1]
   ```
   select
    col # -> 이 부분이 비어있다는 오류
   from
   ```

2. Number of arguments does not match for aggregate function COUNT
   ```
   SELECT
     COUNT(id, name) # -> 이 부분에 두 개 이상의 컬럼이 들어갈 수 없음
   FROM basic.pokemon
   ```
   - 해석: 집계 함수 COUNT의 인자 수가 일치하지 않습니다
     

3. Select list expression references column type1 a which is neither grouped nor aggregated
   ```
   SELECT
     type1,
     COUNT(id) AS cnt
   FROM basic.pokemon
    # 여기서 groupby type1 이 있어야함
   ```
- 해석: select 목록 식은 다음에서 그룹화되거나 집계되지 않은 열을 참조합니다
- group by에 적절한 컬럼을 명시하지 않았을 경우 발생하는 오류
  
4. syntax error: Expected end of input but got keyword SELECT
   ```
   SELECT
     type1,
     COUNT(id) AS cnt
   FROM basic.pokemon
   GROUP BY
     type1

   SELECT
     *
   FROM basic.trainer
   
   ```
- 해석: 입력이 끝날 것으로 예상되었지만 SELECT 키워드가 입력되었습니다 
- 하나의 쿼리엔 SELECT가 1개만 있어야함
- 쿼리가 끝나는 부분에 ; 추가

  5. syntax error: Expected end of input but got keyword WHERE at [5:1]
     ```
     SELECT
       *
     FROM basic.trainer LIMIT 10
     WHERE
       id =3
     ```
- 해석: 입력이 끝날 것으로 예상되었지만 [5:1]에서 키워드 WHERE를 얻었습니다.
- [5:1] -> [줄:칸]
- LIMIT 함수는 가장 마지막에 나와야함

6. syntax error: Expected ")" but got end of script at [8:1]

- 해석: )가 예상되었지만 [8:11]에서 스크립트가 끝났습니다
- 항상 (가 있으면 )를 마지막에 써줘야한다
  

## 4-2. 데이터 타입과 데이터 변환(CAST, SAFE_CAST)
### 데이터 타입
1. 숫자(int64)
2. 문자(string)
3. 시간 날짜 -> ex) 2022-09-29 , 2012-03-19 23:45:29
4. 부울(Bool) -> 참/거짓

### 데이터 타입이 중요한 이유
- 보이는 것과 저장된 것의 차이
- 엑셀 상에서 NaN라고 적혀 있는 것이 빈 셀(NULL)인지 문자열인지 육안으로 알 수 없음

### 자료 타입 변경하기
- 변경함수: CAST
  ```
  select
    cast(1 AS STRING)
  ```
  숫자 1을 문자 1로 변경

  ```
  select
    cast("후영리" AS INT64)
  ```
  문자열을 숫자로 어떻게 바꿔
  오류가 발생!

  <안전하게 데이터 타입 변경>
  
  SAFE_CAST함수
  : 변환이 실패할 경우 NULL 반환

  ```
    select
    cast("후영리" AS INT64)
  ```
"후영리"는 NULL로 반환됨

### 수학함수
- 외울 필요없고 필요할 때 찾아써라
- 나누기를 할 때,
    - x/y 대신 SAFE_DIVIDE함수 이용
    - x,y중 하나라도 0인 경우, 그냥 나누면 zero error 발     
  



## 4-3. 문자열 함수(CONCAT, SPLIT, REPLACE, TRIM, UPPER)

~~~
✅ 학습 목표 :
* 문자열 함수들의 종류를 이해하고 어떠한 상황에서 사용하는지 설명할 수 있다. 
~~~

### concat(문자열 붙이기)
```
select
  concat("안녕","하세요") as result
```
- from이 없어도 작동
- concat 인자로 string이나 숫자를 넣을 때는 데이터를 직접 넣어주게 되는것

### split(문자열 분리하기)
```
select
  split("가,나,다,라",",") as result
```
- split(문자열_원본, "나눌기준이 되는 문자")
- 띄어쓰기도 유의

### replace(특정 단어 수정하기)
```
select
  replace("안녕하세요","하세요","하십니까")
```

- replace(문자열 원본, 바꿀 대상이 되는 단어, 바꿀 단어)

### trim(문자열 자르기)
```
select
  trim("후영리","후")
```

- trim(문자열 원본, 자를단어)
- 자른다기보다는 없애주는 기능

### upper(영어 대문자 변환)
```
select
  upper('abc')
```

- upper(문자열 원본)
- 데이터에서 같은 스펠링이지만 대문자, 소문자 다양한 형태로 이루어진 변수를 찾을 때 유용



## 4-4. 날짜 및 시간 데이터 이해하기(1) (타임존, UTC, Millisecond, TIMESTAMP/DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터 타입과 UTC의 개념을 설명할 수 있다. 
* DATE, DATETIME, TIMESTAMP 에 대해서 설명할 수 있다.
* 시간함수들의 종류와 시간의 차이를 추출하는 방법을 설명할 수 있다. 
~~~

### 날짜 및 시간 데이터 타입 파악하기
1. date
   date만 표시하는 데이터, 2023-01-02

2. datetime
   date+time 표시 데이터, time zone 정보x, 2020-09-19 12:01:09

3. time
   time만 표시하는 데이터, 09:23:45

### TIMEZONE
#### GMT
영국 그리니치 천문대 기준
한국시간: GMT + 9

#### UTC
국제 표준시간
한국시간: UTC + 9

#### TIMESTAMP
UTC부터 경과한 시간을 나타내는 값
TIMEZONE정보 있음
ex) 2023-12-31 14:33:20 UTC


### millisecond, microsecond
#### millisecond
- 1,000ms = 1초
- millisecond -> timestamp -> datetime으로 변경

#### microsecond
- 1,000,000us = 1초

ex) 1704176819711ms
```
select
  timestamp_millis(1704176819711) as milli_to_timestamp_value,
  timestamp_micro(1704176819711000) as micro_to_timestamp_value,
  datetime(timestamp_micros(1704176819711000)) as datetime_value;
```
- 잘못된 쿼리
- 한국시간이 기준인데 UTC시간으로 나왔음

```
  datetime(timestamp_micros(1704176819711000),'Asia/Seoul') as datetime_value_seoul;
```
- 'Asia/Seoul'을 추가해줘야함

**table에 시간이 timestamp로 저장된 경우가 많음 -> timestamp => datetime 변환이 필요할 수 있음**

### TIMESTAMP와 DATETIME비교

```
SELECT
 CURRENT_TIMESTAMP() AS timestamp_col
 DATETIME((CURRENT_TIMESTAMP().'Asia/Seoul') AS datetime_col
```
timestamp_col: 현재 UTC시간
datetime_col: 현재 한국시간 




<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

# 인증샷
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/63a322c9-f1b5-4694-91fd-6f0837931701" />


## 프로그래머스 문제 

> 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
>
> **먼저 문제를 풀고 난 이후에 확인 문제를 확인해주세요**
>
> 문제 링크 
>
> :  https://school.programmers.co.kr/learn/courses/30/lessons/131535#

<!-- 문제를 풀기 위하여 로그인이  필요합니다. -->

<img width="961" height="1079" alt="image" src="https://github.com/user-attachments/assets/0aac36e2-a351-421b-accb-28d5ac774721" />


2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 몇 명인지 출력

```
select
  COUNT(USER_ID) AS CNT
from USER_INFO
WHERE
  JOINED(YEAR) = 2021 AND AGE >= AND AGE <=29
```

## 문제 1

> **🧚Q. 프로그래머스 문제를 풀던 서현이는 여러 번의 시행착오 끝에 결국 혼자 해결하기 어려워 오류 메시지를 공유하며 도움을 요청했습니다. 여러분들이 오류 메시지를 확인하고, 해당 SQL 쿼리에서 어떤 부분이 잘못되었는지 오류 메시지를 해석하고 찾아 설명해주세요.**

~~~sql
# 조건에 맞는 회원 수 구하기 (SELECT, COUNT) 
# 서현이의 SQL 첫 번째 풀이
SELECT COUNT(AGE, JOINED)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : Error: Number of arguments does not match for aggregate function COUNT
 
# 수정하고 난 이후 두 번째 풀이
SELECT AGE, COUNT(*)
FROM USER_INFO
WHERE AGE BETWEEN 20 AND 29
  AND JOINED BETWEEN '2021-01-01' AND '2021-12-31';
  
오류 메시지 : SELECT list expression references column AGE which is neither grouped nor aggregated
~~~



~~~
첫 번째 오류 메세지: 집계 함수 COUNT의 인자 수가 일치하지 않습니다
문제: COUNT함수에는 하나의 인자만 들어가야합니다
해결방법: COUNT(AGE, JOINED) 대신 NULL 값이 없을 것으로 예상되는 USER_ID를 써줍니다. => COUNT(USER_ID)

두 번째 오류 메세지: select 목록 식은 다음에서 그룹화되거나 집계되지 않은 열을 참조합니다
문제: group by에 적절한 컬럼을 명시하지 않았을 경우 발생하는 오류, AGE 칼럼을 명시했지만 GROUP BY 함수를 쓰지 않았기 때문에 생긴 문제입니다
해결방법: AGE를 지워줍니다

~~~



### 🎉 수고하셨습니다.
