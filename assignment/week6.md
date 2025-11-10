# SQL_BASIC 6주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_6th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**6주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_6th

### 섹션 6. 다량의 자료를 연결 : JOIN 

### 5-1. Intro

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기 

### 5-5. JOIN을 처음 공부할 때 헷갈렸던 부분

### 5-6. JOIN 연습문제 1~2번

### 5-6. JOIN 연습문제 3~5번

### 5-7. 정리



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<!-- 여기까진 그대로 둬 주세요-->

<br>

---

# 1️⃣ 개념정리

## 5-2. JOIN 이해하기

~~~
✅ 학습 목표 :
* JOIN에 대한 정의와 필요성에 대해 설명할 수 있다.
~~~


JOIN: 서로 다른 데이터 테이블을 연결

trainer_pokemon 테이블의 trainer_id와 trainer 테이블의 id를 기준으로 두 테이블 연결(JOIN)

```
select
tp*,
t*
from trainer_pokemon as tp
left join trainer as t
on tp.trainer_id=t.id
```



## 5-3. 다양한 JOIN 방법

~~~
✅ 학습 목표 :
* JOIN 방법들의 종류를 설명할 수 있다. 
* 각 JOIN 방법들의 차이점에 대해서 설명할 수 있다. 
~~~

<img width="3373" height="1000" alt="image" src="https://github.com/user-attachments/assets/08cdbe23-22b7-49e2-bc5a-1b127c256399" />



## 5-4. JOIN 쿼리 작성하기 

~~~
✅ 학습 목표 :
* JOIN을 사용한 문법에 대해 이해하여 적용할 수 있다.
* JOIN 을 활용한 쿼리를 작성할 수 있다. 
~~~

1. 테이블 확인: 테이블에 저장된 데이터, 컬럼 확인
2. 기준 테이블 정의: 가장 많이 참고할 기준 테이블 정의
3. JOIN KEY 찾기: 여러 table과 연결할 key 정리
4. 결과 예상하기: 결과 테이블을 예상해서 손 or 엑셀로 작성
5. 쿼리 작성/검증: 예상한 결과와 동일한 결과가 나오는지 확인


**SQL JOIN문법**
```
SELECT
  a.col1,
  a.col2,
  b.col1,
  b.col2
FROM table1 as a
left join table2 as b
on a.key=b.key
```

ex_ 
1. trainer_pokemon의 trainer_id와 trainer의 id join
2. trainer_pokemon의 pokemon_id 와 pokemon의 id join

```
SELECT
tp*,
t*,
p*
FROM basic.trainer_pokemon as tp
left join basic.trainer as t
on tp.trainer_id=t.id
left join basic.pokemon as p
on tp.pokemon_id = p.id
```

**헷갈릴 부분**
1) 여러 JOIN 중 어떤 것 사용?

교집합: inner
모든 조합: cross
그 외: left 추천 

+) left join 
where col is not null 을 쓰면 inner join

2) 어떤 table을 왼쪽에?

   기준이 되는 table이 왼쪽

   기준 -> 데이터 요소가 빠짐없이 존재?

   ex) 유저들의 데이터? -> user table의 id
       주문한 유저들의 데이터? -> order table의 user_id

3) 여러 table 연결 가능?

   가능!

4) 컬럼은 모두 다 선택해야함?

   비용 측면에서 사용하지 않을 컬럼은 선택하지 않는 것을 선호

   제일 안쪽 서브쿼리에서 필요한 컬럼을 적어주고 바깥쿼리에서 * except()을 쓰며 비용 줄이기기



## 5-6. JOIN 연습문제 1~5번 

~~~
✅ 학습 목표 :
* 연습문제(3문제 이상) 푼 것들 정리하기
~~~

### **1번) 트레이너가 보유한 포켓몬들 몇 마리?**

1. 테이블 확인
   trainer_pokemon, trainer, pokemon 모두 필요
   
2. 기준 테이블 정의
  trainer_pokemon이 기준

3. JOIN KEY 찾기
  trainer_pokemon 과 trainer을 id로 join
  trainer_pokemon 과 pokemon도 id로 join
  pokemon 테이블의 kor_name컬럼 필요

```
SELECT
kor_name as pokemon_name, 
count(*아아니 여기에 뭘 넣어야됨???????*) as pokemon_cnt
FROM(
SELECT
  tp.trainer_id,
  tp.pokemon_id,
  tp.status,
  t.id,
  p.id,
  p.kor_name
FROM basic.trainer_pokemon as tp 
LEFT JOIN basic.pokemon as p
on tp.pokemon_id = p.id
LEFT JOIN basic.trainer as t
on tp.trainer_id = t.id
where status in("Active", "Trainig")
)
group by kor_name
```
<오답노트>

count(id)를 쓰니 Column name id is ambiguous 라고 하심 -> 더 정확한 컬럼명을 써야함 

아 그리고 trainer_pokemon을 가져올 때 status가 training과 active인 것만 가져올거임 그걸 tp라고 지정할거임

<retry>

```
SELECT
kor_name as pokemon_name
count(tp.id) as pokemon_cnt
from
(SELECT
id,
trainer_id,
pokemon_id,
status
FROM basic.trainer_pokemon
where status in ("Active", "Training")
) as tp 
LEFT JOIN basic.pokemon as p
on tp.pokemon_id = p.id
LEFT JOIN basic.trainer as t
on tp.trainer_id = t.id
group by kor_name
```

### **2번) 각 트레이너가 보유한 포켓몬들 몇 마리?**

