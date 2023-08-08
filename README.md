# SQL-Database OrangeHRM
## DDL ( Data Definition Language )-- Creaza baza de date
 create database OrangeHRM;

## Stergere baze de date 
#drop database OrangeHRM;

## DDL ( Data Definition Language ) -- Creaza tabele 

### create table user_permissions 
(**id** int not null auto_increment primary key,

**role_employee** varchar(15) not null,

**id_paygrade** int not null
);
### create table Job_titles 
( **job_id** int not null auto_increment primary key,

  **job_name** varchar(15) not null,
  
  **job_description** varchar(50) not null
);

### create table user_management
(**id** int not null auto_increment primary key,

**username** varchar(25) not null,

**employee_name** varchar(25) not null,

**id_role_employee** int,

**id_status** bool,

**job_id** int,

foreign key (**id_role_employee**) references user_permissions(**id**),

foreign key(**job_id**) references job_titles(**job_id**)
);

### create table pay_grades
(
**id_paygrade** int not null auto_increment primary key,

**currency** varchar(5) not null,

**minimum_salary** int not null,

**maximum_salary** int not null
);
### create table employment_type
(
**id** int not null auto_increment primary key,

**job_id** int not null,

**employment_type** varchar(20) not null,

foreign key (**job_id**) references job_titles(**job_id**)
);

### create table seniority_level
(
**id** int not null auto_increment primary key,

**seniority_level_name** varchar(15),

**job_id** int,

foreign key (**job_id**) references job_titles(**job_id**) # Crearea unei chei straine 
);
### create table work_shift
(
**id** int not null auto_increment primary key,

**shift_name** varchar(20) not null,

**start_time** time not null,

**end_time** time not null
);
### create table work_shift_employees
( 
**id_shift** int not null,

**id_employee** int not null,

**start_date** date not null,

**end_date** date not null,

foreign key (**id_shift**) references work_shift(**id**),

foreign key (**id_employee**) references user_management(**id**)
);

## -- Adaugarea unei chei straine
alter table **user_permissions** add foreign key (**id_paygrade**) references pay_grades(**id_paygrade**);

## -- Descrie structura unui tabel
desc **user_management**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(31).png)

desc **user_permissions**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(32).png)

desc **job_titles**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(33).png)

desc **pay_grades**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(34).png)

desc **seniority_level**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(35).png)

desc **work_shift**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(36).png)

desc **employment_type**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(37).png)

desc **work_shift_employees**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(38).png)

 ## -- DDL -- Modificare tipului unei coloane

alter table **user_permissions** modify **role_employee** varchar(20);

alter table **job_titles** modify **job_description** varchar(50) null;

alter table **employment_type** modify **employment_type** varchar(30);

alter table **seniority_level** modify **seniority_level_name** varchar(20);

## DML ( Data Manipulation Language ) -- Inserare valori in tabele 

**insert** into **pay_grades** (currency,minimum_salary,maximum_salary) values

('EURO',2450,3600),

('USD',3460,5679),

('EURO',1687,2876),

('RON',3689,6365),

('HUF',1365,3456),

('USD',1897,4590),

('RON',5437,7854),

('HUF',2564,3500);

**insert** into **user_permissions**(role_employee,id_paygrade) values

('Admin',2),

('Admin',4),

('Admin',7),

('ESS_Employee',1),

('ESS_Employee',8),

('ESS_Supervisor',3),

('ESS_Supervisor',6);

**insert** into **user_permissions**(role_employee,id_paygrade) values

('ESS_Employee',5);


**insert** into **user_management**(username,employee_name,id_role_employee,id_status,job_id) values

('John01','John Trueman',2,true,6),

('Julia42','Julia Anderson',4,true,1),

('Peter21','Peter Selling',8,false,2),

('Patrick02','Patrick Sharp',1,true,4),

('Herman09','Herman Fittermann',3,false,5),

('Mary05','Mary Jackson',6,true,3),

('Silvy21','Silvia Redwoman',7,true,2),

("Patrick08","Patrick Sharp",5,true,5),

("Peter30","Peter Selling",4,true,1);

**insert** into **job_titles** (job_name,job_description) values

('Manager',null),

('Supervisor','Tracking employees'),

('Dispatcher','Answering phone'),

('Dispatcher', null),

('Manager','Create documentation'),

('Supervisor',null);

**insert** into **employment_type**(job_id,employment_type) values

(2,'full time contract'),

(4, 'part-time contract'),

(6, 'internship contract'),

(1, 'full-time contract'),

(3,'internship contract'),

(5, 'part-time contract'),

(6,'internship contract'),

(1,'full-time contract'),

(3, 'part-time contract');

**insert** into **seniority_level**(seniority_level_name,job_id) values

('Official and Manager',1),

('Service Worker',3),

('Professional',2),

('Official and Manager',5),

('Service Worker',4),

('Professional',6);

**insert** into **work_shift**(shift_name,start_time,end_time) values

