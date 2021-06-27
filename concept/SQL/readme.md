# DB+MySQL복습

- 하는 이유 :  DB는 면접대비 SQL은 코테대비 SQL 면접에서 판서로 작성해보라고도 했음. 억울해서 배워야함.
- 참고 : 학부때의 강의자료

<[https://github.com/kkminseok/DB_SQL_Review](https://github.com/kkminseok/DB_SQL_Review)>

- 이미지는 나중에 전부 수정하겠습니다.

- 개념

- SQL(문제푼 것, 다같이 풀어보아요. ㅎ)

    leetcode 175(Eazy) - Combine Two Tables 문제 : 

    <[https://leetcode.com/problems/combine-two-tables/](https://leetcode.com/problems/combine-two-tables/)>

# **SQL 문법**

---

**기본 문법**

- SELECT, count(), DISTINCT

    ## SELECT

    **기본 질의어**

    ```sql
    SELECT first_name FROM employees.employees;

    ```

    결과

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/select1.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/select1.jpg)

    **count()  - 데이터의 갯수를 센다.**

    - ()안에 *가 있을 경우 **전체 행을 가져오고**
    - ()안에 **컬럼명**을 넣을 시 해당 컬럼의 갯수를 가져온다
    - **NULL인 데이터는 제외하고 계산한다.**

    ```sql
    SELECT count(first_name) FROM employees.employees;
    --별칭을 주면 다르게 이름 가능--

    ```

    결과

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/select2.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/select2.jpg)

    **DISTINCT - 중복제거**

    ```sql
    SELECT count(distinct first_name) FROM employees.employees;

    ```

    결과

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/select3.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/select3.jpg)

- WHERE(<, >, ≥, ≤, <>는 ≠,  Like, BETWEEN, IN, AND, OR , NOT)

    특이점으로 BETWEEN은 (x,y] 표기법이다. → x**초과** y**이하**

    NOT 뒤에 조건이 오는 것.

    ```sql
    SELECT * FROM employees.employees where emp_no = 10001;
    SELECT * FROM employees.employees where emp_no > 10500;
    SELECT * FROM employees.employees where emp_no < 10500;
    SELECT * FROM employees.employees where emp_no >= 10500;
    SELECT * FROM employees.employees where emp_no <= 10500;
    SELECT * FROM employees.employees where emp_no <> 10500;
    SELECT * FROM employees.employees where emp_no BETWEEN 10000 and 10100;
    SELECT * FROM employees.employees where last_name LIKE('Facello');
    SELECT * FROM employees.employees where emp_no IN (10001,10005);
    SELECT * FROM employees.employees where last_name = 'Facello' or last_name = 'Simmel';
    SELECT * FROM employees.employees where last_name = 'Facello' or first_name = 'Bezalel';
    SELECT * FROM employees.employees where NOT last_name = 'Facello';
    SELECT * FROM employees.employees 
    where last_name = 'Facello' and (emp_no > 14900 or emp_no < 10100);
    SELECT * FROM employees.employees 
    where NOT last_name = 'Facello' and NOT emp_no > 20000;
    ```

    BETWEEN 결과 : 

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/Untitled.png](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/Untitled.png)

    ...

- Order by - ASC(오름차순), DESC(내림차순)

    ```sql
    SELECT * FROM employees.employees order by last_name;
    SELECT * FROM employees.employees order by last_name DESC;
    SELECT * FROM employees.employees order by last_name, first_name;
    SELECT * FROM employees.employees order by last_name, first_name DESC;
    ```

- INTO

    ```sql
    INSERT INTO table_name (column1, column2, column3, ...)
    VALUES (value1, value2, value3, ...);
    //전체가 아닌 몇개만 값을 지정하고 테이블에 추가하고 싶을때 사용

    INSERT INTO table_name
    VALUES (value1, value2, value3, ...);
    //전체 값을 지정하고 테이블에 추가하고 싶을때 사용
    ```

- NULL

    ```sql
    SELECT * FROM employees.employees WHERE first_name IS NULL;
    SELECT * FROM employees.employees WHERE first_name IS NOT NULL;
    ```

- UPDATE

    ```sql
    UPDATE table_name
    SET column1 = value1, column2 = value2, ...
    WHERE condition;
    --키 안전조건 때문에 예제는..

    UPDATE employees.employees
    SET employees.first_name = 'kms'
    WHERE employees.last_name = 'Facello';
    ```

- DELETE

    ```sql

    DELETE FROM table_name WHERE condition;
    ```

