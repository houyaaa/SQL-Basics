# SQL_BASIC 3주차 정규 과제  

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_3rd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**3주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **7 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 3문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_3rd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-6. 연습문제 1~3번

### 2-6. 연습문제 7~9번

### 2-6. 연습문제 10~12번

### 2-6. 연습문제 13~17번

### 2-7. 정리 

### 2-8. 새로운 집계함수



## 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-1. INTRO

### 3-2. SQL 쿼리 작성하는 흐름

### 3-3. 쿼리 작성 템플릿과 생산성 도구 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 2-6. 연습문제

~~~
✅ 학습 목표 :
* 연습문제(7문제 이상) 푼 것들 정리하기
~~~

#1
처음에 
select
*,
count(id) as cnt
from basic.pokemon
where 
type2 is null

이라고 적음

*오류*
count(id)는 집계함수로 결과를 한 줄(집계된 값)로 만들려고 함
*는 모든 개별 행을 그대로 가져오려는 의도

count(id): 전체를 요약해서 1행으로 만들자
<-> *: 원래대로의 여러 행을 그대로 보여주자
충돌이 일어남 

올바른 정답
select
count(id) as cnt
from basic.pokemon
where type2 is null

#2
처음에
select
type1
from basic.pokemon
where type2 is null;

SELECT 
type1, 
COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY type1
order by cnt desc;

둘이 합칠 수 있음!

select
type1,
COUNT(id) AS cnt
from basic.pokemon
where type2 is null
GROUP BY type1
order by cnt desc;

where절 뒤에 group by order by를 써주면 된다

#11
처음에
select
type1,
count(id) as cnt
from 
group by type1
having type2 is not null
order by cnt desc

*오류*
- 조건문은 group by한 컬럼과 관련이 없으므로 having이 아니라 where을 써야함
- where문은 group by 이전에 나와야함

#15
트레이너가 같은 포켓몬을 여러 마리 가질 수 있으므로 
count(pokemon_id) 에서 distinct를 쓰지 않음
if) count(distinct pokemon_id)를 쓰면 트레이너가 가지고 있는 포켓몬의 종류를 알 수 있음

#17
와 대따 어려움
countif(조건)

SELECT
trainer_id, #를 기준으로 보고싶은거니까 그룹화
countif(status="released") as released_cnt,
count(id) as pokemon_cnt, #트레이너별 전체 포켓몬 수
countif(status="released")/count(id) as ratio
from basic.trainer_pokemon
group by trainer_id
having ratio >=0.2





+) 
0. 쿼리문 작성 전에 
테이블 / 조건 / 컬럼 / 집계 ->를 작성해보고 쓰면 쉽다
1. null 
- null이 아닌 행을 보고 싶을 경우: is not null
- type2=null(x) null은 다른 값과 직접 비교 불가
- null은 is 연산자 사용
2. where절에서 여러 조건을 연결하고 싶은 경우: 
- and
- or 조건 ( ) or ( )
3. distint
- count(distint id)로 써야하는거 아니야 할때 이 자료에서는 id가 중복되지 않기 때문에 count(id) = count(distint id)
4. group by/order by 1 을 쓰면 select 뒤에 써준 첫번째 컬럼을 그룹화시켰다/정렬시킨다는 뜻 
ex) #4 group by is_legendary == group by 1
order by legend_or_not == order by 2
5. 서브쿼리: 쿼리문을 한 번 감싸서 다른 쿼리문에서 사용할 수 있음
ex) select
*
from(
    select
        name,
        count(id) as trainer_cnt
    from basic.trainer
    group by 
        name
)
where
trainer_cnt >=2

==
select
    name,
    count(id) as trainer_cnt
from basic.trainer
group by 
    name
having trainer_cnt >=2

6. or로 조건을 쓰면 너무 길어진다 in ( )을 이용해보자
ex) name in ("Iris","Whitney","Cynthia")
7. 제일 많은/작은 게 무엇인지 궁금한거라면 limit1을 써준다
order by ___ desc limit 1
order by ___ osc limit 1

8. " %" 어떤 문자열이 들어가는 행을 추출하고 싶을 때 like
- "%파": 파로 끝나는 
- "파%": 파로 시작하는
- "%파%": 파가 들어가는 

## 2-8. 새로운 집계함수

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE을 활용하는 방법을 설명할 수 있다. 
~~~

group by all

매번 컬럼을 명시할 필요없이 all을 쓰면 됨



## 3-2. 쿼리를 작성하는 흐름

~~~
✅ 학습 목표 :
* 쿼리를 작성하는 흐름을 설명할 수 있다.
~~~

1. 지표 고민 : 어떤 문제를 해결하기 위해 데이터가 필요한가? 문제정의
2. 지표 구체화: 추상적이지 않고 구체적인 지표 명시 
3. 지표 탐색 : 유사한 문제를 해결한 케이스가 있나 확인
    있다면) 해당 쿼리 리뷰
    없다면)
4. 쿼리 작성 : 구글 검색, chatgpt 검색 등 데이터가 있는 테이블 찾기 (2개 이상: join)
5. 데이터 적합성 확인: 예상한 결과와 동일한지 확인(확인하지 않을 경우, 지표를 다시 찾아야하는 불상사)
6. 쿼리 가독성: 나중을 위해 깔끔하게 쿼리 작성
7. 쿼리 저장: 쿼리는 재사용 됨

4보다는 전후 과정을 잘 따르는 것이 중요



## 3-3. 쿼리 작성 템플릿과 생산성 도구

~~~
✅ 학습 목표 :
* 생산성 도구를 만들 수 있다.
~~~

<!-- 이어질 주차에서 생산성 도구를 활용한 실습이 있습니다.강의에 맞게 제작하여 화면을 캡쳐하여 이 주석을 지우고 올려주세요. -->

오류가 떠서 돌아버리겠습니다



<br>
<br>

---

# 2️⃣ 학습 인증란

c:\Users\82103\Pictures\Screenshots\스크린샷 2025-09-20 160150.png



<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 게임에 재미를 느낀 동혁은 포켓몬 도감에서 강력한 포켓몬 타입을 미리 선점하기 위해, 먼저 어떤 포켓몬들이 있는지 포켓몬 수를 기준으로 내림차순 정렬하여  확인하고자 했습니다.**
>
> 그래서 다음과 같은 필요한 정보를 미리 정리해보았습니다. 

~~~
조건 : type2는 상관없이
보고 싶은 컬럼 : type1
집계 내용 : 각 type1 별 포켓몬 수
정렬 기준 : 포켓몬 수를 기준으로 내림차순 정렬
~~~

> **이 목표를 바탕으로 동혁이 아래와 같은 쿼리를 잘 작성했지만, 일부 SQL 문법 요소를 빼먹었습니다. 비어 있는 부분인 ㄱ,ㄴ,ㄷ 에 들어갈 알맞은 SQL 구문을 채워보세요:**

~~~sql
SELECT type1, (ㄱ)
FROM pokemon
(ㄴ) type1
ORDER BY (ㄱ) (ㄷ);
~~~



~~~
(ㄱ) : count(id) as pokemon_cnt
(ㄴ) : group by
(ㄷ) : DESC

~~~



### 🎉 수고하셨습니다.    
