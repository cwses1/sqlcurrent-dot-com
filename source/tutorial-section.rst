.. _create-tutorial-section:

Create Tutorial
===============================================
In this tutorial, we start with an existing database and create the schema objects in it.

Before proceeding, ensure you've followed the steps in the :ref:`setup-section` section.

Get a database running
-----------------------
This is the most difficult step.
You need to get database server up and running.
For this tutorial, also have a database created for that server using the server specific utilities.
SQL Current also supports creating the physical database for servers that support it, but that is out of scope for this tutorial.

Write a Current Script file
-----------------------
SQL Current's language is called **Current Script**.
This current script defines a PostgreSQL database.
It then *creates* the database by running the ``create.sql`` file.

::

	//
	// DEFINE THE DATABASE.
	//
	database mydb
	{
		driver: 'postgres';
		connString: 'host=127.0.0.1 port=5432 dbname=mydb user=postgres password=postgres';
		create: './create.sql';
	}

	//
	// CREATE THE DATABASE.
	//
	create database mydb;

Save this script to ``script.txt``.
When we run this script, SQL Current will execute the ``create.sql`` file.
But first we must write the ``create.sql`` file which contains all of the DDL and DML we need to create the database objects.

Write the ``create.sql`` file
-----------------------

::

	create table sqlcurrent_record
	(
		record_id int primary key
	);


Run the Current Script
-----------------------
Run the following command in your shell / console / terminal: ::

	% sqlcurrent script.txt

If there are no errors you should see output like this:

::

	mydb: Creating database.
	mydb: Running '/Projects/Database_Migrations/create.sql'.
	mydb: Success.

However, you should expect errors because it is very common during the initial setup of the database.
Check for network connectivity and firewall issues.
Verify the credentials are correct.
SQL Current will print out any errors or exceptions to the terminal that it encounters.
Here is an example of a failed script run from SQL Server:

::

	mydb: Creating database.
	mydb: Running '/Projects/Database_Migrations/create.sql'.
	mydb: Error. (15007, b"'postgres' is not a valid login or you do not have permission.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20018, severity 11:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20018, severity 11:\nGeneral SQL Server error: Check messages from the SQL Server\n")

SQL Current will stop for any error or failed check.

Continue once you have received a success response.

Verify the table was created
-----------------------
Use ``psql`` or pgadmin to verify the table was created in your database.

Verify the update tracking file was created
-----------------------
SQL Current keeps track of each data in an **update tracking file.**
There is one (1) update tracking file per database definition.

Looks for directory ``sqlcurrent_updatingtracking`` and find the update tracking file for this database.

Verify the database version
-----------------------

::

	select databases;

