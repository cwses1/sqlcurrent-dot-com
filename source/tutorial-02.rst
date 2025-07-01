.. _tutorial-02:

Tutorial 2 - Create A Standalone Database And Tables
===============================================
Let's use SQL Current to create a new, standalone database and add some tables to it.
Before proceeding, ensure you've followed the steps in the :ref:`setup-section` section.

Get a database server up and running
-----------------------------
This is probably the most difficult step if it's not already done.
Make sure you have a database server, such as PostgreSQL or SQL Server, up and running.
In this tutorial, we are going to use SQL Server.
The process is essentially the same for other database servers.
Only the SQL syntax changes.

Write the SQL file ``create.sql``
-----------------------
Write a SQL Server SQL script that creates a couple of tables and save it to ``create.sql``.

.. code-block :: sql

	create table table1
	(
		table1_id int primary key
	);

	create table table2
	(
		table2_id int primary key
	);

Note that you could run the above script directly in ``psql`` or ``pgadmin`` without any changes.
SQL Current does not invent any new language for modifying your databases.
It uses the native language of the database (whatever appears in your SQL script, in this case), such as SQL, for doing everything.

Write the SCS ``script.txt`` file
-----------------------------
SQL Current's language is called **SQL Current Script**, or **SCS** for short.
Create the following SCS file ``script.txt`` and save it in the same directory as ``create.sql``.

.. code-block :: none

	database my_db
	{
		driver: 'psycopg';
		connString: 'host=127.0.0.1 port=5432 dbname=my_db user=postgres password=postgres';
		create: 'create.sql';
		dir: '';
	}

	create database mydb;

Here is what happens when you run the above SCS script:

#. Database ``my_db`` is defined.
#. SQL Current connects to the database server using the ``psycopg`` Python driver using the ``connString`` property.
#. SQL Current looks for the ``create.sql`` file in the current directory, specified by the empty ``dir`` property.
#. The text inside ``create.sql`` is sent to the server to create the new tables.
#. SQL Current will report success or failure of the script you know what's going on.

Run the SCS file 
-----------------------
Run the following command in your shell / console / terminal:

.. code-block :: none

	% sqlcurrent script.txt

If there are no errors you should see output like this:

.. code-block :: none

	my_db: Creating database.
	my_db: Running '/Projects/Database_Migrations/create.sql'.
	my_db: Success.

However, it's more common to get errors during initial setup.
Check for network connectivity and firewall issues.
Verify the credentials are correct.
SQL Current will print out any errors or exceptions to the terminal that it encounters.
Here is an example of a failed script run against a SQL Server database:

.. code-block :: none

	my_db: Creating database.
	my_db: Running '/Projects/Database_Migrations/create.sql'.
	my_db: Error. (15007, b"'postgres' is not a valid login or you do not have permission.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20018, severity 11:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20018, severity 11:\nGeneral SQL Server error: Check messages from the SQL Server\n")

SQL Current will stop for any error.

Continue once you have received a success response.

Verify the tables were created
-----------------------
Use ``psql`` or ``pgadmin`` to verify the table was created in your database.

Verify the database version
-----------------------

.. code-block :: none

	select databases;

Verify the update tracking file was created
-----------------------
SQL Current keeps track of each data in an **update tracking file.**
There is one (1) update tracking file per database definition.

Look for directory ``sqlcurrent_updatingtracking`` and find the update tracking file for this database.

* :ref:`update-tracking-file`
