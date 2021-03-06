# π νλ μ΄λ νΈμΉ΄

> κ³ κ°μ΄ μ°¨λ μ‘°ν/λμ¬/λ°λ©μ ν  μ μκ³ , κ΄λ¦¬μλ μ°¨λ λ±λ‘/μ­μ /λͺ¨λ  λμ¬ λ΄μ­μ μ‘°νν  μ μλ λ νΈμΉ΄ μμ½ μμ€ν


# 1. Modeling
![image](https://user-images.githubusercontent.com/74531573/129319247-d86c26e5-917b-4bc1-adf8-7958e8e2acc7.png)


# 2. SQL

## DDL

```sql
DROP TABLE customer cascade constraint;
DROP TABLE car cascade constraint;
DROP TABLE rent cascade constraint;

DROP SEQUENCE customer_idx;
DROP SEQUENCE car_idx;
DROP SEQUENCE rent_idx;

CREATE TABLE customer (
       customer_id	NUMBER	 PRIMARY KEY,
       name         VARCHAR2(20) NOT NULL,
       phone        VARCHAR2(13) NOT NULL,
       license      VARCHAR2(20) NOT NULL
);

CREATE TABLE car (
       car_id       NUMBER PRIMARY KEY,
       model        VARCHAR2(50) NOT NULL,
       brand        VARCHAR2(20) NOT NULL,
       cartype   		VARCHAR2(20) NOT NULL,
       price	 			NUMBER NOT NULL,
       is_rent			VARCHAR2(1) DEFAULT '0'
);

CREATE TABLE rent (
       rent_id			NUMBER PRIMARY KEY,
       startday     DATE NOT NULL,
       endday  			DATE NOT NULL,
       customer_id	NUMBER NOT NULL,
       car_id				NUMBER,
       returnday		DATE DEFAULT NULL       
);

ALTER TABLE rent ADD FOREIGN KEY (customer_id) REFERENCES customer (customer_id);
ALTER TABLE rent ADD FOREIGN KEY (car_id) REFERENCES car (car_id) ON DELETE SET NULL;

CREATE SEQUENCE customer_idx START WITH 1 INCREMENT BY 1 MAXVALUE 10000000 CYCLE NOCACHE;
CREATE SEQUENCE car_idx START WITH 1 INCREMENT BY 1 MAXVALUE 10000000 CYCLE NOCACHE;
CREATE SEQUENCE rent_idx START WITH 1 INCREMENT BY 1 MAXVALUE 10000000 CYCLE NOCACHE;
```

## DML

```sql
-- customer insert[κ³ κ° μ λ³΄ μ μ₯]
insert into customer values(customer_idx.NEXTVAL, 'μ μ¬μ', '010-2384-2842', '11-23-293847-38');
insert into customer values(customer_idx.NEXTVAL, 'μ λμ½', '010-3829-3892', '42-38-293832-38');
insert into customer values(customer_idx.NEXTVAL, 'μ΄μμ', '010-3298-2938', '23-28-589334-38');
insert into customer values(customer_idx.NEXTVAL, 'μ μ§ν', '010-1232-8313', '23-23-173723-70');
insert into customer values(customer_idx.NEXTVAL, 'μ°¨μ¬ν', '010-9373-1743', '12-38-127942-27');
insert into customer values(customer_idx.NEXTVAL, 'μ₯νλ―Ό', '010-7124-3813', '98-02-379134-63'); 

-- car insert[λ νΈμΉ΄ μ λ³΄ μ μ₯]
insert into car values(car_idx.NEXTVAL, 'μ€νν¬', 'μλ³΄λ ', 'κ²½μ°¨', 10000, '0');
insert into car values(car_idx.NEXTVAL, 'μλ°λΌ', 'νλ', 'μ€μ€ν', 20000, '0');
insert into car values(car_idx.NEXTVAL, 'λ μ΄', 'κΈ°μ', 'κ²½μ°¨', 10000, '0');
insert into car values(car_idx.NEXTVAL, 'νΈλ λΈλ μ΄μ ', 'μλ³΄λ ', 'SUV', 25000, '0');
insert into car values(car_idx.NEXTVAL, 'K5', 'κΈ°μ', 'μ€ν', 10000, '0');
insert into car values(car_idx.NEXTVAL, 'S500', 'λ²€μΈ ', 'μΈλ¨', 60000, '0');

-- rent insert[μμ½ μ λ³΄ μ μ₯]
insert into rent values(rent_idx.NEXTVAL, TO_DATE('2021-07-21'), TO_DATE('2021-08-01'), 2, 1, TO_DATE('2021-08-01'));
insert into rent values(rent_idx.NEXTVAL, TO_DATE('2021-08-08'), TO_DATE('2021-08-10'), 3, 2, TO_DATE('2021-08-10'));
insert into rent values(rent_idx.NEXTVAL, TO_DATE('2021-06-01'), TO_DATE('2021-07-31'), 1, 3, TO_DATE('2021-07-31'));
insert into rent values(rent_idx.NEXTVAL, TO_DATE('2021-08-02'), TO_DATE('2021-08-04'), 2, 5, TO_DATE('2021-08-04'));

commit;
```

# 3. Class Diagram
![classDiagram](https://user-images.githubusercontent.com/74531573/129318723-4b8a60e6-7027-451d-bf59-8857bba222b3.gif)



# 4. Function

[κ³ κ°]

1. λͺ¨λ  μ°¨λ μ‘°ννκΈ°
2. μ‘°κ±΄μΌλ‘ μ°¨λ μ‘°ννκΈ° (λͺ¨λΈλͺ, μ°¨μ’, λΈλλ)
    - μ‘°κ±΄μ λ§λ μ°¨λ μ‘΄μ¬νμ§ μμ μ μμΈμ²λ¦¬
3. λμ¬ κ°λ₯ν μ°¨λ μ‘°ν
4. μ°¨λ λμ¬νκΈ°
    - λ°λ©μμ μΌ, κ³ κ°λ²νΈ, μ°¨λλ²νΈλ§ μλ ₯λ°λλ‘ ν¨ (μμ½λ²νΈ, λμ¬μΌμ μλ μμ±)
    - μλ μ°¨λ λ²νΈλ‘ λμ¬ μ μμΈμ²λ¦¬
5. μ°¨λ λ°λ©νκΈ°
    - μλ μμ½λ²νΈλ‘ λ°λ© μ μμΈμ²λ¦¬
6. μμ½ μ‘°ννκΈ° 
    - μλ κ³ κ°λͺμΌλ‘ μμ½ μ‘°ν μ μμΈμ²λ¦¬
7. κ³ κ° λ±λ‘νκΈ°

[κ΄λ¦¬μ]

1. μ°¨λ λ±λ‘νκΈ°
    - μ°¨λ λͺ¨λΈ, λΈλλ, μ μ‘°μ¬, κ°κ²©λ§ μλ ₯λ°λλ‘ ν¨ (λ±λ‘λ²νΈ, λμ¬μ¬λΆ μλ μμ±)
    - μ°¨λ κ°κ²©μ μ«μ ννλ‘ μλ ₯νμ§ μμ μ μμΈμ²λ¦¬
2. μ°¨λ μ­μ νκΈ°
    - μμ½μ€μΈ μ°¨λ μ­μ μ rent νμ΄λΈμμ ν΄λΉ μ°¨λμ car_id κ°μ Nullλ‘ λ³κ²½νκ³  μ­μ νκΈ°

 

# 5. Code Review

- μ°¨λ λμ¬ κΈ°λ₯ - μλ μ°¨λ λ²νΈλ‘ μμ½ μλν΄λ μμ½ μ±κ³΅ λ©μΈμ§ μΆλ ₯   / ν΄κ²° μλ£
- μ°¨λ μ­μ  κΈ°λ₯ - car νμ΄λΈμμ μ°¨λ μ­μ μ, rent νμ΄λΈμμ ν΄λΉ car_idκ° Nullλ‘ λ°λ (ON DELETE SET NULL) β null λ§κ³  μ°¨λλ²νΈμ κ΅¬λ³λλ λ€λ₯Έ μ«μλ‘ λ°κΎΈκΈ°  / λ―Έμμ±
- κ³ κ° νμ΄λΈ - νμ¬ κ³ κ° μΆκ° κΈ°λ₯λ§ μμ΄μ λ€λ₯Έ λ©μλλ κ΅¬ννλ©΄ μ’κ² λ€  / κ°μ  μμ  (ex. κ³ κ° λ¦¬μ€νΈ μ‘°ν κΈ°λ₯ ...)

# 6. λ―Έν‘ν μ 

- μ°¨λ λμ¬ κΈ°λ₯ - ν λ μ§λ³΄λ€ μ΄μ  λ μ§ μλ ₯μ / μλ κ³ κ°λ²νΈ μλ ₯μμ λν μμΈμ²λ¦¬
- μ¬μ©μ μλͺ» μλ ₯μ μ¬μλ ₯ λ°κΈ°