1. 테이블 확인
   trainer_pokemon, pokemon 모두 필요
   
2. 기준 테이블 정의
  trainer_pokemon이 기준

3. JOIN KEY 찾기
   trainer_pokemon의 pokemon_id 와 pokemon의 id join

4. 결과 예상하기
   
| trainer_id  | pokemon            | pokemon_cnt |
| ----- | ---------------------- | --------- |
| 1 | 이상해씨 | 2         |
| 2 | 이브이 | 4         |
| 3 |이상해씨 | 1        |

```
select
tp*,
kor_name as pokemon_name,
count(tp.id) as pokemon_cnt
from
(SELECT
id,
trainer_id,
pokemon_id,
FROM basic.trainer_pokemon 
where status in ("Active", "Training")
) as tp
left join basic.pokemon as p 
on tp.pokemon_id = p.id
where type1 = "Grass"
group by kor_name
```

<오답노트>

tp.*  선택 안해도 됨 출력할 때 필요한 컬럼은 그 컬럼들이 아니니까

**group by kor_name이 아니라 type1을 해줘야함 지금 만들어놓은 것은 grass타입의 포켓몬들 중 어떤 포켓몬들이 트레이너들에게 보유되었는지를 출력**

<retry>

  ```
select
  type1,
  count(tp.id) as pokemon_cnt
from
(SELECT
id,
trainer_id,
pokemon_id,
  status
FROM basic.trainer_pokemon 
where status in ("Active", "Training")
) as tp
left join basic.pokemon as p 
on tp.pokemon_id = p.id
where type1 = "Grass"
group by type1
```

### **3번) 트레이너의 고향과 포켓몬을 포획한 위치가 같은 경우?**

1. 테이블 확인
   trainer_pokemon, trainer 모두 필요
   
2. 기준 테이블 정의
  trainer_pokemon이 기준

3. JOIN KEY 찾기
   trainer_pokemon의 trainer_id 와 trainer의 id join

```
select 
tp.trainer_id,
tp.location,
t.hometown,
t.id
from basic.trainer_pokemon as tp
left join basic.trainer as t
on tp.trainer_id = t.id
where location = hometown
```

<오답노트>

여기까지 했을 때, 위치 고향이 같은 케이스가 모두 나옴

-> count 를 어떻게 써야하지?

<retry>

```
select
  count(distinct tp.trainer_id) as trainer_uniq,** 고향에서 포켓몬을 잡아본 적이 있는 트레이너의 수 
  count(tp.trainer_id) as trainer_cnt** 트레이너가 고향에서 포켓몬을 잡은 모든 경우의 수
from basic.trainer_pokemon as tp
left join basic.trainer as t
on tp.trainer_id = t.id
where 
  tp.location is not null **
  and location = hometown
```

### **4번) Master 등급인 트레이너들은 어떤 타입의 포켓몬을 가장 많이 보유?**

1. 테이블 확인
   trainer_pokemon, trainer, pokemon 모두 필요
   
2. 기준 테이블 정의
  trainer_pokemon이 기준

3. JOIN KEY 찾기
   trainer_pokemon의 trainer_id 와 trainer의 id join
   trainer_pokemon의 pokemon_id 와 pokemon의 id join

```
select
count(tp.id) as pokemon_cnt,
type1
from basic.trainer_pokemon as tp
left join  basic.trainer as t
on tp.trainer_id = t.id 
left join  basic.pokemon as p 
on tp.pokemon_id = p.id
where achievement_level = "Master" 
      and status in ("Active", "Training")
group by type1
order by pokemon_cnt desc
```

<오답노트>

쿼리 비용 측면 -> trainer_pokemon에서 status가 보유한 상태인 것만 가지고 올 것 

order by pokemon_cnt 대신 2라고 써도 됨 


### **5번) Incheon 출신 트레이너 -> 1,2 세대 얼마나 보유?**

1. 테이블 확인
   trainer_pokemon, trainer, pokemon 모두 필요
   
2. 기준 테이블 정의
  trainer_pokemon이 기준

3. JOIN KEY 찾기
   trainer_pokemon의 trainer_id 와 trainer의 id join
   trainer_pokemon의 pokemon_id 와 pokemon의 id join

```
SELECT
count(tp.id) as cnt,
generation
from(
SELECT
id,
trainer_id,
pokemon_id,
status
FROM basic.trainer_pokemon
where status in ("Active", "Training")
) as tp 
LEFT JOIN basic.pokemon as p
on tp.pokemon_id = p.id
LEFT JOIN basic.trainer as t
on tp.trainer_id = t.id
where hometown = "Incheon" 
group by generation
```


<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/164673

> 조건에 부합하는 중고거래 댓글 조회하기 (JOIN)

https://school.programmers.co.kr/learn/courses/30/lessons/144854

> 조건에 맞는 도서와 저자 리스트 출력하기 (JOIN)

<img width="897" height="731" alt="image" src="https://github.com/user-attachments/assets/eb57bd76-26a4-4da2-bab8-5cfc5f3b2290" />

<img width="906" height="760" alt="image" src="https://github.com/user-attachments/assets/366f936c-b2ce-4e34-b184-a0b37cae790a" />



---

# 3️⃣ 참고자료

JOIN 에 대해서 그림으로 쉽게 이해할 수 있는 자료들도 있어서 첨부합니다. 아래의 블로그도 학습할 때 같이 참고해주세요.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90



2. https://velog.io/@wijoonwu/JOIN

<br>

### 🎉 수고하셨습니다.
