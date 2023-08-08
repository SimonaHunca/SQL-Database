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

desc **user_permissions**;

desc **job_titles**;

desc **pay_grades**;

desc **seniority_level**;

desc **work_shift**;

desc **employment_type**;

desc **work_shift_employees**;

 ## -- DDL -- Modificare tipului unei coloane

alter table **user_permissions** modify **role_employee** varchar(20);

alter table **job_titles** modify **job_description** varchar(50) null;

alter table **employment_type** modify **employment_type** varchar(30);

alter table **seniority_level** modify **seniority_level_name** varchar(20);
