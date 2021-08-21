# SQL BASIC WEEK 3

**[수업 목표]**

1. 여러 테이블의 정보를 연결하는 Join을 이해한다.
2. 연결된 정보를 바탕으로 보다 풍부한 데이터분석을 연습한다.
3. 아래 위로 결과를 연결하는 Union을 공부한다.

**[목차]**

모든 토글을 열고 닫는 단축키
Windows : `Ctrl` + `alt` + `t` 
Mac : `⌘` + `⌥` + `t` 

---

## **01. 오늘 배울 것**

- 1) Join: 여러 정보를 한 눈에 보고 싶다면
    - '오늘의 다짐'을 남긴 회원의 이름을 알고싶어요

        오늘의 미션! 

        '오늘의 다짐' 이벤트 당첨자를 선정하여 스타벅스 기프티콘을 지급해야 해요.
        우선, 배운 내용을 사용해서 '오늘의 다짐' 테이블을 불러와 볼까요?

        *오늘의 다짐 이벤트: 오늘의 다짐을 남겨준 10명 추첨해서 기프티콘 지급하는 이벤트.

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled.png)

        - 이제는 테이블 정보를 쉽게 불러올 수 있죠?

        그런데 문제가 생겼어요!

        '오늘의 다짐' 이벤트 당첨자를 추첨하기 위해서는, 이름과 연락처 등의 정보를 알아야 하는데 여기에는 user_id라는 정보만 있어요.

        뭔가 user_id라는 정보에 힌트가 담겨있을 것 같은데... 어떻게 하면 좋을까요?

    - 기존의 방식대로 하면...

        우선, 회원 정보가 필요하니 users 테이블을 한번 살펴볼까요?

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%201.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%201.png)

        - 마찬가지로 select 쿼리문을 사용해서 잘 불러오셨죠?

        오! 뭔가, 똑같은 이름의 필드를 발견했어요. users 테이블의 user_id 필드와, checkins 테이블의 user_id 필드의 이름이 같아요. 이걸 잘 연결시키면 될 것 같지 않나요?

        - 자, 실제로 맞는지 확인해 봅시다! where를 잘 쓰면 되겠죠?

            ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled.png)

            - 우선 checkins 테이블의 맨 첫 데이터 user_id인 4b8a10e6를 복사해 줍니다.

            ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%202.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%202.png)

            - 그리고, user_id가 4b8a10e6인 데이터를 users 테이블에서 불러와보니 이렇게 잘 나오네요!

            대충 감을 잡았어요!

            1. checkins 테이블의 user_id를 복사!
            2. users 테이블에서 해당 user_id를 갖는 데이터를 가져오기!
            3. 작성자를 조회하고 싶은 '오늘의 다짐' 갯수대로 1, 2 과정을 반복!

            오늘의 다짐을 남긴 유저 100명을 얻어야 하면, 100번을 쿼리를 날려야겠죠? 우선 이렇게 하는데... 더 좋은 방법이 없을까요?

        **[오늘의 꿀팁!]** 

        한 테이블에 모든 정보를 담을 수도 있겠지만, 불필요하게 테이블의 크기가 커져 불편해집니다.
        ****그래서, 데이터를 종류별로 쪼개 다른 테이블에 담아놓고 연결이 필요한 경우 연결할 수 있도록 만들어놓습니다. 

        예를 들면, users와 checkins 테이블에 동시에 존재하는 user_id 처럼요. 
        이런 필드를 두 테이블을 연결시켜주는 열쇠라는 의미로 'key'라고 부릅니다.

    - 우리 모두의 시간은 소중하니까. Join을 사용하면?

        소중한 여러분의 시간이 낭비되게 만들도록 개발자 분들은 호락호락하지 않습니다. 
        두 테이블을 연결한다는 의미인 Join을 사용하면 이 고민을 한 방에 해결할 수 있어요!

        - 직접 눈으로 한번 봐볼까요?

            우선 지금은, 눈으로만! 
            이번 주에 열심히 배울 내용입니다.

            ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%203.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%203.png)

            - Join이라는 기능을 사용하면, 이렇게 한 눈에 두 개의 테이블을 연결해서 볼 수 있어요.

        짧은 Join 쿼리 한 줄만 더 쓰면, 한번의 쿼리로 이렇게 정보를 한 눈에 볼 수 있어요!

