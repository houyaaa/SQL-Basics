# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

**## Timestamp vs Datetime 비교**

|       | Timestamp            | Datetime |
| ----- | ---------------------- | --------- |
| 타임존 | UTC(타임존 정보O) | T(타임존 정보X)      |
| 시간차이 | 한국시간 -9시간 | 한국 zone 사용 시 한국시간과 동일        |
|   쿼리    | current_Timestamp()          | Datetime(current_Timestamp(),'Asia/Seoul') |

출력된 쿼리값에 타임존 정보(ex. UTC)가 없으면 어떤 기준으로 나온 시간인지 판별이 어려울 수 있음 

## Datetime 함수

### 1. Current_datetime

CURRENT_DATETIME([time_zone]) : 현재 datetime 출력

```
SELECT
 CURRENT_DATE() AS current_date,
 CURRENT_DATE("Asia/Seoul") AS seoul_date,
 CURRENT_DATETIME() AS current_datetime,
 CURRENT_DATETIME("Asia/Seoul") AS current_datetime_seoul,
```
time_zone이 없을 경우, -9시간의 date와 datetime이 출력됨

### 2. EXTRACT

1) EXTRACT( [PART] FROM DATETIME "[현재 날짜와 시간]" AS 이름 : DATETIME에서 특정 부분만 추출하고 싶은 경우

```
SELECT
 EXTRACT( YEAR FROM DATETIME "2025-10-31 12:52:19" ) AS year
```
-> 2025

2) EXTRACT ( DAYOFWEEK FROM datetime_col) : 요일 추출

```
SELECT
 EXTRACT(DAYOFWEEK FROME DATETIME "2025-10-31 12:52:19") AS day_of_week_sun
```
-> 6(금요일이므로)

일요일부터 [1,7] 범위값

### 3. Datetime_trunc

DATETIME_TRUNC(datetime_col, [Part]) : 파트를 기준으로 출력값을 남기고 싶은 경우

```
SELECT
 DATETIME_TRUNC(DATETIME "2025-10-31 12:52:19", DAY) AS day_trunc,
 DATETIME_TRUNC(DATETIME "2025-10-31 12:52:19", HOUR) AS hour_trunc
```

-> 2025-10-31(day까지만 출력되도록 함)
-> 2025-10-31 12:00:00 

### 4. PARSE_DATETIME

PARSE_DATETIME('문자열의 형태','DATETIME 문자열') AS datetime : 문자열로 저장된 datetime을 daytime 타입으로 바꾸고 싶은 경우

```
SELECT
 PARSE_DATETIME('%Y-%m-%d %H:%M:%S','2025-10-31 12:52:19') AS parse_datetime
```
-> 2025-10-31 12:52:19(이제 datetime 유형의 데이터가 되었음)

### 5. FORMAT_DATETIME

FORMAT_DATETIME("%c", DATETIME "2024-01-11 12:35:35") AS formatted
: DATETIME 타입 데이터를 특정 형태의 문자열 데이터로 변환하고 싶은 경우 

-> PARSE와 반대 


### 6. LAST_DAY

LAST_DAY(DATETIME, [기준]): 마지막 날을 알고 싶은 경우(달마다 마지막날이 다르므로)

```
SELECT
 LAST_DAY(DATETIME '2025-10-21 12:52:19') AS last_day
 LAST_DAY(DATETIME '2025-10-21 12:52:19',week) AS last_day_month
 LAST_DAY(DATETIME '2025-10-21 12:52:19',week(MONDAY)) AS last_day_month_mon
```
-> 2025-10-31
-> 2025-10-25(토요일, sql환경에서는 일요일이 주의 시작점)
-> 2025-10-26(일요일, 월요일을 기준으로 그 전 날)

### 7. DATETIME_DIFF

DATETIME_DIFF(첫 DATETIME, 두 번째 DATETIME, 궁금한 차이): 두 DATETIME의 차이를 알고 싶은 경우

```
SELECT
 DATETIME_DIFF(FIRST, SECOND, DAY) AS day_diff1,
 DATETIME_DIFF(FIRST, SECOND, MONTH) AS day_diff2,
FROM(
 SELECT
  DATETIME "2024-04-02 10:20:00" AS FIRST,
  DATETIME "2021-01-01 15:30:00" AS SECOND,
)
```
-> day_diff1: 1187 (일, 첫 번째 datetime이 더 큰(최근 날짜) 값 이므로 양수)
-> day_diff2: 39 (개월) 


# 4-5. 연습문제

데이터 타입에서 catch_datetime에 UTC가 적혀있음
datetime은 T가 있어야함 이름은 datetime이지만
, Timestamp 타입의 데이터임을 알 수 있음 

