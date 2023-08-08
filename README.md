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

**select** * from **user_management**;

**select** * from **job_titles**;

**select** * from **pay_grades**;

**select** * from **employment_type**;

**select** * from **seniority_level**;

**select** * from **work_shift**;

**select** * from **work_shift_employees**;
