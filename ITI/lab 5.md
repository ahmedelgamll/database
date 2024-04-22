``` sql 
--- Retrieve number of students who have a value in their age. 
select count (St_Id)
from Student
where St_Age is not null



--- Get all instructors Names without repetition
select distinct Ins_Name
from Instructor



--- Display student with the following Format (use isNull function)
Student ID
Student Full Name
Department name



--- Display student with the following Format (use isNull function)
Student ID
Student Full Name
Department name



Display student with the following Format (use isNull function)
Student ID
Student Full Name
Department name

Display student with the following Format (use isNull function)
Student ID
Student Full Name
Department name


--- Display student with the following Format (use isNull function)
select St_Id, isnull (St_Fname+' '+St_Lname,'no name')as [full name],Dept_Name
from Student s,Department d
where d.Dept_Id=s.Dept_Id


--- Display instructor Name and Department Name 
--- Note: display all the instructors if they are attached to a department or not
select Ins_Name,Dept_Name
from Instructor i left outer join Department d
on d.Dept_Id=i.Dept_Id



--- Display student full name and the name of the course he is taking
--- For only courses which have a grade
select St_Fname+' '+ St_Lname as [full name],Crs_Name
from Student s,Stud_Course sc,Course c
where s.St_Id=sc.St_Id and c.Crs_Id= sc.Crs_Id and Grade is not null

--- Display number of courses for each topic name
select count(crs_id),Top_Id
from course 
group by Top_Id


--- Display max and min salary for instructors
select max(salary),min(salary)
from Instructor


--- Display instructors who have salaries less than the average salary of all instructors
select Ins_Name
from Instructor
where salary < (select AVG (salary) from Instructor)



--- Display the Department name that contains the instructor who receives the minimum salary
select Dept_Name
from Department d,Instructor i
where d.Dept_Id=i.Dept_Id and Salary in (select min (salary) from Instructor)



---  Select max two salaries in instructor table.
select top(2) salary
from Instructor
order by 1 desc 


--- Select instructor name and his salary but if there is no salary display instructor bonus. “use one of coalesce Function”  
select Ins_Name,coalesce(Salary,bonus)         
from Instructor



--- Select Average Salary for instructors 
select AVG(salary)
from Instructor



--- Select Student first name and the data of his supervisor   
select y.St_Fname,x.St_Age                                   
from student x inner join Student y
on y.St_Id =x.St_super 



--- Write a query to select the highest two salaries in Each Department for instructors who have salaries. “using one of Ranking Functions”
select salary 
from(
select salary ,
row_number() over (partition by dept_id order by salary desc ) as RN
from Instructor) as newtable
where Salary is not null and rn<=2




 --- Write a query to select a random  student from each department.  “using one of Ranking Functions”
  select st_fname
  FROM(
 select st_fname,
 row_number() over (partition by dept_id order by newid() ) as RN 
 from student ) as newtable
 where rn=1
```