- 2) Join을 사용한 여러가지 연습을 진행하기

    지금까지 배운 내용을 사용해 실전과 같은 데이터분석을 진행해봅니다!

    회사에서 일을 하다보면, 저장된 데이터로부터 얻어내고 싶은 인사이트가 있겠죠? 
    스파르타 데이터베이스를 사용해 실전 데이터분석을 함께 해봅시다.

## **02. 여러 테이블을 연결해보자: Join 이란?**

- 3) Join 이란?

    Join이란?
    두 테이블의 공통된 정보 (key값)를 기준으로 테이블을 연결해서 한 테이블처럼 보는 것을 의미해요.

    예) user_id 필드를 기준으로 users 테이블과 orders 테이블을 연결해서 한 눈에 보고 싶어요!

    위의 예시와 같이, 두 테이블의 정보를 연결해서 함께 보고싶을 때가 있겠죠?

    그럴 때를 대비해서 무언가 연결된 정보가 있을 때, user_id 처럼 동일한 이름과 정보가 담긴 필드를 두 테이블에 똑같이 담아놓는답니다. 이런 필드를 두 테이블을 연결시켜주는 열쇠라는 의미로 'key'라고 불러요.

    - 직접 데이터로 살펴볼까요?

        깜짝 퀴즈! 아래 테이블에서 (checkins 테이블) key값에 해당하는 필드를 찾아보세요.

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%204.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%204.png)

        - 눈치채신 분도 계시겠지만, 빨간색으로 표시해놓은 필드가 모두 key값에 해당하는 필드입니다.

        **[오늘의 꿀팁!]** 
        병원에서 ****의사선생님이 '환자번호 101번님 진료받으러 들어오세요' 라고 불렀는데 같은 환자번호를 가진 사람이 여러명이 있으면 누가 들어와야 할지 환자번호만으로 알 수 없겠죠?

        SQL에서의 Join도 마찬가지에요. 
        key값을 사용해 연결하고 싶은 테이블에 찾아가서 똑같은 값을 가지는 key를 찾게 되는데, 똑같은 key를 가지는 데이터가 여러개 있으면 어느 데이터를 가져와서 연결해야 할지 알 수 없어요.

    - **[코드스니펫] Join을 사용해서 Key값으로 두 테이블 연결해보기**

        자세한 내용은 곧장 설명해드릴테니, 눈으로만 따라오세요!

        ```sql
        select * from point_users
        left join users
        on point_users.user_id = users.user_id
        ```

        대충 감이 잡히나요? 자, 이제 본격 시동을 걸어보죠!

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%205.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%205.png)

    **[오늘의 꿀팁!]** 혹시 엑셀을 잘 쓰신다면? 

    SQL의 Join은 엑셀의 vlookup과 동일하다고 생각하시면 됩니다 :-) 

- 4) Join의 종류: Left Join, Inner Join
    - Left Join: 유저 데이터로 Left Join 이해해보기

        앗! 어디서 많이 본 그림 아닌가요? 

        생각하는 그 그림이 맞아요! SQL에서의 Join은 두 집합 사이의 관계와 같답니다.

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%206.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%206.png)

        - 여기서 A와 B는 각각의 테이블을 의미합니다. 둘 사이의 겹치는 부분은, 뭔가 테이블 A와 B의 key 값이 연결되는 부분일 것 같지 않나요?
        - **[코드스니펫] 유저 데이터로 Left Join 이해해보기**

            ```sql
            select * from users u
            left join point_users p
            on u.user_id = p.user_id;
            ```

        어떤 데이터는 모든 필드가 채워져있지만, 어떤 데이터는 비어있는 필드가 있습니다. 

        꽉찬 데이터: 해당 데이터의 user_id 필드값이 point_users 테이블에 존재해서 연결한 경우
        비어있는 데이터: 해당 데이터의 user_id 필드값이 point_users 테이블에 존재하지 않는 경우

        - 비어있는 데이터의 경우, 회원이지만 수강을 등록/시작하지 않아 포인트를 획득하지 않은 회원인 경우에요!
        - Where를 사용해서 직접 확인해보기!

            꽉찬 데이터, 비어있는 데이터에서 하나씩 user_id를 뽑아서 orders 테이블에서 조회해볼까요?

            꽉찬 데이터의 user_id값 예시: d90e7626
            비어있는 데이터의 user_id값 예시: 3b3eac9f

            위의 user_id값으로 조회하면 데이터가 정상적으로 한 개의 데이터가 출력되지만, 아래의 user_id값으로 조회하면 데이터가 출력되지 않는 것을 알 수 있습니다!

    - Inner Join: 유저 데이터로 Inner Join 이해해보기

        이것도 어디서 많이 본 그림이에요!

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%207.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%207.png)

        - 여기서 A와 B는 각각의 테이블을 의미합니다. 이 그림은 뭔가, 두 테이블의 교집합을 이야기하고 있는 것 같지 않나요?
        - **[코드스니펫] 유저 데이터로 Inner Join 이해해보기**

            ```sql
            select * from users u
            inner join point_users p
            on u.user_id = p.user_id;
            ```

            앗, 여기서는 비어있는 필드가 있는 데이터가 없어요!

            그 이유는, 같은 user_id를 두 테이블에서 모두 가지고 있는 데이터만 출력했기 때문이에요.

        - 진짜 그런지 확인해 볼까요?

            Left Join을 했을 때 빈 필드가 없는 데이터의 갯수와, Inner Join을 했을때의 전체 데이터의 갯수가 같은지 확인해보면 되겠죠?

            저랑 같이 해볼까요? 

