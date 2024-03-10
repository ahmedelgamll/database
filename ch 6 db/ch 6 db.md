  # ch6 ..The relational algebra and calculus
- هي مجموعه من العمليات التي تطبق علي الجداول لتنفيذ quries واسترجاع البيانات
- the result of an operation is a new relation , which may have been formed from one or more input relations.
- A sequence of relational algebra operations Forms a relational algebra expression.
  ___
   ### Relational Algebra consists of several groups of operations

 1- Unary Relational Operations
   - SELECT
   - PROJECT
  - RENAME
  
 2- Relational Algebra Operations From Set Theory
 - UNION  , INTERSECTION , DIFFERENCE (or MINUS - )
 - CARTESIAN PEODUCT (product of relations with each other)
  
 3- Binary Relational Operations
 - JOIN (several variations of JOIN exist)
- DIVISION
  
 4- Additional Relational Operations

- OUTER  JOINS , OUTER UNION
- AGGREGATE FUNCTIONS ( These compute summary of information : for Example SUM , COUNT , AVG , MIN , MAX
___
### (1) Unary Relational Operations

is executed on only one relation.

` 1. SELECT Operation σ (sigma)`

is used to select a subset of the tuples from a relation based on a selection condition.

تستخدم فى اختيار صف معين محدد من الجدول بناء على شرط معين

- the selection condition acts as a filter.
- we can take more than one condition by using and &  ,  or || .
- The number of tuples in the result of a SELECT is less than
(or equal to) the number of tuples in the input relation R

**general form eqn:**

![1](../ch%206%20db/pics/1.png)


___
### 2. PROJECT Operation σ (PI)

- PROJECT Operation is denoted by π (pi)
- PROJECT keeps certain columns (attributes) form a relation and discards the other column.

هى عمليه تستخدم لاختيار أعمده معينه من الجدول دون غيرها مع عدم التكرار

- PROJECT creates a vertical partitioning
- The list of needed columns (attributes) is kept in each tuple.
- The other attributes in each tuple are discarded 
- project operation removes any duplicate tuples
- so , The number of tuples in the result of projection is always less or equal to the number of tuples in R (the original relation <= الجدول الاساسى اللى من غير اى عمليات عليه )

![2](../ch%206%20db/pics/2.png)
___
` (2) Relational Algebra Operations From Set Theory`

### UNION Operation ∪

- Binary Operation  , denoted by ∪
- the result of R ∪ S , is a relation that includes all tuples that are either in R or in S or in both R and S.
- NO Duplicate tuples.
- The two operand relations R and S must be “Type Compatible”
    - R and S must have same number of attributes
    - Each pair of attributes must be the same datatype (have same domains).
  ![u](../ch%206%20db/pics/union.png)

### INTERSECTION Operator ∩

- INRESECTION is denoted by ∩
- the result of the operation R ∩ S , is a relation that includes all tuples that are in both R and S.
- the two operand relations R and S must be Type Compatible
     -   R and S must have same number of attributes
    - Each pair of attributes must be the same datatype (have same domains).


### SET DIFFERENCE –

- SET DIFFERENCE (also called MINUS or EXCEPT) is denoted by –
- the result of R – S , is a relation that includes all tuples that are in R but not in S .
- Two operand relations R and S must be “Type Compatible”.
    - R and S must have same number of attributes
    - Each pair of attributes must be the same datatype (have same domains).



### CARTESIAN PRODUCT Operation X

هى عمليه الغرض منها دمج البيانات الموجوده فى الجدولين (طرفى العملية) فى جدول واحد - 
- فيها كل صف من الجدول الاول بياخد كل صف من الجدول التاني
- Denoted By R(A1 , A2 , …. , An) X S( B1 , B2 , …. , Bm)
- Result is a relation Q with degree n+m attributes
    - Q(A1,A2, … , An , B1 , B2 , …. , Bm) in that order.
- number of tuples is n*m
- the two operand do NOT have to be “Type Compatible”.
  ![6](../ch%206%20db/pics/6.png)

$👀$ CROSS PRODUCT is not a meaningful operation , But it can become meaningful whenfollowed by other operations like SELECT Operation.**
  

  ` 3) Binary Relational Operation`

### JOIN Operation

بيكون طالب عرض بيانات موجوده في اكتر من جدول

it is an operation that used to join the rows of the first relation with the rows of the second relation According to a join Condition .

join condition is an attribute in first relation equal another attribute in second relation.

It called EquiJoin → two attributes have not the same name

join == cartesian product operation + select operation

R1 columns = R columns + S columns

- it is better than CARTESIAN PRODUCR Operation
- this operation is very important , because it allows us combine related tuples from various relations.

**EXAMPLE:**
![5](../ch%206%20db/pics/5.png)
![4](../ch%206%20db/pics/4.png)
![3](../ch%206%20db/pics/3.png)

### In case no common attribute in two relation → try to find another relation has a common link between them>>>

find name of employee and the projects he works on
![7](../ch%206%20db/pics/7.png)
![8](../ch%206%20db/pics/8.png)

**Natural join   R1 ← R * S**

  In case the two attributes have the same name in tables,  Don’t have to set a condition

![9](../ch%206%20db/pics/9.png)


**OUTER JOIN**
to reduce data loss.  



1- left outer join

![10](../ch%206%20db/pics/10.png)

2- right outer join

![11](../ch%206%20db/pics/11.png)

3- full outer join

![12](../ch%206%20db/pics/12.png)



### DIVISION Operation (/,÷)

you could say that , The division operator is used for queries which involve the ' all ' .
 
 Division operator A ÷ B can be applied if and only if :
 1. attributes of B is subset of attributes of A
 2. the attributes of the returned relation will be (all attributes of A - all attributes of B)
 3. the relation returned by division operator will return tuples from relation A which are associated to every B's tuple. 
![13](../ch%206%20db/pics/13.png)

advanced example:
![14](../ch%206%20db/pics/14.png)
![15](../ch%206%20db/pics/15.png)
![16](../ch%206%20db/pics/16.png)


___

` (4) Additional Relational Algebra Operation`

### Aggregate Functions 
it is a collection of functions that used in simple statistical queries to summarize information from the database tuples.

هى مجموعه من الدوال الرياضية الحصائية و التى تستخدم للحصول على معلومات احصائيه عن البيانات المخزنة فى الجداول                                                                                                         

AVG,MAX,MN,COUNT

it is applied on just one column from the relation.

The COUNT function is used for counting tuples or values Wthout removing dublicates

![17](../ch%206%20db/pics/17.png)


**Grouping:** 

هي عملية تقسيم الصفوف في الجدول الي مجموعات بناء علي قيمه عمود معين(Attribute) ثم يتم تنفيذ ال aggregate function علي كل مجموعه بشكل منفصل

Each(employee,department...) ⇒ indicate to use grouping

![18](../ch%206%20db/pics/18.png)
![19](../ch%206%20db/pics/19.png)



___ 
`EXAMPLES ON THE RELATIONAL ALGEBRA:`

[first video](https://www.youtube.com/watch?v=bX7rFFODwIw&list=PL37D52B7714788190&index=29)

[second video](https://www.youtube.com/watch?v=wsC2N3XJysQ&list=PL37D52B7714788190&index=30)

[third video](https://www.youtube.com/watch?v=xfJ5IRSEnDI&list=PL37D52B7714788190&index=31)
___
