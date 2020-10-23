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
