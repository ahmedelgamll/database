``` sql
create rule r1 as @x in('NY','DS','KW')
create default d1 as 'ny'
sp_addtype loc,'nchar(2)'

sp_bindrule r1, loc
sp_bindefault d1, loc
--- table department
create table department
(
DeptNo nchar(2) primary key ,
DeptName varchar(20),
loction loc
)
--- data in department
insert into department
 values('d1' , 'Research' , 'NY')
insert into Department	
values('d2' , 'Accounting' , 'DS')
insert into Department	
values('d3' , 'Markiting' , 'KW')

--- employee
create table employee
(
EmpNo int primary key,
Fname  varchar(20)  not null,
Lname varchar(20)  not null,
Dept_No nchar(2),
Salary money unique,
constraint c1 foreign key (Dept_No) references department(DeptNo)
)
create rule r2 as @x<6000
sp_bindrule r2, 'employee.salary'


--- data in employee
insert into employee
values(25348,'Mathew','Smith','d3',2500)
insert into employee
values(10102,'Ann','Jones','d3',3000)

--- project
create table project(
ProjectNo varchar(2) primary key,
ProjectName varchar(20) not null,
Budget money 
)
--- data in project
insert into project
values('p1','Apollo',120000)
insert into project
values('p2','Gemini',95000)
insert into project
values('p3','Mercury',185600)

---table works on
create table works_on 
(
EmpNo int not null,
ProjectNo varchar(2) not null,
Job varchar(10),
Enter_Date date not null default getdate(),
constraint b1 primary key (EmpNo,ProjectNo)
)


--- data in workson
insert into works_on
values(10102,'p1','Analyst','2006.10.1')

insert into works_on
values(10102,'p3','Manager','2012.1.1')

insert into works_on
values(25348,'p2','Clerk','2007.2.15')




insert into works_on
values(11111,'','','')
--- can't be added




update works_on 
set EmpNo=11111
where EmpNo=10102

--- can't be updated because this column is not matches in the parent table 




update employee  
set EmpNo=22222
where EmpNo=10102
--- can't be updated because on update not cascade , has a child





delete employee 
where EmpNo=10102 
--- can't be deleted because on delete not cascade , has a child





alter table employee add TelephoneNumber varchar(18)
alter table employee drop column TelephoneNumber 



------------------------------------------------------
create schema company
alter schema company transfer Department
alter schema company transfer Project  



create schema hr
alter schema hr transfer Employee 


---Create Synonym for table Employee as Emp and then run the following queries and describe the results
create Synonym Emp
for hr.Employee

---Select * from Employee
select *
from employee
---xxxxx

---Select * from [Human Resource].Employee
select *
from hr.employee

---Select * from Emp
select *
from emp

---Select * from [Human Resource].Emp
select *
from hr.emp    
--xxxxxxxxx



--- Increase the budget of the project where the manager number is 10102 by 10%.
update company.project
set Budget=1.1*Budget
from company.project p ,works_on w
where p.ProjectNo=w.ProjectNo and Job='Manager'and EmpNo=10102


insert into hr.employee
values(29346,'James','James','d2',2800)


--- Change the name of the department for which the employee named James works.The new department name is Sales.
update company.department
 set DeptName='Sales'
from company.department d,hr.employee e
where d.DeptNo =e.Dept_No and e.Fname='James'



--- Change the enter date for the projects for those employees who work in project p1 and belong to department ‘Sales’. The new date is 12.12.2007.
update works_on
    set Enter_Date='12.12.2007'
 from works_on w, company.department d,hr.employee e
 where d.DeptNo=e.Dept_No and e.EmpNo=w.EmpNo and ProjectNo='p1' and d.DeptName='sales'


--- Delete the information in the works_on table for all employees who work for the department located in KW.
delete 
 from works_on w , company.department d     ,  hr.employee e
where d.DeptNo=e.Dept_No and e.EmpNo=w.EmpNo and d.loction='kw'
--- something is wrong
__________________________________________________________________
```