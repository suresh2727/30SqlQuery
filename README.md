# 30SqlQuery

1) WAQTD THE EMP FIRST NAME , LAST NAME , WHOSE NAME AS 2ND CHAR SHOULD BE 'A';

--> SELECT FIRST_NAME , LAST_NAME FROM EMP WHERE FIRST_NAME LIKE '_A%';
+------------+-----------+
| FIRST_NAME | LAST_NAME |
+------------+-----------+
| RAHUL      | MUKARJEE  |
| SAMEER     | KHAN      |
| KARAN      | BHAT      |
| MAURALI    | KRISHNAN  |
| RASHMI     | GOWDA     |
| FARIYA     | TAJ       |
+------------+-----------+


2) WAQTD THE DETAILS OF EMPLOYEE WHOSE DEPT NO IS SAME AS KARAN'S DEPT NO 

-->  SELECT * FROM EMP WHERE DNO IN (SELECT DNO FROM EMP WHERE FIRST_NAME = 'KARAN');
+------+------------+-----------+------------+--------+----------+------+------------+-----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB      | MGR  | DOJ        | SAL       | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+----------+------+------------+-----------+---------+------+------+
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER  | 1602 | 2017-04-17 | 100000.00 |    NULL |  111 | NULL |
| 1903 | KARAN      | BHAT      | 1997-12-26 | M      | SALESMAN | 1701 | 2019-12-26 |  45000.00 |    NULL |  111 | NULL |
| 2101 | RASHMI     | GOWDA     | 1995-10-03 | f      | SALESMAN | 1701 | 2021-01-02 |  45000.00 | 3000.00 |  111 | NULL |
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN | 1701 | 2021-12-26 |  40000.00 |    NULL |  111 | NULL |
+------+------------+-----------+------------+--------+----------+------+------------+-----------+---------+------+------+ 


3) WAQTD THE DETAILS OF EMPLOYEE WHO ARE GETTING SAL MORE THAN ABHIJIT

-->  SELECT * FROM EMP WHERE SAL > (SELECT SAL FROM EMP WHERE FIRST_NAME = 'ABHIJIT');
+------+------------+-----------+------------+--------+---------+------+------------+-----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB     | MGR  | DOJ        | SAL       | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+---------+------+------------+-----------+------+------+------+
| 1601 | SIDDARTH   | PATIL     | 1985-11-24 | M      | CEO     | NULL | 2016-01-16 | 500000.00 | NULL |  113 | NULL |
| 1602 | HEMA       | SHETTY    | 1996-03-20 | F      | HR      | 1601 | 2016-10-20 | 150000.00 | NULL |  112 |  507 |
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER | 1602 | 2017-04-17 | 100000.00 | NULL |  111 | NULL |
| 1702 | SAMEER     | KHAN      | 1995-04-20 | M      | MANAGER | 1602 | 2017-07-07 |  90000.00 | NULL |  110 | NULL |
+------+------------+-----------+------------+--------+---------+------+------------+-----------+------+------+------+


4) WAQTD THE WORKING LOCATIONS OF THE EMP WHO BELONGS TO ACCOUNTING DEPT 

-->   SELECT * FROM LOCATION WHERE LID IN (SELECT LID FROM DEPT WHERE DNAME = 'ACCOUNTING');
+-----+-------------+-----------+-----------+
| LID | LOCATION    | CITY      | STATE     |
+-----+-------------+-----------+-----------+
|   1 | VIJAYANAGAR | BANGALORE | KARNATAKA |
+-----+-------------+-----------+-----------+

-->  SELECT L1.* FROM LOCATION L1 INNER JOIN DEPT D1 ON L1.LID=D1.LID WHERE D1.DNAME = 'ACCOUNTING';
+-----+-------------+-----------+-----------+
| LID | LOCATION    | CITY      | STATE     |
+-----+-------------+-----------+-----------+
|   1 | VIJAYANAGAR | BANGALORE | KARNATAKA |
+-----+-------------+-----------+-----------+


5*) WAQTD ALL THE EMPLOYEES WHO ARE ALSO THE CUSTOMERS OF THAT PARTICULAR COMPANY

