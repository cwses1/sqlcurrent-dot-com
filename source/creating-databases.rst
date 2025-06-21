.. _creating-databases:

Creating Databases
=================================

Summary 
---------------------------------
How to create a database that does not exist initially.
We also cover the execution order of create scripts for both branched and standalone databases.

Create Database Problem
---------------------------------
Suppose we have the following database definition:

::

	database mydb
	{
			driver: 'sqlserver';
			connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=mydb';
			create: '/create.sql';
	}

We would like to create this database, so we run this command:

::

	create database mydb;

But we get an error with output that looks like this:

::

	mydb: Creating database.
	mydb: Running '/create.sql'.
	mydb: Error. (18456, b"Login failed for user 'sandy'.DB-Lib error message 20018, severity 14:\nGeneral SQL Server error: Check messages from the SQL Server\nDB-Lib error message 20002, severity 9:\nAdaptive Server connection failed (192.168.10.170)\nDB-Lib error message 20002, severity 9:\nAdaptive Server connection failed (192.168.10.170)\n")

Here we get a general ``Login failed for user 'sandy'`` error, which is not very descriptive.
This could be caused by several factors, one of which is the database does not exist.
If the database does not exist then you will NEVER be able to log in, especially in the case of SQL Server.
The solution is to remove the ``Database`` parameter from the connection string.
You will then be able to create the database.
However, this causes another problem - you won't be able to update your database later because the database parameter was removed.

The SQL Current solution to this is to use a **server connection string** and a **script hint**, which is a connection string that does not have a database parameter.
You effectively end up defining multiple connection strings for the database.
SQL Current provides two options for this.

**Solution 1**
Define property ``serverConnString`` directly in the database definition and add a script hint:

::

	database mydb
	{
			driver: 'sqlserver';
			connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=mydb';

			//
			// INTRODUCE serverConnString
			//
			serverConnString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=mydb';

			//
			// ADD A SCRIPT HINT IN PARENTHESIS AFTER THE SCRIPT PATH.
			//
			create: '/create.sql' (serverConnString);
	}

SQL Current will use the connection string in the ``serverConnString`` for each hinted script.
Otherwise, ``connString`` will be used.

**Solution 2**

Define a server and add a script hint to the create property:

::

	server myserver
	{
		driver: 'sqlserver';
		connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=mydb';
	}

	database mydb
	{
			driver: 'sqlserver';
			connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=mydb';
			create: '/create.sql' (myserver);
	}

SQL Current will use the ``myserver`` connection string for the script defined by ``create``.

See Also
---------------------------------
* :ref:`create-database-statement`
* :ref:`create-databases-statement`
* :ref:`database-statement`