## **03. Join 본격 사용해보기**

- 5) Join 함께 연습해보기

    자, 이제 본격 여러 테이블을 연결해 볼까요? 두근두근! 
    SQL 쿼리는 직접 짜면서 가장 빠르게 배운답니다.

    - [실습] orders 테이블에 users 테이블 연결해보기

        주문 정보에 유저 정보를 연결해 분석을 위한 준비를 하려고 합니다! 우선 inner Join을 사용해서 주문 정보에, 유저 정보를 붙여서 볼까요?

        - 정답 쿼리 살펴보기

            ```sql
            select * from orders o
            inner join users u
            on o.user_id = u.user_id;
            ```

        **[오늘의 팁!]**
        주문을 하기 위해서는 회원정보가 있어야 할테니, orders 테이블에 담긴 user_id는 모두 users 테이블에 존재하겠죠? 

    - [실습] checkins 테이블에 users 테이블 연결해보기

        '오늘의 다짐' 테이블에 유저 정보를 연결해 분석을 위한 준비를 하려고 합니다! 우선 Inner Join을 사용해서 '오늘의 다짐' 테이블에, 유저 테이블을 붙여서 볼까요?

        - 정답 쿼리 살펴보기

            ```sql
            select * from checkins c
            inner join users u
            on c.user_id = u.user_id;
            ```

        **[오늘의 팁!]**

        연결의 기준이 되고싶은 테이블을 from 절에, 
        기준이 되는 테이블에 붙이고 싶은 테이블을 Join 절에 위치해 놓습니다. 

    - [실습] enrolleds 테이블에 courses 테이블 연결해보기

        '수강 등록' 테이블에 과목 정보를 연결해 분석을 위한 준비를 하려고 합니다! 우선 Inner Join을 사용해서 '수강 등록' 테이블에, 과목 테이블을 붙여서 볼까요?

        - 정답 쿼리 살펴보기

            ```sql
            select * from enrolleds e
            inner join courses c
            on e.course_id = c.course_id;
            ```

- 6) SQL 쿼리가 실행되는 순서

    ```sql
    select * from enrolleds e
    inner join courses c
    on e.course_id = c.course_id;
    ```

    위 쿼리가 실행되는 순서: from → join → select

    1. from enrolleds: enrolleds 테이블 데이터 전체를 가져옵니다.
    2. inner join courses on e.course_id = c.course_id: courses를 enrolleds 테이블에 붙이는데, enrolleds 테이블의 course_id와 동일한 course_id를 갖는 courses의 테이블을 붙입니다.
    3. select * : 붙여진 모든 데이터를 출력합니다.

    항상 from에 들어간 테이블을 기준으로, 다른 테이블이 붙는다고 생각하면 편합니다!

## **04. 배웠던 문법을 Join과 함께 사용해보기**