-->  SELECT * FROM EMP WHERE EID IN (SELECT EID FROM ORDERS WHERE ORDER_ID IN (SELECT ORDER_ID FROM CUSTOMER WHERE ORDER_ID IS NOT NULL));
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 | 50000.00 |    NULL |  110 |  505 |
| 2001 | MAURALI    | KRISHNAN  | 1998-06-08 | M      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+


6)  WAQTD ALL THE EMP WHOSE JOB NOT SAME AS DHARANI AND SAL GREATHER THAN FARIYA

-->  SELECT * FROM EMP WHERE JOB NOT IN(SELECT JOB FROM EMP WHERE FIRST_NAME ='DHARANI') AND SAL >ALL(SELECT SAL FROM EMP WHERE FIRST_NAME ='FARIYA');
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL       | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+
| 1601 | SIDDARTH   | PATIL     | 1985-11-24 | M      | CEO        | NULL | 2016-01-16 | 500000.00 |    NULL |  113 | NULL |
| 1602 | HEMA       | SHETTY    | 1996-03-20 | F      | HR         | 1601 | 2016-10-20 | 150000.00 |    NULL |  112 |  507 |
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER    | 1602 | 2017-04-17 | 100000.00 |    NULL |  111 | NULL |
| 1702 | SAMEER     | KHAN      | 1995-04-20 | M      | MANAGER    | 1602 | 2017-07-07 |  90000.00 |    NULL |  110 | NULL |
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 |  45000.00 | 1000.00 |  110 | NULL |
| 1901 | SHIVANI    | RAI       | 1998-11-07 | f      | TESTER     | 1601 | 2019-12-12 |  45000.00 |    NULL |  113 |  502 |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 |  50000.00 |    NULL |  110 |  505 |
| 1903 | KARAN      | BHAT      | 1997-12-26 | M      | SALESMAN   | 1701 | 2019-12-26 |  45000.00 |    NULL |  111 | NULL |
| 2001 | MAURALI    | KRISHNAN  | 1998-06-08 | M      | DISPATCHER | 1702 | 2020-03-15 |  45000.00 | 1000.00 |  110 | NULL |
| 2101 | RASHMI     | GOWDA     | 1995-10-03 | f      | SALESMAN   | 1701 | 2021-01-02 |  45000.00 | 3000.00 |  111 | NULL |
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN   | 1701 | 2021-12-26 |  40000.00 |    NULL |  111 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+



7) WAQTD THE DETAILS OF EMP WHO JOINED AFTER TWO YEARS OF FIRST EMP OF THE COMPANY AND MORE THAN AMAN'S SAL

--> 



8) LIST ALL THE DETAILS OF EMP WHOSE JOB IS SAME AS RASHMI AND THEIR SAL LESS THAN NAIK 

-->  SELECT * FROM EMP WHERE JOB IN (SELECT JOB FROM EMP WHERE FIRST_NAME ='RASHMI') AND SAL < ALL(SELECT SAL FROM EMP WHERE LAST_NAME ='NAIK');
+------+------------+-----------+------------+--------+----------+------+------------+----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB      | MGR  | DOJ        | SAL      | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+----------+------+------------+----------+------+------+------+
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN | 1701 | 2021-12-26 | 40000.00 | NULL |  111 | NULL |
+------+------------+-----------+------------+--------+----------+------+------------+----------+------+------+------+


9) WAQTD ALL THE DEPT INFORMATION OF EMP WHO IS WORKING FOR MYSORE LOCATION

--> 
mysql> SELECT D1.* FROM DEPT D1 INNER JOIN LOCATION L1 ON D1.LID=L1.LID WHERE L1.CITY='MYSORE';
+-----+-----------+-----+
| DNO | DNAME     | LID |
+-----+-----------+-----+
| 110 | DELIVERY  |   2 |
| 111 | MARKETING |   2 |
+-----+-----------+-----+


10) WAQTD ALL THE EMP WHO ARE JOINED BEFORE THE LAST PERSON

