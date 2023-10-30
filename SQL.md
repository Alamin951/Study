## IMP Link

https://www.w3schools.com/sql/sql_wildcards.asp

https://www.w3schools.com/sql/sql_like.asp

https://www.w3schools.com/sql/sql_in.asp

https://www.w3schools.com/sql/sql_isnull.asp

# quickly checking

https://www.w3schools.com/sql/sql_quickref.asp


## view
- Create a view
    ~~~
    CREATE VIEW view_name AS
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition;
    ~~~
- create or update a query
    ~~~
    CREATE OR REPLACE VIEW view_name AS
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition;
    ~~~
- Drop view
    ~~~
    DROP VIEW view_name;
    ~~~
	
## updating the existing table by the view
- view query formed using just one query
- view query cannot have distinct clause
- view query cannot have group by clause
- view query cannot have with clause
- view query cannot have window function
	

## Queries
    limit the output rows
    SELECT * FROM Customers
    WHERE Country='Germany'
    LIMIT 3;
	
 The following constraints are commonly used in SQL:

- **NOT NUL:L** Ensures that a column cannot have a NULL value
- **UNIQUE:** Ensures that all values in a column are different
- **PRIMARY KEY:** A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
- **FOREIGN KEY:** Prevents actions that would destroy links between tables
- **CHECK:** Ensures that the values in a column satisfies a specific condition
- **DEFAULT:** Sets a default value for a column if no value is specified
- **CREATE INDEX:** Used to create and retrieve data from the database very quickly
	
	
	
	
To name a UNIQUE constraint, and to define a UNIQUE constraint on multiple columns, use the following SQL syntax:

	CREATE TABLE Persons (
		ID int NOT NULL,
		LastName varchar(255) NOT NULL,
		FirstName varchar(255),
		Age int,
		CONSTRAINT UC_Person UNIQUE (ID,LastName)
	);
	
 The following SQL statement defines the "Personid" column to be an auto-increment primary key field in the "Persons" table:

	CREATE TABLE Persons (
		Personid int IDENTITY(1,1) PRIMARY KEY,
		LastName varchar(255) NOT NULL,
		FirstName varchar(255),
		Age int
	);
	
SQL Date Data Types
	MySQL comes with the following data types for storing a date or a date/time value in the database:

	DATE - format YYYY-MM-DD
	DATETIME - format: YYYY-MM-DD HH:MI:SS
	TIMESTAMP - format: YYYY-MM-DD HH:MI:SS
	YEAR - format YYYY or YY
	SQL Server comes with the following data types for storing a date or a date/time value in the database:

	DATE - format YYYY-MM-DD
	DATETIME - format: YYYY-MM-DD HH:MI:SS
	SMALLDATETIME - format: YYYY-MM-DD HH:MI:SS
	TIMESTAMP - format: a unique number
	Note: The date types are chosen for a column when you create a new table in your database!
	
- Format a number:

        SELECT FORMAT(123456789, '##-##-#####');

    gives the output of 12-34-56789
		

- to Use TypeQuery we must use an entry annotation on the DTO class to map with the entity object.
	
	
## SQL Trigger

A trigger is a stored procedure in a database that automatically invokes whenever a special event in the database occurs.
Every trigger has a table attached to it. Because a trigger can not be called directly, unlike a stored procedure, it is refers to a special procedure.
A trigger is automatically called whenever a data modification event against a table take place.

Before using trigger we need to be aware of the frequency and timing of changes to a table that is constantly changing.

Difference between trigger and stored procedure:
1. Triggers can not be manually invoked or executed.
2. There is no chance that triggers will receive parameters.
3. A transaction cannot be committed or rolled back inside a trigger.
	
Syntax:

	create trigger [trigger_name] : Creates or replaces an existing trigger with the trigger_name.

	[before | after]  : specifies when the trigger will be executed.

	{insert | update | delete}  : This specifies the DML operations.

	on [table_name]  : Table name.

	[for each row]  : row level trigger -> will be affected for each affected row.

	[trigger_body] : trigger operation to be performed. 
	
	
Example:Denka	

- mnt_budget_header INSERT trigger:
    ~~~
    CREATE TRIGGER mnt_budget_header_insert
    AFTER INSERT
    ON mnt_budget_header
    FOR EACH ROW INSERT INTO log_mnt_budget_header
    values (new.CREATED_BY, new.CREATED_DATE, null, null,
            new.ID,
            new.MST_COMPANY_ID,
            new.MST_FACTORY_ID,
            new.MST_DEPARTMENT_ID,
            new.MNT_PLANT_LOCATION_ID,
            new.MNT_PM_ACTIVITY_ID,
            new.MNT_BUDGET_MASTER_ID,
            new.FIRST_OR_SECOND_HALF,
            new.BUDGET_YEAR,
            new.BUDGET_AMOUNT,
            new.EQUIPMENT_NAME,
            new.TAG_NO,
            new.EQUIPMENT_RANK,
            new.EQUIPMENT_OR_SERVICE,
            new.INTERVAL_FROM,
            new.INTERVAL_TO,
            new.VENDOR_CODE,
            new.VENDOR,
            new.REMARKS,
            new.NO_OF_TIMES,
            new.FREQUENCY,
            new.CONTRACT_OR_ADHOC,
            new.MONTHLY,
            null, now(), 'insert', new.CREATED_BY);
    ~~~
- mnt_budget_header UPDATE trigger:
    ~~~
    CREATE TRIGGER mnt_budget_header_update
        AFTER UPDATE
        ON mnt_budget_header
        FOR EACH ROW INSERT INTO log_mnt_budget_header
        values (new.CREATED_BY, new.CREATED_DATE, new.MODIFIED_BY, new.MODIFIED_DATE,
                new.ID,
                new.MST_COMPANY_ID,
                new.MST_FACTORY_ID,
                new.MST_DEPARTMENT_ID,
                new.MNT_PLANT_LOCATION_ID,
                new.MNT_PM_ACTIVITY_ID,
                new.MNT_BUDGET_MASTER_ID,
                new.FIRST_OR_SECOND_HALF,
                new.BUDGET_YEAR,
                new.BUDGET_AMOUNT,
                new.EQUIPMENT_NAME,
                new.TAG_NO,
                new.EQUIPMENT_RANK,
                new.EQUIPMENT_OR_SERVICE,
                new.INTERVAL_FROM,
                new.INTERVAL_TO,
                new.VENDOR_CODE,
                new.VENDOR,
                new.REMARKS,
                new.NO_OF_TIMES,
                new.FREQUENCY,
                new.CONTRACT_OR_ADHOC,
                new.MONTHLY,
                null, now(), 'update', new.MODIFIED_BY);
	~~~					 
						 