- 7) 배웠던 문법 Join과 함께 연습해보기
    - checkins 테이블에 courses 테이블 연결해서 통계치 내보기

        '오늘의 다짐' 정보에 과목 정보를 연결해 과목별 '오늘의 다짐' 갯수를 세어보자!

        - **[코드스니펫] 과목별 오늘의 다짐 갯수 세어보기**

            ```sql
            select co.title, count(co.title) as checkin_count from checkins ci
            inner join courses co
            on ci.course_id = co.course_id 
            group by co.title
            ```

        **[오늘의 팁!]**

        2주차에 배운 alias는 이렇게 사용하면 편합니다. 연결되는 테이블이 많아지면서 필드명과 테이블명이 헷갈려 실수할 수 있는데, 이렇게 alias를 지정해 주면 편하고 깔끔하게 SQL 쿼리를 작성할 수 있어요.

    - point_users 테이블에 users 테이블 연결해서 순서대로 정렬해보기

        유저의 포인트 정보가 담긴 테이블에 유저 정보를 연결해서, 많은 포인트를 얻은 순서대로 유저의 데이터를 뽑아보자!

        - **[코드스니펫] 많은 포인트를 얻은 순서대로 유저 데이터 정렬해서 보기**

            ```sql
            select * from point_users p
            inner join users u 
            on p.user_id = u.user_id
            order by p.point desc
            ```

    - orders 테이블에 users 테이블 연결해서 통계치 내보기

        주문 정보에 유저 정보를 연결해 네이버 이메일을 사용하는 유저 중, 성씨별 주문건수를 세어보자!

        - **[코드스니펫] 네이버 이메일 사용하는 유저의 성씨별 주문건수 세어보기**

            ```sql
            select u.name, count(u.name) as count_name from orders o
            inner join users u
            on o.user_id = u.user_id 
            where u.email like '%naver.com'
            group by u.name
            ```

- 8) SQL 쿼리가 실행되는 순서

    ```sql
    select u.name, count(u.name) as count_name from orders o
    inner join users u
    on o.user_id = u.user_id 
    where u.email like '%naver.com'
    group by u.name
    ```

    위 쿼리가 실행되는 순서: from → join → where → group by → select

    1. from orders o: orders 테이블 데이터 전체를 가져오고 o라는 별칭을 붙입니다.
    2. inner join users u on o.user_id = u.user_id : users 테이블을 orders 테이블에 붙이는데, orders 테이블의 user_id와 동일한 user_id를 갖는 users 테이블 데이터를 붙입니다. (*users 테이블에 u라는 별칭을 붙입니다)
    3. where u.email like '%naver.com': users 테이블 email 필드값이 naver.com으로 끝나는 값만 가져옵니다.
    4. group by u.name: users 테이블의 name값이 같은 값들을 뭉쳐줍니다.
    5. select u.name, count(u.name) as count_name : users 테이블의 name필드와 name 필드를 기준으로 뭉쳐진 갯수를 세어서 출력해줍니다. 

    Join의 실행 순서는 항상 from 과 붙어다닌다고 생각하면 편해요!

## **05. 이제는 실전! 본격 쿼리 작성해보기**

- 9) [퀴즈] Join 연습1

    결제 수단 별 유저 포인트의 평균값 구해보기
    (어느 결제수단이 가장 열심히 듣고 있나~)

    join 할 테이블: `point_users` 에, `orders` 를 붙이기

    꿀팁! → `round(숫자,자릿수)` 를 이용해서 반올림을 해볼까요?

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%208.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%208.png)

    - 정답 쿼리 살펴보기!

        ```sql
        select o.payment_method, round(AVG(p.point)) from point_users p
        inner join orders o 
        on p.user_id = o.user_id 
        group by o.payment_method
        ```

        이해가 안 되신다고요? 저랑 같이 해봐요!

- 10) [퀴즈] Join 연습2

    결제하고 시작하지 않은 유저들을 성씨별로 세어보기
    (어느 성이 가장 시작을 안하였는가~)

    join 할 테이블: `enrolleds` 에, `users` 를 붙이기

    꿀팁! → `is_registered = 0` 인 사람들을 세어보아요!

    꿀팁! → `order by` 를 이용해서 내림차순으로 정렬하면 보기 좋겠죠?

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%209.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%209.png)

    - 정답 쿼리 살펴보기!

        ```sql
        select name, count(*) as cnt_name from enrolleds e
        inner join users u
        on e.user_id = u.user_id 
        where is_registered = 0
        group by name
        order by cnt_name desc
        ```

        이해가 안 되신다고요? 저랑 같이 해봐요!