('Night Shift','22:00','7:00'),

('Morning Shift','7:00','16:00'),

('Afternoon Shift','14:00','22:00');

**insert** into **work_shift_employees**(id_shift,id_employee,start_date,end_date) values

(1,21,'2023-01-10','2023-04-10'),

(2,25,'2023-04-11','2023-08-11'),

(3,19,'2023-08-12','2023-12-12'),

(1,27,'2023-01-10','2023-04-10'),

(2,20,'2023-04-11','2023-08-11'),

(3,23,'2023-08-12','2023-12-12'),

(1,22,'2023-01-10','2023-04-10'),

(2,26,'2023-04-11','2023-08-11'),

(3,24,'2023-08-12','2023-12-12');

## DQL ( Data Query Language ) -- Afisarea tabelului

**select** * from **user_permissions**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(39).png)

**select** * from **user_management**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(40).png)

**select** * from **job_titles**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(43).png)

**select** * from **pay_grades**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(44).png)

**select** * from **employment_type**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(45).png)

**select** * from **seniority_level**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(46).png)

**select** * from **work_shift**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(47).png)

**select** * from **work_shift_employees**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(48).png)

## DML -- Stergerea tuturor datelor din tabela

#delete from user_management;

#truncate table user_management; 

#truncate table job_titles;

## DQL (DATA QUERY LANGUAGE) 

## -- Afisarea unei sau mai multor coloane

**select** username , id_role_employee from user_management;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(49).png)


**select** employee_name from user_management;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(50).png)


## -- Selectarea angajatilor care au status disabled 

**select** * from **user_management** where **id_status** = false;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(51).png)

## -- Selectarea angajatilor care au status enabled

**select** * from **user_management** where **id_status** = true;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(52).png)

## -- Selectarea angajatilor care au acelasi rol

**select** user_management.employee_name,user_permissions.role_employee
from **user_management** inner join **user_permissions**
on user_management.id_role_employee = user_permissions.id
where **role_employee = 'Admin'**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(54).png)

**select** user_management.employee_name,user_permissions.role_employee
from **user_management** inner join **user_permissions**
on user_management.id_role_employee = user_permissions.id
where **role_employee = 'ESS_Employee'**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(55).png)

**select** user_management.employee_name,user_permissions.role_employee
from **user_management** inner join **user_permissions**
on user_management.id_role_employee = user_permissions.id
where **role_employee = 'ESS_Supervisor'**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(56).png)

## -- Selectare angajatilor cu numele Patrick Sharp si Peter Selling

**select** * from **user_management** where **employee_name in ("Patrick Sharp")**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(57).png)

**select** * from **user_management** where **employee_name in ("Peter Selling")**;

