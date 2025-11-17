# SQL_BASIC 7주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_7th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**7주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

**(마지막 주차입니다. 조금만 더 힘내주세요~!!!)**

## SQL_BASIC_7th

### 섹션 7 데이터 결과 검증, 가독성 있는 쿼리 작성하기

### 6-1. Intro

### 6-2. 가독성을 챙기기 위한 SQL 스타일 가이드

### 6-3. 가독성을 챙기기 위한 WITH 문 & 파티션

### 6-4. 데이터 결과 검증 정의

### 6-5. 데이터 결과 검증 예시

### 6-6. 정리 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | ✅         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 6-2. 가독성을 챙기기 위한 SQL 스타일 가이드

~~~
✅ 학습 목표 :
* 데이터 결과 검증하기 전에 실수가 발생하는 원인을 설명할 수 있다.
* SQL 쿼리를 가독성 있게 작성할 수 있다. 
~~~

### 1. 예약어는 대문자로 작성

```
SELECT

FROM
WHERE 
GROUP BY 
ORDER BY
```


### 2. 컬럼 이름 Snake_case

아래 바가 있는 이름으로 작명



### 3. 명시적 vs 암시적인 이름

Alias (AS 사용할 때 하는 작명) 로 별칭을 지을 때, 명시적인 이름 적용

count(id) AS pokemon_cnt



### 4. 왼쪽 정렬

```
SELECT
  col
FROM table
WHERE
```

### 5. 예약어, 컬럼은 한 줄에 하나씩 권장

바로 주석처리할 수 있게

```
SELECT
  col1,
  col2,
  col3,
FROM table
WHERE
```

### 6. 쉼표는 컬럼 바로 뒤에 

```
SELECT
  col1
  ,col2
  ,col3
FROM table
WHERE
```



## 6-3. 가독성을 챙기기 위한 WITH문 & 파티션

~~~
✅ 학습 목표 :
* SQL 쿼리를 가독성 있게 작성할 수 있다. 
* WITH문과 파티션을 활용해서도 가독성을 챙길 수 있다. 
~~~

### WITH

서브쿼리의 단점: 안쪽 쿼리 먼저 실행하기 때문에 직관적으로 이해가 어려움

**-> 해결: WITH 문 활용**

```
WITH temp_table AS (
  SELECT
    col1
    ,col2
    ,col3
  FROM table
)
SELECT
 col1,
FROM temp_table 
WHERE
```

**WITH 구문의 장점**
1. 재사용 가능
2. 먼저 실행되는 안쪽 쿼리를 보면서 가독성이 떨어지는 일이 없음

### PARTITION

쿼리 비용 측면에서 탐색비용 또한 비용임 
애초에 일자별로 정리하면 특정 시기에 들어온 물건을 비용 효율적으로 찾을 수 있음

**PARTITION의 장점**

1. 쿼리 성능향상
   빠름

2. 데이터 관리 용이성
   특정 일자의 데이터를 모두 변경, 삭제해야하면 파티션을 설정해서 삭제할 수 있음

3. 비용
   파티션에 해당되는 데이터만 스캔해서 비용을 줄일 수 있음


그냥 where절을 쓰면 되는거고 내부적으로 데이터를 **저장**할 때 필요한 개념   





## 6-4. 데이터 결과 검증 정의 

~~~
✅ 학습 목표 :
* 데이터 결과 검증이 어떤 과정인지 설명할 수 있다. 
* 데이터 결과 검증에 대한 예시를 이해할 수 있다.  
~~~


[복습]
1. where 과 having의 차이점
   where: 전처리(그룹을 짓기 전에 적용되는 조건)
   having: 후처리(그룹의 결과를 검사해서 거름)

2. countif
   countif(조건) as 새로운 컬럼명(여기다가 조건에 맞게 세어준 수를 적어주는 것)

  group by 랑 짝꿍!

[COUNTIF - GROUPBY]
단순히 "전체 회원 중 남자가 몇 명인가?"를 알고 싶다면 GROUP BY가 필요 없음
하지만 "부서별(GROUP)로 남자가 몇 명인지" 알고 싶다면 반드시 그룹을 지어야 함

GROUP BY 없이: 전체 통계 (예: 우리 회사 전체 남자 수)
GROUP BY 있음: 그룹별 통계 (예: 부서별 남자 수, 연도별 가입자 수)



4. case when
   case
     when 조건 then 행이름(맞으면 뭐라고 할건지)
     else 행이름
   end as 위에서 지정해준 행들의 컬럼

5. except
특정 컬럼을 제외하고 싶을 때
select
* except id 

<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/157343

> 특정 옵션이 포함된 자동차 리스트 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/59044

> 오랜 기간 보호한 동물(1) 

https://school.programmers.co.kr/learn/courses/30/lessons/59043

> 있었는데요 없었습니다.



## LeetCode 문제

https://leetcode.com/problems/combine-two-tables/description/

> 175. Combine Two Tables

https://leetcode.com/problems/list-the-products-ordered-in-a-period/

> 1327. List the Products Ordered in a Period



<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 



## 문제 1

> **🧚예운이는 다음 SQL 쿼리를 다트비 정규과제에 제출했다. 제출한 쿼리는 다음과 같고, 이 쿼리는 에러 메시지 없이 잘 수행하는 쿼리이다.**

~~~sql
# 주영이가 작성한 가독성 나쁜 SQL 

select u.name , o.OrderID
, p.ProductName ,od.Quantity ,od.UnitPrice 	from Users u	join Orders o on u.id = o.userId
join OrderDetails od on o.OrderID = od.orderID	join Products p on od.ProductID = p.ProductID
where u.region= 'Busan'			order by o.OrderID
~~~

> **이에 과제를 검사하던 정우는 작성한 SQL을 보고 코드 리뷰를 진행하려고 했지만, 다음 쿼리를 보고 예운이에게 질문을 하였다. "예운아, 이 쿼리 가독성이 좀 안 좋은데 내가 고쳐도 괜찮을까? 가독성 좋게 SQL 가이드에 따라 정리해보려고 해"**
>
> 다음 SQL 쿼리를 **가독성 좋은 스타일로 다시 작성해보세요.** 



~~~
여기에 답을 작성해주세요.
~~~



<br>

<br>

<!-- 이렇게 SQL BASIC 과제가 마무리되었습니다. SQL은 범위가 넓고 처음 접할 때 어렵게 느껴지는 학문이지만, 이번 기수에서는 지난 기수에도 활용했던 인프런 무료 강의를 통해 기초를 탄탄히 다질 수 있도록 구성했습니다. 환경 세팅 과정이 다소 복잡했을 수도 있지만, 이번 과제를 통해 기본적인 쿼리 작성과 SELECT 명령어의 개념을 충분히 익혔을 거라 생각합니다. BASIC을 통해 데이터를 추출하는 기초를 다졌으면, 이제 ADVANCED 트랙에서 실무에 맞게 더 복잡한 문접과 분석 쿼리, 그리고 MASTER 트랙에서 실제 데이터베이스를 다루는 실무 명령어까지 배워갈 수 있습니다. 앞으로의 SQL 학습에도 화이팅이고, 부족한 템플릿이었지만 끝까지 함께해줘서 진심으로 감사드립니다.  -->

### 🎉 수고하셨습니다.
