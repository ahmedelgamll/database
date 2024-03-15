![1](../ITI/pics/1.png)

**ANSI:**

 هي library فيها كل ال queries بتاعه sql وابتدت كل شركه كبيره تستخدمها وتعدل عليها وتقسمها الي مجموعه من ال categories


### DDL:
![2](../ITI/pics/2.png)

 create: create Table

alter:add, delete, or modify columns in an existing table
___
### DML:
**insert:**

![3](../ITI/pics/3.png)


**update and delete:**
![4](../ITI/pics/4.png)
___
### DQL:
- select:
- ![5](../ITI/pics/5.png)

  ___
  ## Joins:
  
 ![5](../ITI/pics/6.png)

we will discuss these 2 tables:  
![7](../ITI/pics/7.png)

**cross join:**  
without where(condition)
```sql
selsect sname,dname
from student ,dept
```

**inner (Equi) join**  
there is where condition :match the primary key of one table  with the foreign key of the another table

```sql
selsect sname,dname
from student s ,dept d
where d.did=s.did
```
OR
```sql
selsect sname,dname
from student s inner join dept d
on d.did=s.did
```
**outer join:**
1.  left outer join: will get all the left rows with if it matches a value of the right table or not (is null)
   
     ```sql
        selsect sname,dname
        from student s left outer join dept d
        on d.did=s.did
      ```
2.   right outer join: will get all the right rows with if it matches a value of the left table or not (is null)
      ```sql
        selsect sname,dname
        from student s right outer join dept d
        on d.did=s.did
      ```
3.  full outer join: will get all the rows from left or right even if no matches (null)
     ```sql
        selsect sname,dname
        from student s full outer join dept d
        on d.did=s.did
      ```


**self join:**


![8](../ITI/pics/8.png)

- like employee and manager.
- the table which has the foreign key is>> the child ,is existed in the database>>employee
- the copied table is the parent , is stored in the memory only >>manager
    ```sql
        selsect x.ename as empname ,y.ename as mgname
        from employee x ,employee y
        on y.eid=x.superid
    ```

  
**join multiple tables**

لو مفيش علاقه تربط جدولين ببعض وانا عايز داتا من الجدولين
- we must use bridge table  
- conditions=tables-1
    ```sql
        select Fname,Pname
        from Employee E,Project P,Works_for W
        where e.SSN=w.ESSn and p.Pnumber=w.Pno
    ```
OR

![10](../ITI/pics/10.png)


**join ,DMl**
**join ,Update**

![11](../ITI/pics/11.png)

note:      
 join   بعمل  
 
 لو انا عايز بيانات موجوده في جدول بمعلوميه بيانات موجوده في جدول تاني

 زي اعرضلي درجات الطلاب (موجوده في COURSE ) اللي عايشه في القاهره (موجوده في student)


**some built in functions**    
`how to exchange the null value:`
![12](../ITI/pics/12.png)
- null take one replacment     
-  Coalesce take multiple replacement     
   exchange Null value with any avilable data



`to combine two columns using contact fun`
- turn any column to string data type to concat between them
- replace any NULL value with empty string
![13](../ITI/pics/13.png)


 **like**: 
  as '=' ,its appended to:
    - ***_:*** one character
    - ***%:*** zero or more characters

```sql
        select *
        from student s
        where s.name like '_a%'
 ```
![14](../ITI/pics/14.png)



**order:**

![15](../ITI/pics/15.png)
___
## normalization :
i wrote an article about it before:
[normalization](https://medium.com/@a7medelgaml11a/functional-dependencies-normalization-088215f56dd5)

### two examples:
![17](../ITI/pics/17.png)
![18](../ITI/pics/18.png)
![19](../ITI/pics/19.png)
![20](../ITI/pics/20.png)
___
![16](../ITI/pics/16.png)