![RESULTS](https://github.com/SimonaHunca/SQL-Database/blob/main/Screenshot%20(58).png)

## -- Selectarea id-ului/numelui angajatilor care nu au introdus nicio data in Job description
select job_titles.job_description,user_management.employee_name 
from job_titles inner join user_management
on job_titles.job_id=user_management.job_id
where job_description is null;

-- Selectarea id-ului/numelui angajatilor care au introdus date in Job description
select * from job_titles where job_description is not null;
select job_titles.job_description,user_management.employee_name 
from job_titles inner join user_management
on job_titles.job_id=user_management.job_id
where job_description is not null;

-- Filtreaza angajatii in functie de moneda salariului
select user_management.employee_name,user_permissions.id_paygrade,pay_grades.currency
from user_management inner join user_permissions inner join pay_grades
on user_management.id_role_employee = user_permissions.id and user_permissions.id_paygrade = pay_grades.id_paygrade
where currency = 'EURO';

select user_management.employee_name,user_permissions.id_paygrade,pay_grades.currency
from user_management inner join user_permissions inner join pay_grades
on user_management.id_role_employee = user_permissions.id and user_permissions.id_paygrade = pay_grades.id_paygrade
where currency = 'RON';

select user_management.employee_name,user_permissions.id_paygrade,pay_grades.currency
from user_management inner join user_permissions inner join pay_grades
on user_management.id_role_employee = user_permissions.id and user_permissions.id_paygrade = pay_grades.id_paygrade
where currency = 'USD';

select user_management.employee_name,user_permissions.id_paygrade,pay_grades.currency
from user_management inner join user_permissions inner join pay_grades
on user_management.id_role_employee = user_permissions.id and user_permissions.id_paygrade = pay_grades.id_paygrade
where currency = 'HUF';

-- filtreaza angajatii cu salariul maxim sub 4000 euro
select pay_grades.maximum_salary,pay_grades.currency,user_management.employee_name,user_permissions.id_paygrade
from pay_grades inner join user_management inner join user_permissions
on user_permissions.id_paygrade = pay_grades.id_paygrade and user_management.id_role_employee = user_permissions.id
where maximum_salary<4000 and currency ='Euro';

-- filtreaza angajatii cu salariul minim mai mare sau egal cu 2000 Ron
select pay_grades.minimum_salary,user_management.employee_name,user_permissions.id_paygrade
from pay_grades inner join user_management inner join user_permissions
on user_management.id_role_employee = user_permissions.id and user_permissions.id_paygrade = pay_grades.id_paygrade
where maximum_salary >=2000 and currency ='RON';

-- filtreaza angajatii in functie de contractele lor
select employment_type.employment_type,user_management.employee_name,job_titles.job_id
from employment_type inner join user_management inner join job_titles
on user_management.job_id = job_titles.job_id and employment_type.job_id = job_titles.job_id
where employment_type in ('full-time contract');
select employment_type.employment_type,user_management.employee_name
from employment_type inner join user_management 
on employment_type.job_id = user_management.job_id 
where employment_type in ('part-time contract');
SELECT employment_type.employment_type,user_management.employee_name
FROM employment_type INNER JOIN user_management ON employment_type.job_id = user_management.job_id
WHERE employment_type IN ('internship contract');


-- filtreaza angajatii activi cu salariul maxim mai mic de 5000 euro functia de supervisor si contract full-time
select user_management.employee_name,job_titles.job_name,employment_type.employment_type,pay_grades.currency,pay_grades.maximum_salary,user_permissions.id_paygrade
from user_management inner join job_titles inner join employment_type inner join pay_grades inner join user_permissions
on user_management.job_id = job_titles.job_id and employment_type.job_id = job_titles.job_id  and user_permissions.id_paygrade = pay_grades.id_paygrade 
where maximum_salary<5000 and job_name in ('Supervisor') and employment_type in ('part-time contract');

-- filtreaza angajatii cu functia de dispatcher si contract internship
select job_titles.job_name,employment_type.employment_type
from job_titles inner join employment_type
on job_titles.job_id = employment_type.job_id
where job_name in ('Dispatcher') and employment_type in ('internship contract');

-- afiseaza angajatii cu functiile si contractele lor
select user_management.employee_name,job_titles.job_name,employment_type.employment_type
from job_titles inner join employment_type inner join user_management
on job_titles.job_id=employment_type.job_id and job_titles.job_id = user_management.job_id;

-- filtreaza angajatii activi cu salariul maxim de 3000 euro
select pay_grades.maximum_salary, pay_grades.currency,status.status_employee,user_management.employee_name
from pay_grades inner join status inner join user_management
where status_employee = true and maximum_salary > 3000 and currency='EURO';

-- afiseaza angajatii si turele corespondente
select user_management.employee_name, work_shift.shift_name, work_shift_employees.id_employee
from work_shift inner join user_management inner join work_shift_employees
on user_management.id=work_shift_employees.id_employee and work_shift_employees.id_shift = work_shift.id;

-- afiseaza angajatii cu categoria de munca
select user_management.employee_name,seniority_level.seniority_level_name,job_titles.job_id
from user_management inner join seniority_level inner join job_titles
on user_management.job_id = job_titles.job_id and seniority_level.job_id = job_titles.job_id;

 -- afiseaza angajatii cu tura de dimineata si afiseaza si orele de lucru si perioada in care va lucra in aceasta tura
select user_management.employee_name,work_shift.shift_name,work_shift.start_time,work_shift.end_time,work_shift_employees.start_date,work_shift_employees.end_date
from user_management inner join work_shift inner join work_shift_employees
on user_management.id = work_shift_employees.id_employee and work_shift_employees.id_shift = work_shift.id
where shift_name = 'Morning Shift';

-- afiseaza angajatii cu tura de dupa amiaza si afiseaza si orele de lucru si perioada in care va lucra in aceasta tura
select user_management.employee_name,work_shift.shift_name,work_shift.start_time,work_shift.end_time,work_shift_employees.start_date,work_shift_employees.end_date
from user_management inner join work_shift inner join work_shift_employees
on user_management.id = work_shift_employees.id_employee and work_shift_employees.id_shift = work_shift.id
where shift_name = 'Afternoon Shift';

-- afiseaza angajatii cu tura de noapte si afiseaza si orele de lucru si perioada in care va lucra in aceasta tura
select user_management.employee_name,work_shift.shift_name,work_shift.start_time,work_shift.end_time,work_shift_employees.start_date,work_shift_employees.end_date
from user_management inner join work_shift inner join work_shift_employees
on user_management.id = work_shift_employees.id_employee and work_shift_employees.id_shift = work_shift.id
where shift_name = 'Night Shift';

-- afiseaza angajatii cu turele lor plus orele de lucru si perioada in care va lucra in aceasta tura
select user_management.employee_name,work_shift.shift_name,work_shift.start_time,work_shift.end_time,work_shift_employees.start_date,work_shift_employees.end_date
from user_management inner join work_shift inner join work_shift_employees
on user_management.id = work_shift_employees.id_employee and work_shift_employees.id_shift = work_shift.id;

