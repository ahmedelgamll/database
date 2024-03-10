# ch10>> FUNCTIONAL DEPENDENCIES AND NORMALIZATION:

ال Relation المثالية هي التي تخلو من ال Redundancy والعيوب الناتجه عنه في عملية تحديث البيانات 

Redundancy causes :
1. waste of storage .
2. problems with update anomalies:
- insertion    anomalies
- deletion anomalies
- modification anomalies
  
مثال يوضح المشاكل اللي بتقابلني اللي انا عايز احلها:

![1](../ch%2010%20db/pics/1.png)


 `Update Anomaly `
- at EMP_PROJ ⇒ Changing the name of project number P1 from “Billing” to “Customer-Accounting” may cause this update to be made for all 100 employees working on project .
  
- same thing at Ename , if the same employee work at different projects his name will written more than one (redundancy) and that waste memory , it is enough to know ssn of the employee.
  
- at EMP_DEPT ⇒ Changing the manger of any Department that update will be made for all employees that work at this department , it is depend on the number of employees at department .

 `Insert Anomaly`
-  you can’t insert a project unless an employee is assigned to it , becaues ssn is pk.
- Conversely , you can’t insert an employee unless he/she is assigned to a project.
  
 `Delete Anomaly `
- when a project is deleted it will result in delete all the employees who work on that project.
- if an employee is the sole employee on a project , deleting that employee would result in deleting the project
 ___
 طب علشان احل المشاكل السابقه اعمل ايه؟؟


 **normalization:**

 The process of  organizing data and decomposing the bad relations by breaking up their attributes into smaller relation according to rules (normal forms)designed to protect the data and to make the database more flexible by eliminating redundancy and inconsistent dependency.


  
  طب علي اساس ايه بجزأ الجدول بتاعي لكام جدول اشمعنا مثلا 3 او 4 او..؟؟

  وعلي اساس ايه بردو بحط مثلا attribute 1 , 3 في اول جدول و2و4 في تاني جدول مثلا؟؟

  ..>>علي اساس ال **Functional Dependency**

  **Functional Dependency:**

  هي علاقه او ارتباط بين attribute  و attribute اخر في نفس الجدول.

  x->y  ... the value of x determines the value of y او y is functionally dependece of x

  EXAMPLES:

  Ssn->Ename    
  ssn determines emolyee name

  Pnum->{pname,plocation}    
  project num determines project name and location

  {ssn,pnum}->hour    
  ssn,project num determines the hours per week the employee works on the project

  - Note on Keys
    - PK → It is all unique attributes in table (SSN and Pnumber)
    - prime attribute (key attribute) → attribute is a member of PK (SSN or Pnumber)
    - non-key attribute ⇒ normal attribute
  
   ![8](../ch%2010%20db/pics/8.png)


types of FD:
   ![9](../ch%2010%20db/pics/9.png)

___
### normal forms:
![2](../ch%2010%20db/pics/2.png)

**first normal forms:**

Disallows:
- Composite attribute
- Multi-value attribute
- Nested relation(non atomic attribute)
  
  ex:

  ![5](../ch%2010%20db/pics/5.png)
![6](../ch%2010%20db/pics/6.png)

![7](../ch%2010%20db/pics/7.png)


**Second Normal Form:**
- must be first normal form 
- Disallow Partial Dependency
- A relation schema R is in second normal form (2NF) if every non-prime attribute A in R is fully functionally dependent on the primary key.

![10](../ch%2010%20db/pics/10.png)

**Third Normal Form**
- must be second normal form 
- Disallow Partial Dependency
   - Transitive Dependency → non-prime attribute depend on another non-prime attribute 
  
![11](../ch%2010%20db/pics/11.png)

**Boyce Codd Normal Form**
  - BCNF → X - > A, X must be super-key in this relation even if A is prime attribute
      - لا تسمح لاي attribute   ان يكون dependent الا علي primary key بتاع الجدول
  - Any relation in BCNF is a 3NF, but not the opposite
   
   ![12](../ch%2010%20db/pics/12.png)
___
![4](../ch%2010%20db/pics/4.png)

  





