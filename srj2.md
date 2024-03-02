sal 
- row_number() 
- rank() 
- dense_rank()

10000
10000
20000
30000
 # Finding nth highest/lowest any salary----
```sql
select * from(select emp_id,emp_name,emp_salary,dense_rank() over(order by emp_salary asc)rn from emp) where rn IN (1,2,8,5);
```

    EMP_ID EMP_NAME             EMP_SALARY         RN

         1 John Doe                  50000          1
         4 Emily Davis               52000          2
         3 Michael Johnson           55000          5
        11 Changu Mangu              59000          8
        10 Mary Taylor               59000          8
        
## ROW_NUMBER()
 ``````sql     
select emp_id,emp_name,emp_salary,row_number() over(order by emp_salary asc)rn from emp;
``````
    EMP_ID EMP_NAME             EMP_SALARY         RN

         1 John Doe                  50000          1
         4 Emily Davis               52000          2
         5 David Wilson              53000          3
         8 Jennifer Anderson         54000          4
         3 Michael Johnson           55000          5
         9 Christopher Martinez      57000          6
         6 Sarah Brown               58000          7
        11 Changu Mangu              59000          8
        10 Mary Taylor               59000          9
         2 Jane Smith                60000         10
         7 James Lee                 62000         11

11 rows selected.

## RANK()
``````
select emp_id,emp_name,emp_salary,rank() over(order by emp_salary asc)rn from emp;
``````

    EMP_ID EMP_NAME             EMP_SALARY         RN

         1 John Doe                  50000          1
         4 Emily Davis               52000          2
         5 David Wilson              53000          3
         8 Jennifer Anderson         54000          4
         3 Michael Johnson           55000          5
         9 Christopher Martinez      57000          6
         6 Sarah Brown               58000          7
        11 Changu Mangu              59000          8
        10 Mary Taylor               59000          8
         2 Jane Smith                60000         10
         7 James Lee                 62000         11

11 rows selected.

## DENSE_RANK()
``````
select emp_id,emp_name,emp_salary,dense_rank() over(order by emp_salary asc)rn from emp;
``````

    EMP_ID EMP_NAME             EMP_SALARY         RN

         1 John Doe                  50000          1
         4 Emily Davis               52000          2
         5 David Wilson              53000          3
         8 Jennifer Anderson         54000          4
         3 Michael Johnson           55000          5
         9 Christopher Martinez      57000          6
         6 Sarah Brown               58000          7
        11 Changu Mangu              59000          8
        10 Mary Taylor               59000          8
         2 Jane Smith                60000          9
         7 James Lee                 62000         10

11 rows selected.
``````
select emp_id,emp_name,emp_salary,did,dense_rank() over(partition by did order by emp_salary asc)rn from emp;


    EMP_ID EMP_NAME             EMP_SALARY        DID         RN
---------- -------------------- ---------- ---------- ----------
         1 John Doe                  50000         10          1
         5 David Wilson              53000         10          2
         3 Michael Johnson           55000         10          3
         6 Sarah Brown               58000         10          4
        10 Mary Taylor               59000         10          5
         4 Emily Davis               52000         20          1
         8 Jennifer Anderson         54000         20          2
         2 Jane Smith                60000         20          3
         9 Christopher Martinez      57000         30          1
        11 Changu Mangu              59000         30          2
         7 James Lee                 62000         30          3
         
  