- SELECT + TOP

    ```sql
    -- 기본 문법
    SELECT column_name(s)
    FROM table_name
    WHERE condition
    LIMIT number;

    -- 예제
    SELECT *
    FROM employees.employees
    WHERE emp_no > 10005
    LIMIT 3;
    --emp_no가 10005을 넘는 데이터를 위에서 3개의 데이터만 출력

    ```

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/top.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/top.jpg)

- Min(), Max()

    ```sql
    SELECT MAX(employees.birth_date), MIN(employees.birth_date) AS min_emp_birth
    FROM employees.employees
    WHERE employees.emp_no > 10500;

    -- emp_no이 10500을 넘는 것중 birth_date가 제일 큰 값, 제일 작은 값을 찾아 보여준다.
    작은 값의 이름은 min_emp_birth로 한다.
    ```

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/min.max.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/min.max.jpg)

- Count(), Sum(), AVG()

    ```sql
    -- COUNT() function : 조건에 맞는 row의 갯수

    -- The AVG() : numeric colum의 평균 값 출력

    -- The SUM() : numeric colum의 총합 출력

    -- date형식도 되는데 원하는 값이 나오지는 않는다.

    -- 예제
    SELECT COUNT(emp_no), AVG(emp_no), SUM(emp_no), AVG(birth_date), SUM(birth_date), COUNT(birth_datE)
    FROM employees.employees;
    ```

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/count_sum_avg.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/count_sum_avg.jpg)

- Like operator, NOT LIKE

    % : 0개나 1개의 문자를 의미

    _ : 1개의 문자를 의미

    NOT 과 사용할 경우 NOT이 먼저 나와야함. NOT LIKE임.

    ```sql
    -- SELECT column1, column2, ...
    -- FROM table_name
    -- WHERE columnN LIKE pattern;

    -- 예제
    -- last_name이 F로 시작하는 것들.
    SELECT last_name
    FROM employees.employees
    WHERE last_name LIKE 'F%';

    -- last_name이 F로 시작하고 문자열의 길이가 5인 것들.
    SELECT last_name
    FROM employees.employees
    WHERE last_name LIKE 'F____';

    -- F로 끝나는 것들.
    SELECT last_name
    FROM employees.employees
    WHERE last_name LIKE '%F';

    -- F로 시작하고 a로 끝나는 것들.
    SELECT last_name
    FROM employees.employees
    WHERE last_name LIKE 'F%a';

    -- F로 시작하고 a는 아무데나 있으면 되는 경우.(끝 포함.)
    SELECT last_name
    FROM employees.employees
    WHERE last_name LIKE 'F%a%';

    -- F로 시작하고 a는 아무데나 있으면 되는 경우를 제외한 경우.(끝 포함.)
    SELECT last_name
    FROM employees.employees
    WHERE last_name NOT LIKE  'F%a%';
    ```

- IN operator

    ```sql
    -- 기본 구문

    SELECT column_name(s)
    FROM table_name
    WHERE column_name IN (value1, value2, ...);

    SELECT column_name(s)
    FROM table_name
    WHERE column_name IN (SELECT STATEMENT);

    -- 예제

    -- last_name이 'Facello'이거나, 'Koblick'인 사람의 emp_no를 찾기

    SELECT emp_no
    FROM employees.employees
    WHERE last_name IN ('Facello', 'Koblick');

    -- employees 테이블의 last_name을 찾는데, dept_manage에 있는 emp_no에 속해있는 사람들을 뽑음

    SELECT last_name
    FROM employees.employees
    WHERE emp_no IN (SELECT emp_no FROM employees.dept_manager);
    ```

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/inoper.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/inoper.jpg)

- BETWEEN + 날짜, 여러구문

    ```sql
    -- birthdate가 1953년 09.02 부터 1954.05.01까지인 사람. 또한 emp_no가 10500을 넘지 않는 사람
    SELECT *
    FROM employees.employees
    WHERE birth_date BETWEEN '1953-09-02' AND '1954-05-01' 
    AND NOT emp_no > 10500;

    ```

- AS + CONCAT(), table AS

    ```sql
    -- firstname과 emp_no을 ','로 구문하여 합친 것을 hello라는 column으로 보여줌.
    SELECT last_name, CONCAT(first_name, ', ', emp_no) AS hello
    FROM employees.employees;
    ```

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/asconcat.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/asconcat.jpg)

    ```sql
    -- emp_no와 title을 보여준다. employees 테이블은 e로, titles테이블은 t로 축약.
    SELECT e.emp_no, t.title
    FROM employees.employees AS e, employees.titles AS t
    WHERE e.emp_no = t.emp_no;

    ```

    ![DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/astable.jpg](DB+MySQL%E1%84%87%E1%85%A9%E1%86%A8%E1%84%89%E1%85%B3%E1%86%B8%208fe4dfdca0b5480f94a7faf735c93be2/astable.jpg)

-