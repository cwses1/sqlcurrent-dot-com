.. _tutorial-04:

Tutorial 4 - Branching
===============================================
Let's use SQL Current to create a new, standalone database and add some tables to it.
A standalone database is a database that does not belong to a branch.
Before proceeding, ensure you've followed the steps in the :ref:`setup-section` section.


Write the SQL files
-----------------------
Write a SQL script that creates the physical database ``my_db``.
Save the following script to ``create-database.sql``.

.. code-block :: sql

	create database my_db on
	(
		name = my_db_dat,
		filename = 'C:\\Data\\my_db.mdf',
		size = 64MB,
		maxsize = 512MB,
		filegrowth = 100%
	)
	log on
	(
		name = my_db_log,
		filename = 'C:\\Data\\my_db.ldf',
		size = 8MB,
		filegrowth = 0%
	);

	alter database heavywork_athena set recovery simple;

Write a SQL script that creates tables ``table1`` and ``table2``.
Save the following script to ``create-tables.sql``.

.. code-block :: sql

	create table table1
	(
		table1_id int primary key
	);

	create table table2
	(
		table2_id int primary key
	);

Note that you could run the above script directly in SSMS (SQL Server Management Studio) without any changes.

Write the SCS ``script.txt`` file
-----------------------------
SQL Current's built-in scripting language is called **Current Script**.
Create the following SCS file ``script.txt`` and save it in the same directory as ``create-database.sql`` and ``create-tables.sql``.

Let's incrementally define our standalone database, starting with the following database definition statement.

.. code-block :: none

	database my_db
	{
		driver: 'sqlserver';
		connString: 'server=myserver.sqlcurrent.com;user=sa;password=sandy;database=my_db;autocommit=1';
		create: './create-database.sql';
		create: './create-tables.sql';
	}

The current script above defines a database without a ``branch`` property, making it a standalone database.

* ``driver``: SQL Current will use the best SQL Server Python driver (``pymssql``) to connect to the database.
* ``connString``: The connection string for the driver.  Note the ``database=my_db`` component.  This is the name of the database we are creating.
* ``create``: There are two (2) create scripts defined.  They will be executed in the order they are specified.

Let's add a ``create database`` statement to ``script.txt``.

.. code-block :: none

	database my_db
	{
		driver: 'sqlserver';
		connString: 'server=myserver.sqlcurrent.com;user=sa;password=sandy;database=my_db;autocommit=1';
		create: './create-database.sql';
		create: './create-tables.sql';
	}

	create database mydb;

Execute ``script.txt``.

.. code-block :: none

	% sqlcurrent script.txt

The current script should fail with an error similar to this:

.. code-block :: none

	my_db: Creating database.
	my_db: Running '/Projects/Database_Migrations/create-database.sql'.
	my_db: Error. (15007, b"'sa' is not a valid login or you do not have permission.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20018, severity 11:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20018, severity 11:\nGeneral SQL Server error: Check messages from the SQL Server\n")

There can be several reasons why the login failed.
One of the reasons is we are trying to connect to a database that does not exist.
If you connect to SQL Server, and you specify a database that does not exist, then you can NEVER login, even as an administrator.

The solution to this problem is to use a *server connection string* (``serverConnString``) with a *script hint* as follows:

.. code-block :: none
	emphasize-lines: 5, 6

	database my_db
	{
		driver: 'sqlserver';
		connString: 'server=myserver.sqlcurrent.com;user=sa;password=sandy;database=my_db;autocommit=1';
		serverConnString: 'server=myserver.sqlcurrent.com;user=sa;password=sandy;autocommit=1'; // server connection string
		create: './create-database.sql' (serverConnString); // script hint
		create: './create-tables.sql';
	}

	create database mydb;

Note how ``serverConnString`` has no database.
The first ``create`` script will use the connection string in ``serverConnString`` instead of the default ``connString``.

Execute ``script.txt`` again.

.. code-block :: none

	% sqlcurrent script.txt

The current script should run successfully with output similar to this:

.. code-block :: none

	my_db: Creating database.
	my_db: Running '/Projects/Database_Migrations/create-database.sql'.
	my_db: Success.
	my_db: Running '/Projects/Database_Migrations/create-tables.sql'.
	my_db: Success.
	my_db: Create database complete.

For more information, see :ref:`creating-databases` and :ref:`script-hints`.

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