--> SELECT * FROM EMP WHERE DOJ NOT IN(SELECT MAX(DOJ) FROM EMP);
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL       | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+
| 1601 | SIDDARTH   | PATIL     | 1985-11-24 | M      | CEO        | NULL | 2016-01-16 | 500000.00 |    NULL |  113 | NULL |
| 1602 | HEMA       | SHETTY    | 1996-03-20 | F      | HR         | 1601 | 2016-10-20 | 150000.00 |    NULL |  112 |  507 |
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER    | 1602 | 2017-04-17 | 100000.00 |    NULL |  111 | NULL |
| 1702 | SAMEER     | KHAN      | 1995-04-20 | M      | MANAGER    | 1602 | 2017-07-07 |  90000.00 |    NULL |  110 | NULL |
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 |  45000.00 | 1000.00 |  110 | NULL |
| 1901 | SHIVANI    | RAI       | 1998-11-07 | f      | TESTER     | 1601 | 2019-12-12 |  45000.00 |    NULL |  113 |  502 |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 |  50000.00 |    NULL |  110 |  505 |
| 1903 | KARAN      | BHAT      | 1997-12-26 | M      | SALESMAN   | 1701 | 2019-12-26 |  45000.00 |    NULL |  111 | NULL |
| 2001 | MAURALI    | KRISHNAN  | 1998-06-08 | M      | DISPATCHER | 1702 | 2020-03-15 |  45000.00 | 1000.00 |  110 | NULL |
| 2002 | DHARANI    | PATIL     | 1998-11-10 | f      | DEVELOPER  | 1601 | 2021-06-20 |  30000.00 | 3000.00 |  113 | NULL |
| 2101 | RASHMI     | GOWDA     | 1995-10-03 | f      | SALESMAN   | 1701 | 2021-01-02 |  45000.00 | 3000.00 |  111 | NULL |
| 2102 | FARIYA     | TAJ       | 1999-01-03 | f      | DEVELOPER  | 1601 | 2021-03-01 |  32000.00 | 3600.00 |  113 | NULL |
| 2103 | PRIYA      | SHETTY    | 1998-03-20 | f      | ACCOUNTANT | 1602 | 2021-05-01 |  32000.00 | 3600.00 |  112 | NULL |
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN   | 1701 | 2021-12-26 |  40000.00 |    NULL |  111 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+



11) WAQTD THE EMP DETAILS WITH THEIR ANNUAL SAL WHO EARN MAXIMUM COMMISSION

--> SELECT * , SAL*12 AS 'ANNUAL SAL' FROM EMP WHERE COMM IN (SELECT MAX(COMM) FROM EMP );
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+------------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  | ANNUAL SAL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+------------+
| 2102 | FARIYA     | TAJ       | 1999-01-03 | f      | DEVELOPER  | 1601 | 2021-03-01 | 32000.00 | 3600.00 |  113 | NULL |  384000.00 |
| 2103 | PRIYA      | SHETTY    | 1998-03-20 | f      | ACCOUNTANT | 1602 | 2021-05-01 | 32000.00 | 3600.00 |  112 | NULL |  384000.00 |
| 2201 | KIRAN      | RAJ       | 1999-09-21 | M      | ACCOUNTANT | 1602 | 2022-08-28 | 30000.00 | 3600.00 |  112 |  503 |  360000.00 |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+------------+



12) WAQTD THE LAST EMP RECORDS WITH 25% HIKE IN SALARY

-->  SELECT * , (SAL)*(25/100) as '25% HIKE'FROM EMP WHERE DOJ IN(SELECT MAX(DOJ) FROM EMP);
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+-------------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  | 25% HIKE    |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+-------------+
| 2201 | KIRAN      | RAJ       | 1999-09-21 | M      | ACCOUNTANT | 1602 | 2022-08-28 | 30000.00 | 3600.00 |  112 |  503 | 7500.000000 |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+-------------+


13) WAQTD THE EMP INFORMATION WHO IS NOT TAKING COMM AND JOINED COMPANY AFTER JULY 2018

