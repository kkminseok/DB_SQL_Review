# **SQL 문법**

-----

## SELECT

**기본 질의어**

```SQL
SELECT first_name FROM employees.employees;
```


**count()  - 데이터의 갯수를 센다.**
- ()안에 *가 있을 경우 **전체 행을 가져오고**
- ()안에 **컬럼명**을 넣을 시 해당 컬럼의 갯수를 가져온다
- **NULL인 데이터는 제외하고 계산한다.**

![](select/select1.JPG)  


```SQL
SELECT count(first_name) FROM employees.employees;
```

**DISTINCT - 중복제거**

![](select/select2.JPG)  

```SQL
SELECT count(distinct first_name) FROM employees.employees;
```

![](select/select3.JPG)  