- 11) [퀴즈] Join 연습3

    과목 별로 시작하지 않은 유저들을 세어보기

    join 할 테이블: `courses`에, `enrolleds` 를 붙이기

    꿀팁! → `is_registered = 0` 인 사람들을 세어보아요!

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2010.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2010.png)

    - 정답 쿼리 살펴보기!

        ```sql
        select c.course_id, c.title, count(*) as cnt_notstart from courses c
        inner join enrolleds e 
        on c.course_id = e.course_id
        where is_registered = 0
        group by c.course_id
        ```

        이해가 안 되신다고요? 저랑 같이 해봐요!

## **06. 이렇게 끝내면 아쉽죠? 한번 더 총복습!**

- 12) [퀴즈] Join 연습4

    웹개발, 앱개발 종합반의 week 별 체크인 수를 세어볼까요? 보기 좋게 정리해보기!

    join 할 테이블: `courses`에, `checkins` 를 붙이기

    꿀팁! → group by, order by에 `콤마`로 이어서 두 개 필드를 걸어보세요!

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2011.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2011.png)

    - 정답 쿼리 살펴보기!

        ```sql
        select c1.title, c2.week, count(*) as cnt from checkins c2
        inner join courses c1 on c2.course_id = c1.course_id
        group by c1.title c2.week
        order by c1.title, c2.week
        ```

        이해가 안 되신다고요? 저랑 같이 해봐요!

- 13) [퀴즈] Join 연습5

    연습4번에서, 8월 1일 이후에 구매한 고객들만 발라내어 보세요!

    join 할 테이블: `courses`에, `checkins` 를 붙이고!
    + `checkins` 에, `orders` 를 한번 더 붙이기!

    꿀팁! → `orders` 테이블에 inner join을 한번 더 걸고, where 절로 마무리!

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2012.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2012.png)

    - 정답 쿼리 살펴보기!

        ```sql
        select c1.title, c2.week, count(*) as cnt from courses c1
        inner join checkins c2 on c1.course_id = c2.course_id
        inner join orders o on c2.user_id = o.user_id
        where o.created_at >= '2020-08-01'
        group by c1.title, c2.week
        order by c1.title, c2.week
        ```

        이해가 안 되신다고요? 저랑 같이 해봐요!

## **07. Left Join - 안써보니까 섭섭했죠?**

- 14) 다시한번 복습! inner join vs left join

    inner join 은 교집합, left join 은 첫번째 원에 붙이는 것!

    - 그림으로 복습하기
        - inner join

            ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%207.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%207.png)

        - left join

            ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%206.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%206.png)

    - 그래서! left join은 `어디에 → 뭐를 붙일건지, 순서가 중요`하답니다!
- 15) Left join 언제쓸까요? (복습)

    바로 한번 볼까요?

    예를 들면 모든 유저가 포인트를 갖고 있지를 않을 수 있잖아요!

    - users 테이블과 ↔ point_users 테이블을 left join 해봅시다.

        ```jsx
        select * from users u
        left join point_users pu on u.user_id = pu.user_id
        ```

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2013.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2013.png)

    - 이 상태에선, 이런 게 가능합니다.

        유저 중에, 포인트가 없는 사람(=즉, 시작하지 않은 사람들)의 통계!
        속닥속닥) `is NULL` , `is not NULL` 을 함께 배워보아요!

        ```jsx
        select name, count(*) from users u
        left join point_users pu on u.user_id = pu.user_id
        where pu.point_user_id is NULL
        group by name
        ```

        ```jsx
        select name, count(*) from users u
        left join point_users pu on u.user_id = pu.user_id
        where pu.point_user_id is not NULL
        group by name
        ```