--> SELECT * FROM EMP WHERE COMM IS NULL AND DOJ > '2018-07-01';
+------+------------+-----------+------------+--------+------------+------+------------+----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+------+------+------+
| 1901 | SHIVANI    | RAI       | 1998-11-07 | f      | TESTER     | 1601 | 2019-12-12 | 45000.00 | NULL |  113 |  502 |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 | 50000.00 | NULL |  110 |  505 |
| 1903 | KARAN      | BHAT      | 1997-12-26 | M      | SALESMAN   | 1701 | 2019-12-26 | 45000.00 | NULL |  111 | NULL |
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN   | 1701 | 2021-12-26 | 40000.00 | NULL |  111 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+------+------+------+


14) WAQTD THE FIRST_NAME AND LAST_NAME OF EMP WHO EARN HIGHEST SAL IN THEIR RESPECTIVE JOBS

--> 



15) WAQTD ALL THE EMP WHOSE SAL IS GREATHER THAN AVG SAL OF DNO 113;

-->   SELECT * FROM EMP WHERE SAL > ALL(SELECT AVG(SAL) FROM EMP WHERE DNO=113);
+------+------------+-----------+------------+--------+-----+------+------------+-----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB | MGR  | DOJ        | SAL       | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+-----+------+------------+-----------+------+------+------+
| 1601 | SIDDARTH   | PATIL     | 1985-11-24 | M      | CEO | NULL | 2016-01-16 | 500000.00 | NULL |  113 | NULL |
+------+------------+-----------+------------+--------+-----+------+------------+-----------+------+------+------+


16) WAQTD DETAILS OF SHIVAINI AND EMPLOYEES WORKING AS CEO ALONG WITH HIKE OF 35% IN SALARY 

--> 


17) WAQTD FIRST EMP RECORD BASED ON HIREDATE

--> SELECT * FROM EMP WHERE DOJ IN(SELECT MIN(DOJ) FROM EMP);
+------+------------+-----------+------------+--------+-----+------+------------+-----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB | MGR  | DOJ        | SAL       | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+-----+------+------------+-----------+------+------+------+
| 1601 | SIDDARTH   | PATIL     | 1985-11-24 | M      | CEO | NULL | 2016-01-16 | 500000.00 | NULL |  113 | NULL |
+------+------------+-----------+------------+--------+-----+------+------------+-----------+------+------+------+


18) WAQTD THE DETIALS OF CUSTOMERS WHO ARE FROM VIJAYANAGAR

--> SELECT C1.* FROM CUSTOMER C1 INNER JOIN LOCATION L1 ON C1.LID=L1.LID WHERE L1.LOCATION='VIJAYANAGAR';
+-----+------------+-----------+-----+----------+------------+
| CID | FIRST_NAME | LAST_NAME | LID | ORDER_ID | PRODUCT_ID |
+-----+------------+-----------+-----+----------+------------+
| 502 | SHIVANI    | RAI       |   1 |     NULL |       NULL |
+-----+------------+-----------+-----+----------+------------+



19) WAQTD THE LOCATIONS OF THE DEPARTMENTS USING LOCATION TABLE;

-->  SELECT L1.LOCATION FROM LOCATION L1 INNER JOIN DEPT D1 ON L1.LID = D1.LID;
+-------------+
| LOCATION    |
+-------------+
| VIJAYANAGAR |
| VIJAYANAGAR |
| VIJAYANAGAR |
| HEBBAL      |
| HEBBAL      |
+-------------+


20) WAQTD THE FIRST_NAME OF THE CUSTOMERS WHO ARE FROM MAHARASHTRA BY USING LOCATION TABLE;

-->  SELECT C1.FIRST_NAME FROM CUSTOMER C1 INNER JOIN LOCATION L1 ON C1.LID = L1.LID WHERE L1.STATE = 'MAHARASHTRA';
+------------+
| FIRST_NAME |
+------------+
| SALMAN     |
| SELVA      |
| PATRICK    |
+------------+



21) WAQTD THE DETAILS OF EMP WHO ARE GETTING SAL LESS THAN KARAN BHAT

