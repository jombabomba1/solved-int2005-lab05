Download Link: https://assignmentchef.com/product/solved-int2005-lab05
<br>
Database Management System

<strong> </strong>

<strong> </strong>

<strong>The View WITH CHECK OPTION Clause</strong>

The WITH CHECK OPTION is an integrity constraint on <strong>an updatable view</strong> to prevent inserts to rows for which the WHERE clause in the select_statement is not true. WITH CHECK OPTION testing is standard-compliant.

<strong> </strong>

<strong>Syntax for creating a view </strong><strong><em> </em></strong>

<strong><em> </em></strong>

<h1>CREATE[OR REPLACE]</h1>

<strong>    </strong><strong>VIEW</strong><strong> view_name </strong><strong>[(</strong><strong>column_list</strong><strong>)]</strong>

<strong>    </strong><strong>AS</strong><strong> select_statement  </strong>

<strong>[WITH [<u>CASCADED</u> | LOCAL] CHECK OPTION]</strong>;




<strong>The Syntax of CREATE VIEW statement</strong>:

Documentation: <a href="https://dev.mysql.com/doc/refman/8.0/en/create-view.html">https://dev.mysql.com/doc/refman/8.0/en/create</a><a href="https://dev.mysql.com/doc/refman/8.0/en/create-view.html">–</a><a href="https://dev.mysql.com/doc/refman/8.0/en/create-view.html">view.html</a>




The WITH CHECK OPTION clause can be given for an updatable view to prevent inserts or updates to rows except those for which the WHERE clause in the select_statement is true.

In a WITH CHECK OPTION clause for an updatable view, the LOCAL and CASCADED keywords determine the scope of check testing when the view is defined in terms of another view. The LOCAL keyword restricts the CHECK OPTION only to the view being defined. CASCADED causes the checks for underlying views to be evaluated as well. When neither keyword is given, <u>the default is CASCADED</u>.

Resource: <a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">https://www.mysqltutorial.org/mysql</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">view</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">local</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">cascaded</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">in</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">with</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">check</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">–</a><a href="https://www.mysqltutorial.org/mysql-view-local-cascaded-in-with-check-option">option</a>




<strong>Example: </strong>

<strong> </strong>

CREATE TABLE t1 (a INT);




CREATE OR REPLACE VIEW v1

AS SELECT *

FROM t1

WHERE a &lt; 2;







CREATE OR REPLACE VIEW v2

AS SELECT *

FROM v1 WHERE a &gt; 1

WITH <strong>LOCAL</strong> CHECK OPTION;




CREATE OR REPLACE VIEW v3

AS SELECT *

FROM v1

WHERE a &gt; 0

WITH CASCADED CHECK OPTION;

<strong> </strong>

<strong>Evaluate the following INSERT statements: </strong>— 1. What is the result?

INSERT INTO v2 VALUES (1);

— The “CHECK OPTION failed” error is returned because the ”a &gt; 1” WHERE condition of V2 is False.

— 2. What is the result?

INSERT INTO v2 VALUES (3);

— The INSERT statement is executed successfully because the ”a &gt; 1” WHERE condition of V2 is True.

— 3. What is the result?

INSERT INTO v3 VALUES (1);

— The INSERT statement is executed successfully because both the ”a &gt; 0” WHERE condition of V3 and the “a &lt; 2” WHERE condition of V1 are True.

— 4. What is the result?

INSERT INTO v3 VALUES (3);

— The “CHECK OPTION failed” error is returned because only the ”a &gt; 0” WHERE condition of V3 is True while the “a &lt; 2” WHERE condition of V1″ is False.

<strong> </strong>

<strong>Subquery Review: </strong>

A subquery is a <u>SELECT</u> statement within another statement.

<strong> </strong>

<ul>

 <li>Type 1 – <strong>Nested Subquery</strong>: Database evaluates the whole query in two steps: ○ First, execute the subquery (inner query).</li>

</ul>

○ Second, use the result of the subquery in the parent statement (outer query).

