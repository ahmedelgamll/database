``` sql
--- Display (Using Union Function)
 --- The name and the gender of the dependence that's
 --- gender is Female and depending on Female Employee.
 --- And the male dependence that depends on Male Employee.
 select Dependent_name ,d.Sex
 from Dependent d inner join Employee e
 on e.SSN=d.ESSN and d.sex ='f' and e.Sex='f'
 union all
 select Dependent_name ,d.Sex
 from Dependent d,Employee e
 where e.SSN=d.Essn and d.sex ='m' and e.Sex='m'



 --- For each project, list the project name and the total hours per week (for all employees) spent on that project
select sum(hours) as [total hours],Pname 
from Project,Works_for
where Pnumber=Pno
group by pname



-- Display the data of the department which has the smallest employee ID over all employees' ID.
select d.*
from Departments d inner join Employee  e
on d.dnum = e.Dno
where e.ssn in (SELECT MIN(SSN) FROM employee)
    


--- For each department, retrieve the department name and the maximum, minimum and average salary of its employees
select Dname,max(salary) as [maximum salary],min(salary) as [minimum salary ],Dnum
from Departments d ,Employee e
where d.Dnum=e.Dno
group by d.Dnum,Dname



--- List the last name of all managers who have no dependents.
select e.Lname
from Employee e , Departments d
where e.SSN=d.MGRSSN and e.ssn not in( select ESSN from Dependent)



---For each department-- if its average salary is less than the average salary of all employees-- display its number, name and number of its employees.
select Dno , Dname,count(ssn)
from Departments d inner join Employee e
on d.Dnum=e.Dno
group by Dno , Dname
having avg (e.salary)<(select avg (salary) from Employee)





--- Retrieve a list of employees and the projects they are working on ordered by department and within each department, ordered alphabetically by last name, first name.
select CONCAT (Fname,' ',Lname) as [full name],p.Pname
from Employee e,Project p,Works_for w
where e.SSN=w.ESSn and p.Pnumber=w.Pno
order by Dnum,Lname,Fname asc



---Try to get the max 2 salaries using subquery
select salary
from employee
where Salary in (Select distinct top 2 salary  from Employee order by Salary Desc)
order by salary desc



--- Get the full name of employees that is similar to any dependent name
select CONCAT (Fname,' ',Lname) as [full name]
from employee 
where Fname in (select Dependent_name from Dependent)



--- Try to update all salaries of employees who work in Project ‘Al Rabwah’ by 30% 
update Employee
set Salary+=0.3*Salary
where ssn in (select ssn 
from Employee e,Project p,Works_for w
where e.SSN=w.ESSn and p.Pnumber=w.Pno and p.Pname='Al Rabwah'
)



--- Display the employee number and name if at least one of them have dependents (use exists keyword) self-study
select ssn, CONCAT (Fname,' ',Lname) as [full name]
from employee
where exists (
select 1 
from Dependent d
where ssn=ESSN
)

___
--- In the department table insert new department called "DEPT IT" , with id 100, employee with SSN = 112233 as a manager for this department. The start date for this manager is '1-11-2006'
insert into Departments 
values('DEPT IT',100,112233,1-11-2006)



---Do what is required if you know that : Mrs.Noha Mohamed(SSN=968574)  moved to be the manager of the new department (id = 100), and they give you(your SSN =102672) her position (Dept. 20 manager) 
---First try to update her record in the department table
delete from Employee
where SSN='968574'

insert into Departments 
values('DEPT IT',100,102672,getdate())

--- update your record to be department 20 manager.
update  Employee
set Dno=20
where SSN=102672

--- Update the data of employee number=102660 to be in your teamwork (he will be supervised by you) (your SSN =102672)
update  Employee
set Superssn=102672
where SSN=102660



--- Unfortunately the company ended the contract with Mr. Kamel Mohamed (SSN=223344) so try to delete his data from your database in case you know that you will be temporarily in his position.
Hint: (Check if Mr. Kamel has dependents, works as a department manager, supervises any employees or works in any projects and handle these cases).

delete from Dependent 
where ESSN=223344

delete from Departments
where MGRSSN=223344

delete from Employee
where Superssn=223344


delete from Employee
where SSN=223344
```