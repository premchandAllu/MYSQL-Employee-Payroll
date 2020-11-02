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

### UC-10 Ability to Add Teresa to Sales And Marketing Department
```
UPDATE employee_payroll SET DEPARTMENT='Sales' where NAME='Terisa';
INSERT into employee_payroll (NAME,DEPARTMENT,GENDER,BASIC_PAY,DEDUCTIONS,TAXABLE_PAY,TAX,NET_PAY,START)
VALUES('Terisa', 'Marketing', 'F', 200000, 50000, 150000, 50000, 100000, '2018-01-03');
```
### UC11 - Implement the ER Diagram into Payroll Service DataBase

#### Create Company Table
```CREATE TABLE company
    -> (
    -> company_id      INT NOT NULL PRIMARY KEY,
    -> company_name    VARCHAR(150) NOT NULL
    -> );
```
#### Create Table Employee Details
```CREATE TABLE employee_details
    -> (
    -> employee_id     INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    -> company_id      INT NOT NULL,
    -> FOREIGN KEY     (company_id) REFERENCES company (company_id),
    -> name            VARCHAR(150) NOT NULL,
    -> phone_number    BIGINT(15) NOT NULL,
    -> address         VARCHAR(250) NOT NULL,
    -> gender          CHAR(1) NOT NULL,
    -> start_date      DATE NOT NULL
    -> );
```
#### Create Table Payroll
```CREATE TABLE payroll
    -> (
    -> employee_id     INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    -> FOREIGN KEY     (employee_id) REFERENCES employee (employee_id),
    -> basic_pay       DOUBLE NOT NULL,
    -> deductions      DOUBLE NOT NULL,
    -> taxable_pay     DOUBLE NOT NULL,
    -> tax             DOUBLE NOT NULL,
    -> net_pay         DOUBLE NOT NULL
    -> );
```
#### Create Table Department
```CREATE TABLE department
    -> (
    -> department_id   INT NOT NULL PRIMARY KEY,
    -> department_name VARCHAR(150) NOT NULL
    -> );
```
#### Create Table Employee Department
```CREATE TABLE employee_department
    -> (
    -> employee_id     INT UNSIGNED NOT NULL AUTO_INCREMENT,
    -> FOREIGN KEY     (employee_id) REFERENCES employee (employee_id),
    -> department_id   INT NOT NULL,
    -> FOREIGN KEY     (department_id) REFERENCES department (department_id)
    -> );
```
### Inserting values into the tables created
#### Insert into Company Table
```INSERT INTO company VALUES
    -> (1,'Google'),
    -> (2,'Microsoft'),
    -> (3,'Capgemini');
```
#### Insert into Employee Table
```INSERT INTO employee VALUES
    -> (101, 1, 'Bill', '9494118273', 'Hyderabad', 'M', '2018-01-01'),
    -> (102, 2, 'Terisa', '7207020464', 'Nizamabad', 'F', '2019-11-11'),
    -> (103, 3, 'Charlie', '9440293758', 'Chennai', 'M', '2020-05-21');
```
#### Insert into Payroll Table
```INSERT INTO payroll VALUES
    -> ('101', 4000000.00, 1000000.00, 3000000.00, 500000.00, 2500000.00),
    -> ('102', 5000000.00, 1500000.00, 3500000.00, 1000000.00, 2500000.00),
    -> ('103', 6000000.00, 2000000.00, 4000000.00, 1500000.00, 2500000.00);
```
#### Insert into Department Table
```INSERT INTO department VALUES
    -> (110,'Sales'),
    -> (111,'Marketing'),
    -> (112,'Finance');
```
#### Insert into employee Department Table
```INSERT INTO employee_department VALUES
    -> (101,110),
    -> (102,111),
    -> (103,112),
    -> (102,110);
```
### UC12 - Ability to ensure all retrieve queries done are working with new table structure
```SELECT * FROM company;
SELECT * FROM employee_details;
SELECT * FROM payroll;
SELECT * FROM department;
SELECT * FROM employee_department;
SELECT salary FROM payroll WHERE name = 'Bill';
SELECT * FROM payroll WHERE start BETWEEN CAST('2018-01-01' AS DATE) and DATE(NOW());
SELECT SUM(p.net_pay), e.gender FROM employee e LEFT JOIN payroll p ON p.employee_id = e.employee_id GROUP BY e.gender;
SELECT AVG(p.net_pay), e.gender FROM employee e LEFT JOIN payroll p ON p.employee_id = e.employee_id GROUP BY e.gender;
SELECT MIN(p.net_pay), e.gender FROM employee e LEFT JOIN payroll p ON p.employee_id = e.employee_id GROUP BY e.gender;
SELECT MAX(p.net_pay), e.gender FROM employee e LEFT JOIN payroll p ON p.employee_id = e.employee_id GROUP BY e.gender;
SELECT COUNT(p.net_pay), e.gender FROM employee e LEFT JOIN payroll p ON p.employee_id = e.employee_id GROUP BY e.gender;
```