--> SELECT * FROM EMP WHERE SAL < (SELECT SAL FROM EMP WHERE FIRST_NAME='KARAN' AND LAST_NAME='BHAT');
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| 2002 | DHARANI    | PATIL     | 1998-11-10 | f      | DEVELOPER  | 1601 | 2021-06-20 | 30000.00 | 3000.00 |  113 | NULL |
| 2102 | FARIYA     | TAJ       | 1999-01-03 | f      | DEVELOPER  | 1601 | 2021-03-01 | 32000.00 | 3600.00 |  113 | NULL |
| 2103 | PRIYA      | SHETTY    | 1998-03-20 | f      | ACCOUNTANT | 1602 | 2021-05-01 | 32000.00 | 3600.00 |  112 | NULL |
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN   | 1701 | 2021-12-26 | 40000.00 |    NULL |  111 | NULL |
| 2201 | KIRAN      | RAJ       | 1999-09-21 | M      | ACCOUNTANT | 1602 | 2022-08-28 | 30000.00 | 3600.00 |  112 |  503 |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+


22) WAQTD THE NAME OF EMP WHO DELIVERED THE PRODUCT TO CUSTOMER NAMED SELVA MANI

-->   SELECT E1.* FROM EMP E1 INNER JOIN ORDERS O1 ON E1.EID = O1.EID INNER JOIN CUSTOMER C1 ON O1.ORDER_ID = C1.ORDER_ID WHERE C1.FIRST_NAME='SELVA';
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+


-->  SELECT * FROM EMP WHERE EID IN (SELECT EID FROM ORDERS WHERE ORDER_ID IN (SELECT ORDER_ID FROM CUSTOMER WHERE FIRST_NAME='SELVA' AND LAST_NAME='MANI'
));
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+


23) WAQTD THE PRODUCT DETAILS WHHICH IS BEING DELIVERED BY JHNAVI NAIK

-->  SELECT P1.* FROM PRODUCT P1 INNER JOIN ORDERS O1 ON P1.PRODUCT_ID = O1.PRODUCT_ID INNER JOIN EMP E1 ON E1.EID = O1.EID WHERE FIRST_NAME='JHNAVI' AND LAST_NAME='NAIK';
+------------+--------+---------+
| PRODUCT_ID | PNAME  | PRICE   |
+------------+--------+---------+
|        801 | WALLET | 2000.00 |
|        801 | WALLET | 2000.00 |
+------------+--------+---------+


24*) WAQTD THE DETAILS EMP WHERE THERE SAL ARE MORE THAN ANY OTHER SALESMAN

-->  SELECT * FROM EMP WHERE SAL > ALL(SELECT SAL FROM EMP WHERE JOB='SALESMAN');
+------+------------+-----------+------------+--------+------------+------+------------+-----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL       | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+------+------+------+
| 1601 | SIDDARTH   | PATIL     | 1985-11-24 | M      | CEO        | NULL | 2016-01-16 | 500000.00 | NULL |  113 | NULL |
| 1602 | HEMA       | SHETTY    | 1996-03-20 | F      | HR         | 1601 | 2016-10-20 | 150000.00 | NULL |  112 |  507 |
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER    | 1602 | 2017-04-17 | 100000.00 | NULL |  111 | NULL |
| 1702 | SAMEER     | KHAN      | 1995-04-20 | M      | MANAGER    | 1602 | 2017-07-07 |  90000.00 | NULL |  110 | NULL |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 |  50000.00 | NULL |  110 |  505 |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+------+------+------+


25) WAQTD THE DETAILS OF EMP IF HE IS WORKING IN MYSORE

