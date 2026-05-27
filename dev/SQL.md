**SQL**

Relational databases consists of tables of rows and columns, there is relation between tables in relational database , sql is the query language for relational database, RDBMS is relational database management system to control and manage the database like MYSQL, SQL SERVER, ORACLE

DML statements : are used to read and modify data

SELECT **Count**(country) from table A

Select **Distinct** country from table A

![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.001.png)SELECT \* from table A **Limit** 5  -à only first 5 rows

**INSERT INTO** table A (country , name , age) **VALUES** (‘’ , ‘’) 	insert multiple rows 

`                               `**Values** (‘’ ,’’ )

à the number of values and column names should be same

**Update** A 

`   `set country = ‘’, age = ‘’

**DELETE** from A

**Relational Database**

Relational model allows for data independence – storing in table allow for independence

**ERD** à entity relationship diagram / relationshis between tables (entity)/ attriutes are columns

Entities are independence of any other entities 

Entities have attributes : tell us more about entity

![Diagram

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.002.png)

**Datatypes** : 

Varchar : when the characters are of variant length like a book title

Char: when the characters are of fixed length

Each table is assigned a **primary key** that uniquely identifys each row in table preventing duplication of data and define a way to define relationships between tables

Tables can have **foreign keys** that are primary keys of other tables and define a ink to that table

**Cloud databases** 

**Examples of relational databases on cloud** : IBM Db2 , PostgreSQL on cloud, Oracle database on cloud, Microsoft Azure SQL database, Amazon relational database

![Diagram

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.003.png)

SQL statements : 

**DDL** : data definition : define, change, drop data / create , alter, drop**, truncate** -> delete data in table but not the table itself

**DML**: data manipulation : read and modify datas /insert , select , update , delete -> removes row from table

![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.004.png)![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.005.png)![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.006.png)![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.007.png)![Text

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.008.png)![Graphical user interface

Description automatically generated with low confidence](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.009.png)

![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.010.png)![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.011.png)![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.012.png)![Graphical user interface, text, application

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.013.png) ![Text

Description automatically generated with low confidence](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.014.png) delete all the rows in              

`                                                                                                                  `table but not the table itself

**SELECT Statement**

![Text

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.015.png)

![Graphical user interface, text, application

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.016.png)



![](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.017.png)

![Graphical user interface, text

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.018.png) -à order by title DESC

![Table

Description automatically generated with medium confidence](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.019.png) oder by 2 à column 2

![Text

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.020.png)![Table

Description automatically generated](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.021.png)

![Text, table

Description automatically generated with medium confidence](Aspose.Words.1f9ac5ef-6a67-4f66-86ed-94668c2d2ab8.022.png)
