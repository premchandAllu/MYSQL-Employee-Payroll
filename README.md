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
### UC-5 Retrieving data of a particular person
```
SELECT SALARY FROM employee_payroll WHERE NAME = 'Bill';
```
#### Checking the list of persons who joined after a particular date
```
SELECT * FROM employee_payroll WHERE start BETWEEN CAST('2019-01-01' AS DATE) AND DATE(NOW());
```
### UC-6 Adding Column To Employee Payroll Table
```
ALTER TABLE employee_payroll ADD GENDER CHAR(1) After NAME;
```
#### Added Query to Set Gender
```
UPDATE employee_payroll SET GENDER= F WHERE NAME='Terisa';
UPDATE employee_payroll SET GENDER = M WHERE NAME='Bill' Or NAME='Charlie';
```
#### Show the Table
``` SELECT * FROM employee_payroll;```

### UC-7 Ability to Find Sum,Avg,Max,Min,Count of employee_payroll
#### Total Salary According to Gender
```SELECT GENDER,SUM(SALARY) From employee_payroll GROUP BY GENDER;```
#### Average Salary for Each Gender
```SELECT GENDER,AVG(SALARY) From employee_payroll GROUP BY GENDER;```
#### Maximum Salary for each Gender
```SELECT GENDER,MIN(SALARY) From employee_payroll GROUP BY GENDER;```
#### Minimum Salary for each Gender
`SELECT GENDER,MIN(SALARY) From employee_payroll GROUP BY GENDER;`
#### Count Of Persons in each Gender
`SELECT GENDER,COUNT(SALARY) From employee_payroll GROUP BY GENDER;`

### UC-8 Ability to Extend employee_payroll to Store Phone No,Address,Department
#### Add Column Phone No after NAME
``` ALTER TABLE employee_payroll ADD PHONE_NUMBER VARCHAR(250) AFTER NAME;```
#### Add Column Address After Phone No
```ALTER TABLE employee_payroll ADD ADDRESS VARCHAR(250) AFTER PHONE_NUMBER;```
#### Add Column Department After Address
``` ALTER TABLE employee_payroll ADD DEPARTMENT VARCHAR(250) NOT NULL AFTER ADDRESS;```
#### Set Default Address to TBD
``` UPDATE employee_payroll SET ADDRESS ='TBD';```

#### View Table
``` SELECT * FROM employee_payroll;```

### UC-9 Ability to extend employee_payroll to store Basic Pay,Deductions,Taxable Pay,Income Tax,Net Pay

#### Changing salary column name to basic_pay
```ALTER TABLE employee_payroll RENAME COLUMN SALARY TO BASIC_PAY;```

#### Adding deductions after basic_pay
```ALTER TABLE employee_payroll ADD DEDUCTIONS DOUBLE NOT NULL AFTER BASIC_PAY;```

#### Adding taxable_pay after deductions
```ALTER TABLE employee_payroll ADD TAXABLE_PAY DOUBLE NOT NULL AFTER DEDUCTIONS;```

#### Adding tax after taxable_pay
```ALTER TABLE employee_payroll ADD TAX DOUBLE NOT NULL AFTER TAXABLE_PAY;```

#### Adding net_pay after tax
```ALTER TABLE employee_payroll ADD NET_PAY Double NOT NULL AFTER TAX;```