- 16) [퀴즈] 여기서 퀴즈! - 막해보기

    7월10일 ~ 7월19일에 가입한 고객 중,
    포인트를 가진 고객의 숫자, 그리고 전체 숫자, 그리고 비율을 보고 싶어요!

    아래와 같은 결과를 보고 싶다면 어떻게 해야할까요?

    - 이렇게 저렇게 해볼까요?

        힌트1 → `count` 은 NULL을 세지 않는답니다!

        힌트2 → Alias(별칭)도 잘 붙여주세요!

        힌트3 → 비율은 소수점 둘째자리에서 반올림!

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2014.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2014.png)

    - 정답 쿼리 살펴보기

        ```sql
        select count(point_user_id) as pnt_user_cnt,
               count(*) as tot_user_cnt,
               round(count(point_user_id)/count(*),2) as ratio
          from users u
          left join point_users pu on u.user_id = pu.user_id
         where u.created_at between '2020-07-10' and '2020-07-20'
        ```

## **08. 결과물 합치기! Union 배우기**

- 17) Select를 두 번 할 게 아니라, 한번에 모아서 보고싶은 경우, 있을걸요!
    - 예를 들면 이렇게!

        근데, 그러려면 한 가지 조건이 있어요! 노란색과 파란색 박스의 필드명이 같아야 한답니다. 🙂 (당연하겠죠?)

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2015.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2015.png)

- 18) Union을 이용해서 아래와 같은 모습을 만들어볼까요?
    - **[코드스니펫] - 퀴즈5 쿼리**

        ```jsx
        select c1.title, c2.week, count(*) as cnt from courses c1
        inner join checkins c2 on c1.course_id = c2.course_id
        inner join orders o on c2.user_id = o.user_id
        where o.created_at >= '2020-08-01'
        group by c1.title, c2.week
        order by c1.title, c2.week
        ```

    - 보고 싶은 모습!

        ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2016.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2016.png)

    - 우선, 'month'를 붙여줘야겠네요!

        ```sql
        select '7월' as month, c.title, c2.week, count(*) as cnt from checkins c2
        inner join courses c on c2.course_id = c.course_id
        inner join orders o on o.user_id = c2.user_id
        where o.created_at < '2020-08-01'
        group by c2.course_id, c2.week
        order by c2.course_id, c2.week
        ```

    - 여기에 아래 위로 `Union all`을 사용해 붙여주면 끝!

        ```sql
        (
        	select '7월' as month, c.title, c2.week, count(*) as cnt from checkins c2
        	inner join courses c on c2.course_id = c.course_id
        	inner join orders o on o.user_id = c2.user_id
        	where o.created_at < '2020-08-01'
        	group by c2.course_id, c2.week
          order by c2.course_id, c2.week
        )
        union all
        (
        	select '8월' as month, c.title, c2.week, count(*) as cnt from checkins c2
        	inner join courses c on c2.course_id = c.course_id
        	inner join orders o on o.user_id = c2.user_id
        	where o.created_at > '2020-08-01'
        	group by c2.course_id, c2.week
          order by c2.course_id, c2.week
        )
        ```

    - 앗, 그런데, 한 가지! 정렬이 깨졌네요!? 😂

        네 맞습니다! union을 사용하면 내부 정렬이 먹지 않아요.
        이 때 유용한 방법이 있지요. 바로, SubQuery(서브쿼리) !

        - 그런데 이번주는 푹 쉬구요! 4주차에 나올 거니까 기대해주세요!

## 09**. 끝 & 숙제 설명**

이번 3주차도 고생 많았습니다. 역시 한 주의 마무리는 숙제죠!

숙제: enrolled_id별 수강완료(done=1)한 강의 갯수를 세어보고, 완료한 강의 수가 많은 순서대로 정렬해보기. user_id도 같이 출력되어야 한다.

- 힌트!
    - 조인해야 하는 테이블: `enrolleds`, `enrolleds_detail`
    - 조인하는 필드: `enrolled_id`
- 결과

    ![SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2017.png](SQL%20BASIC%20WEEK%203%20501599a6ac874eb0bf50d533dbe137f8/Untitled%2017.png)

    이런 결과가 나오면 정답! 👏

## 10. 3주차 숙제 답안 코드

- **[코드스니펫] - 3주차 숙제 답안 코드**

    ```sql
    select e.enrolled_id,
    	     e.user_id,
    	     count(*) as cnt
      from enrolleds e
     inner join enrolleds_detail ed on e.enrolled_id = ed.enrolled_id
     where ed.done = 1
     group by e.enrolled_id, e.user_id
     order by cnt desc
    ```