-->  SELECT E1.* FROM EMP E1 INNER JOIN DEPT D1 ON E1.DNO = D1.DNO INNER JOIN LOCATION L1 ON D1.LID = L1.LID WHERE L1.CITY='MYSORE';
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL       | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+
| 1702 | SAMEER     | KHAN      | 1995-04-20 | M      | MANAGER    | 1602 | 2017-07-07 |  90000.00 |    NULL |  110 | NULL |
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 |  45000.00 | 1000.00 |  110 | NULL |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 |  50000.00 |    NULL |  110 |  505 |
| 2001 | MAURALI    | KRISHNAN  | 1998-06-08 | M      | DISPATCHER | 1702 | 2020-03-15 |  45000.00 | 1000.00 |  110 | NULL |
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER    | 1602 | 2017-04-17 | 100000.00 |    NULL |  111 | NULL |
| 1903 | KARAN      | BHAT      | 1997-12-26 | M      | SALESMAN   | 1701 | 2019-12-26 |  45000.00 |    NULL |  111 | NULL |
| 2101 | RASHMI     | GOWDA     | 1995-10-03 | f      | SALESMAN   | 1701 | 2021-01-02 |  45000.00 | 3000.00 |  111 | NULL |
| 2104 | AMAN       | RAI       | 1998-08-15 | M      | SALESMAN   | 1701 | 2021-12-26 |  40000.00 |    NULL |  111 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+-----------+---------+------+------+


26) WAQTD DETAILS OF EMP IF THERE MANAGER IS SAMEER KHAN 

--> SELECT E1.* FROM EMP E1 JOIN EMP E2 ON E1.MGR=E2.EID WHERE  E2.FIRST_NAME='SAMEER' AND E2.LAST_NAME='KHAN';
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 | 50000.00 |    NULL |  110 |  505 |
| 2001 | MAURALI    | KRISHNAN  | 1998-06-08 | M      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+


27) WAQTD THE LAST_NAME OF THE EMP IF THEY ARE DIRECTLY TO COMPANY CEO;

-->  SELECT LAST_NAME FROM EMP WHERE MGR IN (SELECT EID FROM EMP WHERE JOB='CEO');
+-----------+
| LAST_NAME |
+-----------+
| SHETTY    |
| RAI       |
| PATIL     |
| TAJ       |
+-----------+



28) WAQTD THE DETAILS OF THE EMP WHO ARE REPORTING TO SAMEER

-->  SELECT E1.* FROM EMP E1 INNER JOIN EMP E2 ON E1.MGR = E2.EID WHERE E2.FIRST_NAME='SAMEER';
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB        | MGR  | DOJ        | SAL      | COMM    | DNO  | CID  |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+
| 1801 | JHNAVI     | NAIK      | 1996-04-11 | f      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
| 1902 | ABHIJIT    | GOWDA     | 1997-12-25 | M      | DISPATCHER | 1702 | 2019-02-28 | 50000.00 |    NULL |  110 |  505 |
| 2001 | MAURALI    | KRISHNAN  | 1998-06-08 | M      | DISPATCHER | 1702 | 2020-03-15 | 45000.00 | 1000.00 |  110 | NULL |
+------+------------+-----------+------------+--------+------------+------+------------+----------+---------+------+------+



29) WAQTD THE MANAGER OF THE EMP WHO WORKS IN SALES TEAM

--> SELECT * FROM EMP WHERE EID IN (SELECT MGR FROM EMP WHERE JOB='SALESMAN');
+------+------------+-----------+------------+--------+---------+------+------------+-----------+------+------+------+
| EID  | FIRST_NAME | LAST_NAME | BIRTHDATE  | GENDER | JOB     | MGR  | DOJ        | SAL       | COMM | DNO  | CID  |
+------+------------+-----------+------------+--------+---------+------+------------+-----------+------+------+------+
| 1701 | RAHUL      | MUKARJEE  | 1991-02-19 | M      | MANAGER | 1602 | 2017-04-17 | 100000.00 | NULL |  111 | NULL |
+------+------------+-----------+------------+--------+---------+------+------------+-----------+------+------+------+



30) WAQTD THE EMP FIRST_NAME , LAST_NAME OF EMP WHO DELIVERED THE PRODUCT ON '12-NOV-22'

-->   SELECT FIRST_NAME , LAST_NAME FROM EMP WHERE EID IN (SELECT EID FROM ORDERS WHERE DELIVERY_DATE = '2022-11-12');
+------------+-----------+
| FIRST_NAME | LAST_NAME |
+------------+-----------+
| JHNAVI     | NAIK      |
+------------+-----------+