<ul>

 <li>Type 2 – <strong>Correlated Subquery</strong>: Database evaluated once for each row processed by the parent statement.</li>

</ul>

○ This operation is used when a subquery refers to a column from a table in an outer query.

○ The unqualified columns in the subquery are resolved by looking in the tables named in the inner query and then in the tables named in the outer query.




Subquery Documentation:<a href="https://dev.mysql.com/doc/refman/8.0/en/subqueries.html"><strong>https://dev.mysql.com/doc/refman/8.0/en/subqueries.html</strong></a>

<strong>Subquery in DML statements </strong>

<ul>

 <li>INSERT statement – adds new rows of data to a table</li>

 <li>UPDATE statement – modifies existing data in a table</li>

 <li>DELETE statement – removes rows of data from a table</li>

</ul>

<strong>— Syntax — </strong>

<strong>INSERT</strong> <strong>INTO</strong><strong> table_name|view_name [</strong><strong>(</strong><strong>column_list</strong><strong>)</strong><strong>] </strong>

<strong>  </strong><strong>SELECT</strong><strong> column(s) </strong>

<strong>  </strong><strong>FROM</strong><strong> table_name| view_name  </strong>

<strong>  [WHERE</strong><strong> condition(s)</strong><strong>]</strong><strong>;</strong>




<strong> UPDATE</strong><strong> table_name|view_name  </strong>

<strong>SET </strong><strong> column = value [,column2 = value2,…] </strong>

<strong> [WHERE</strong><strong> condition(s)</strong><strong>]</strong><strong>;</strong>




<strong> DELETE</strong><strong> table_name|view_name  </strong>

<strong> [WHERE</strong><strong> condition(s)</strong><strong>]</strong><strong>;</strong>




<strong>SAFE-UPDATES option </strong>

MySQL session has the safe-updates option set (SET SQL_SAFE_UPDATES = 1). This means that you can’t update or delete records without specifying a key (ex. primary key) in the WHERE clause. If you want to disable the safe-updates option, you can set  SET SQL_SAFE_UPDATES = 0.




<u>MySQL Workbench</u>: Checking the safe-updates option

Menu =&gt; Tools/MySQLWorkbench =&gt; Preferences  =&gt; SQL Editor =&gt; Safe-updates













<strong>AUTOCOMMIT Mode</strong>

By default, MySQL starts the session for each new connection <u>with </u><a href="https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_autocommit">autocommit</a> <u>enabled</u>, so MySQL does a commit after each SQL statement if that statement did not return an error.




If <strong><u>autocommit</u></strong> mode is disabled within a session with SET autocommit = 0, the session always has a transaction open. A <a href="https://dev.mysql.com/doc/refman/8.0/en/commit.html">COMMIT</a> or <a href="https://dev.mysql.com/doc/refman/8.0/en/commit.html">ROLLBACK</a> statement ends the current transaction and a new one starts. If a session that has <a href="https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_autocommit">autocommit</a> disabled ends without explicitly committing the final transaction, MySQL rolls back that transaction.




<u>MySQL Workbench:</u> Checking the autocommit mode

Menu =&gt; Tools/MySQLWorkbench =&gt; Preferences  =&gt; SQL Execution




<u>Switch to SQL Editor</u>

<ul>

 <li>You should specify the classicmodels database before writing SQL statements using the following command:</li>

</ul>

USE db_name;




The <a href="https://dev.mysql.com/doc/refman/8.0/en/use.html">USE</a>statement tells MySQL to use the named database as the default (current) database for subsequent statements. This statement requires some privilege for the database or some object within it.

<strong> </strong>

<strong> The ER diagram for the classicmodels.</strong>

<u>Note:</u> The MSRP is “Manufacturer’s suggested retail price” (ราคาขายปลกี แนะน าของผผู้ ลติ).

<strong>MySQL Workbench: </strong>

<ul>

 <li>You can see details of a view by clicking i button below:</li>

</ul>




<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong>Task 1: Using the </strong>”<strong>classicmodels</strong>”<strong> database and write SQL statements to answer the following questions. </strong>

