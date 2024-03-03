## lag()-previous record

select ---------lag(colname,offset,default) over(order by colname)alias   from  tablename;
```sql
select emp_id,emp_name,emp_salary,did,dense_rank() over(partition by did order by emp_salary asc)rn,lag(emp_salary,1,0) over(order by emp_salary)pre from emp;
```

|    EMP_ID| EMP_NAME            | EMP_SALARY|        DID |        RN |       PRE
|----------| --------------------| ----------| ---------- |---------- |----------
|         1| John Doe            |      50000|         10 |         1 |         0
|         4| Emily Davis         |      52000|         20 |         1 |     50000
|         5| David Wilson        |      53000|         10 |         2 |     52000
|         8| Jennifer Anderson   |      54000|         20 |         2 |     53000
|         3| Michael Johnson     |      55000|         10 |         3 |     54000
|         9| Christopher Martinez|      57000|         30 |         1 |     55000
|         6| Sarah Brown         |      58000|         10 |         4 |     57000
|        10| Mary Taylor         |      59000|         10 |         5 |     58000
|        11| Changu Mangu        |      59000|         30 |         2 |     59000
|         2| Jane Smith          |      60000|         20 |         3 |     59000
|         7| James Lee           |      62000|         30 |         3 |     60000


## lead()-next record
```sql
 select emp_id,emp_name,emp_salary,did,dense_rank() over(partition by did order by emp_salary asc)rn,lead(emp_salary,1,0) over(order by emp_salary)next from emp;
 ```

|    EMP_ID| EMP_NAME            | EMP_SALARY |       DID |        RN |      NEXT
|----------| --------------------| ---------- |---------- |---------- |----------
|         1| John Doe            |      50000 |        10 |         1 |     52000
|         4| Emily Davis         |      52000 |        20 |         1 |     53000
|         5| David Wilson        |      53000 |        10 |         2 |     54000
|         8| Jennifer Anderson   |      54000 |        20 |         2 |     55000
|         3| Michael Johnson     |      55000 |        10 |         3 |     57000
|         9| Christopher Martinez|      57000 |        30 |         1 |     58000
|         6| Sarah Brown         |      58000 |        10 |         4 |     59000
|        10| Mary Taylor         |      59000 |        10 |         5 |     59000
|        11| Changu Mangu        |      59000 |        30 |         2 |     60000
|         2| Jane Smith          |      60000 |        20 |         3 |     62000
|         7| James Lee           |      62000 |        30 |         3 |         0
 

 ``````        
create table emp2 as select * from emp;        //to copy table
create table emp2 as select * from emp where 1=2;    //copy just table structure
create table emp2 as select * from emp where id=2;    //copy table with require data
``````
# view:temporary table
* views are stored in information_schema.views 
* views are 2 types
    1. simple-
	     - select statement-
  where-
  in column
  	     - Insert/Update/Delete will support
    2. complex-
	    - select statement-
	union,joins,window functions
    	- Insert/Update/Delete will not support

## MATERIALIZED VIEW(only in oracle)
- when accessing data from such view it stores that data after first time it accessed.which increses the performance but also takes memory

# indexes--(only sql server supports)

* create index to increse performace when fetching data
* clustered index-phisycally rows /data will get ordered
* non-clustered index- reference is used for indexing.i.e.refernced through memory address without physically moving data
* one table only one clustered index----can be multiple non-clustered index

=======================**Points yet to study**================================================

relations between tables-
1 to 1
1 to many
many to 1
many to many

==========================================================

ACID property

==========================================================

normalization



