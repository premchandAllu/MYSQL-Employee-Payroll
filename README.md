## MYSQL-Employee-Payroll
### UC-1 Create DataBase Payroll_Service
```
CREATE DATABASE payroll_service
```
#### See the created DataBase
```
show databases;
```
#### Use the DataBase
```
use payroll_service;
```
### UC-2 Create Table employee_payroll
```
 CREATE TABLE employee_payroll 
 ->( 
 ->  ID      int unsigned  NOT NULL AUTO_INCREMENT,
 ->  NAME    varchar(150)  NOT NULL, 
 ->  SALARY  double        NOT NULL,
 ->  START   DATE          NOT NULL, 
 ->  Primary Key(ID));
```
#### See the Table
```
DESRIBE employee_payroll;
```
### UC-3 Insert Data into Table
```
INSERT INTO employee_payroll(name , salary , start) VALUES
    -> ( 'Bill',1000000.00,'2018-01-03'),
    -> ( 'Terisa',2000000.00,'2019-11-13'),
    -> ('Charlie',3000000.00,'2020-05-21');
 ```
 ### UC-4 Retrieving Data
 ```
 SELECT * FROM employee_payroll;
 ```
 