<strong> </strong>

use classicmodels;




<ol>

 <li>Create a new table named ”usa_customers” with copying only the structure of four columns: customernumber, customername, city, country of the ”customers” table. Do not copy any data from the ”customers” table. Please verify by querying data from the table. — Write a statement(s) here</li>

</ol>




<ol start="2">

 <li>Insert data by copying the existing data of all customers who live in the USA from the ”customers” table into the “usa_customers” table. Please verify by querying data from the table. How many rows are inserted into the “usa_customers” table.</li>

</ol>

— Write a statement(s) here and also capture the screen of querying data from the table.




<ol start="3">

 <li>Based on the ”usa_customers” table, modify the city of the customername “Mini Wheels Co.” to the same city of the customer number 344 of the “customers” table. Please verify your data modification.</li>

</ol>

— Write a statement(s) here and also capture the screen of querying data from the table.




<ol start="4">

 <li>Based on the ”usa_customers” table, modify the city of all customers who have a sales representative (employee) last named “Patterson” to “Bangmod”. Please verify your data modification.</li>

</ol>

Hint: you may use the customers and employees tables to find out “who have a sales representative (employee) last named “Patterson”.

— Write a statement(s) here and also capture the screen of querying data from the table.




<ol start="5">

 <li>Modify an existing view named “mini_customer_view” to display the customer number, customer name, city and country of all customers whose names start with the word “Mini” from the ”usa_customers” table. Name four columns of this view to “cno”, ”cname”, “city” and ”country”, respectively. Please verify by querying data from this view.</li>

</ol>

— Write a statement here(s) and also capture the screen of querying data from the table/view.




<ol start="6">

 <li>Create a view named “miniltd_customer_view” to display the customer number, customer name, city and country of all customers whose names end with the word “Ltd.” from the “mini_customer_view” view. <u>Please ensure that the rows that are being changed through this view</u> <u>are conformable to the definition of the “miniltd_customer_view” view</u>. Name four columns of this view to “custno”, “custname”, “custcity” and “custcountry”, respectively. Please verify by querying data from this view.</li>

</ol>

— Write a statement(s) here and also capture the screen of querying data from the table/view.




<ol start="7">

 <li>Insert new data {customer number “9000”, customer name ”SUNISA Ltd.”, city ”Texas” and country ”USA”} through the “miniltd_customer_view” view. Please verify by querying data from both this view and the base table. Can the data be inserted through this view? If not, please explain. — Write a statement(s) here</li>

</ol>




<ol start="8">

 <li>Insert new data {customer number “9001”, customer name ”Mini SUNISA”, city = ”Texas” and country ”USA”} through the “miniltd_customer_view” view. Please verify by querying data from both this view and the base table. Can the data be inserted through this view? If not, please explain. — Write a statement(s) here</li>

</ol>




<ol start="9">

 <li>Modify an existing view named the “miniltd_customer_view” created in Question 6 to ensure that the rows that are being changed through this view are conformable to the definition of the “miniltd_customer_view” view and also the definition of the underlying views recursively.</li>

</ol>

— Write a statement(s) here and also capture the screen of querying data from the table/view.




<ol start="10">

 <li>Try to insert the same data of Question 7-8 again.</li>

</ol>




What happened to the row of the customer name ”SUNISA Ltd.”? Please verify by querying data from both this view and the base table. Can the data be inserted through this view? If not, please explain.

— Write a statement(s) here




What happened to the row of the customer name ”Mini SUNISA” ?  Please verify by querying data from both this view and the base table. Can the data be inserted through this view? If not, please explain.

— Write a statement(s) here




<ol start="11">

 <li>Please insert one row through the “miniltd_customer_view” view. You should create the data by yourself that can be inserted through this view. Please verify by querying data from both the views and the base table.</li>

</ol>

— Write a statement(s) here and also capture the screen of querying data from the table/view.




<ol start="12">

 <li>Remove two existing views that were<u> created in Lab04</u>. You can select two views by yourself. — Write a statement(s) here</li>

</ol>





