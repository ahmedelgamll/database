``` sql
--- Display all the employees Data
select * 
from employee


--- Display the employee First name, last name, Salary and Department number.
select Fname,Lname,salary,dno
from employee


--- Display all the projects names, locations and the department which is responsible about it.
select Pname,Plocation,Dname
from Project p,Departments d
where d.Dnum=p.Dnum



--- If you know that the company policy is to pay an annual commission for each employee with specific percent equals 10% of his/her annual salary .Display each employee full name and his annual commission in an ANNUAL COMM column (alias).
select fname+' '+Lname as fullname,Salary*12*0.1 as ANNUALCOMM
from employee


--- Display the employees Id, name who earns more than 1000 LE monthly.
select ssn,Fname
from employee
where Salary>=1000


--- Display the employees Id, name who earns more than 10000 LE annually
select ssn,Fname
from employee
where Salary*12>=10000


--- Display the names and salaries of the female employees 
select Fname,Salary
from employee
where sex='f'


--- Display each department id, name which managed by a manager with id equals 968574.
select Dnum,Dname 
from departments
where MGRSSN=968574


--- Dispaly the ids, names and locations of  the pojects which controled with department 10.
select Pnumber,Pname,Plocation
from Project
where Dnum=10

```