## part 1:
``` sql
--- Display the Department id, name and id and the name of its manager.
select dnum,Dname,MGRSSN,CONCAT(Fname,' ',lname) as [full name]
from Departments ,Employee 
where ssn=MGRSSN



--Display the name of the departments and the name of the projects under its control.
select Dname,Pname
from Departments d,Project p
where d.Dnum=p.Dnum


--- Display the full data about all the dependence associated with the name of the employee they depend on him/her
select d.* ,Fname
from Dependent d, employee e
where ssn =essn 


--- Display the Id, name and location of the projects in Cairo or Alex city.
select Pnumber,Pname,Plocation
from Project
where city in ('cairo','alex')



--- Display the Projects full data of the projects with a name starts with "a" letter.
select *
from Project
where Pname like 'a%'



--- display all the employees in department 30 whose salary from 1000 to 2000 LE monthly
select CONCAT(Fname,' ',Lname) as [full name]
from employee
where Dno=30 and( Salary>=1000 and salary <=2000)


--- Retrieve the names of all employees in department 10 who works more than or equal10 hours per week on "AL Rabwah" project.
select CONCAT(Fname,' ',Lname) as [full name]
from employee e ,Works_for w,Project p
where Dno=10 and ssn =essn and Pnumber=Pno and hours >=10 and Pname='AL Rabwah'



--- Find the names of the employees who directly supervised with Kamel Mohamed.
select  CONCAT(x.Fname,' ',x.Lname) as [full name]
from Employee x , employee y
where y.SSN=x.Superssn and CONCAT(y.Fname,' ',y.Lname)='Kamel Mohamed'



--- Retrieve the names of all employees and the names of the projects they are working on, sorted by the project name.
select CONCAT(Fname,' ',Lname) as [full name],Pname
from Employee e,Project p, Works_for w
where e.ssn=w.essn and p.Pnumber=w.Pno 
order by 2



--- For each project located in Cairo City , find the project number, the controlling department name ,the department manager last name ,address and birthdate.
select Pnumber,Dname,e.Lname,e.Address,e.Bdate
from Project p,Departments d,Employee e
where d.Dnum=p.Dnum and e.SSN=d.MGRSSN and City='cairo'



--- Display All Data of the mangers
select e.*
from employee e,Departments d
where e.SSN= d.MGRSSN



--- Display All Employees data and the data of their dependents even if they have no dependents
select e.* , d.*
from employee e left outer join Dependent d
on  e.SSN=d.ESSN


___

--- DML
--- Insert your personal data to the employee table as a new employee in department number 30, SSN = 102672, Superssn = 112233, salary=3000.
insert into Employee
values('ahmed','emad',102672,1/9/2003,'hai shark-mansoura','M',3000,112233,30)



--- Insert another employee with personal data your friend as new employee in department number 30, SSN = 102660, but don’t enter any value for salary or manager number to him.
insert into Employee(Fname,Lname,ssn,Bdate,Address,sex,Dno)
values('ali','eyad',102660,1/6/2003,'hai shark-mansoura','M',30)



--- Upgrade your salary by 20 % of its last value.
update Employee
set Salary+=0.2*Salary
where SSN=102672

___
## part 2:
1 nf:
order(`item`,`customer n` order,deescription , quantity, unitprice,total)
basics(`customer n`,customer name,customer ad,son,sod,clerk num,clerrk name)


2 nf:



```