-> 그렇다면, catch_date의 기준 타임존은 어디일까? 를 의심해봐야함 

sol) DATE(DATETIME(catch_datetime, "Asia/Seoul")) != catch_date 

라면, catch_date는 사용하기 어려울 수 있음 

```
select
count(*)
from(
 select
  id,
  catch_date,
  date(datetime(catch_datetime,"Asia/Seoul")) as changed_to_kr_time
 from basic.pokemon_trainer
)
where
catch_date != changed_to_kr_time
```

-> 141 행(이 다른 날짜를 가진 행)

따라서 컬럼의 설명을 꼭 확인하고 sql을 확인해야한다. 

## 1번 문제 
Q; 트레이너가 포켓몬을 포획한 날짜(catch_date)를 기준으로 2023년 1월에 포획한 포켓몬의 수 

-- 컬럼을 꼭 확인하고 쿼리를 작성(catch_date가 어떤 데이터 타입인지 확인)



## 2번 문제 전에 확인해야할 것 
battle_datetime과 datetime(battle.timestamp,"Asia/Seoul")이 같은지 확인

```
select
*
from basic.battle
where
battle_datetime!= datetime(battle.timestamp,"Asia/Seoul")

```
-> 실행 결과 없음 (다른 것이 없다는 얘기)

or 이렇게 쿼리를 짤 수도 있음

```
select
countif(battle_datetime!= datetime(battle.timestamp,"Asia/Seoul")
as not_same_date
from basic.battle

```
-> not_same_date : 0 



**숫자형일 때, between을 쓸 수 있음** 
ex) extract(hour from battle_datetime) between 6 and 18

## 2-1문제
Q: 시간대별로 몇 개의 배틀이 있나? 

```
select
count(distinct id) as cnt,
hour
from(
select
id, #본 쿼리에서 id의 개수를 쓸거니까 id를 선택해줘야함
extract(hour from battle_datetime) as hour
from basic.pokemin_trainer
)
group by hour
 
```

## 3번 문제
각 트레이너별<< 이기 때문에 group by 를 써야함

```
select
trainer_id,
format_date*%m/%d/%Y, min_catch_date)
from(
select
trainer_id,
min(date(catch_datetime,"Asia/Seoul")) as min_catch_date
from basic.trainer_pokemon
)
group by trainer_id
```

%Y: 2023 // %y:23 

## 4번 문제
```
select
extract(dayofweek from battle_datetime) as weekday,
count(*) as cnt
from basic.trainer_pokemon
group by weekday
```

count(*) cnt를 안적으면 
배틀이 발생한 요일에는 어떤 것들이 있나요? 라고 물어보는거랑 같음
결과) 
weekday
1(일요일)
2(월요일)
4
7
이렇게 나올거임 

## 5번 문제
```
select
trainer_id,
datetime_diff(min_catch_date,max_catch_date,day) as diff
from(
select
trainer_id,
min(date(catch_datetime,"Asia/Seoul"))as min_catch_date,
max(date(catch_datetime,"Asia/Seoul"))as max_catch_date
from basic.trainer_pokemon

group by trainer_id
)
order by diff desc

```
? 왜 group by trainer_id가 있어야 하느냐
"데이터를 먼저 trainer_id별로 같은 폴더에 넣고 각 폴더에서 min값과 max값을 계산해줘" 
어떤 기준으로 묶어서 집계할 것인지 반드시 group by 절에 명시해야함 

# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->



 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->



<br>

<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 사용자 로그 데이터에서, 2021년에 접속한 사용자 수를  집계하려고 했습니다. 그는 여러 SQL 쿼리들을 실행해봤지만, 그 중 일부는 문법적으로 잘못되어 실행되지 않았습니다. 다음 보기 중 틀린 쿼리를 모두 골라보세요 (복수 선택 가능)**

~~~sql
1. SELECT COUNT(*)  
   FROM user_log  
   WHERE EXTRACT(YEAR FROM login_date) = 2021;

2. SELECT EXTRACT(YEAR FROM login_date), COUNT(*)  
   FROM user_log  
   GROUP BY EXTRACT(YEAR FROM login_date);

3. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date = '2021';

4. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date BETWEEN '2021-01-01' AND '2021-12-31';
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 login_data 컬럼은 DATE type의 데이터를 가지고 있다고 가정하시면 됩니다. -->

~~~
여기에 답을 작성해주세요!
~~~



## 문제 2

> **🧚Q. 혜성이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
여기에 답을 작성해주세요!
~~~
## 인증샷
<img width="1891" height="752" alt="image" src="https://github.com/user-attachments/assets/e90f17ae-ff7b-41b3-b039-c15d68eb43c9" />



<br>

### 🎉 수고하셨습니다.
