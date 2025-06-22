.. _script-hints:

Script Hints
=================================
A script hint instructs SQL Current to use a different connection string when running a database script.
This can be very useful for executing database scripts that require different credentials or parameters, such as create and reset scripts.

Example
---------------------------------
When SQL Current runs the following create command, it will use the ``connString`` of ``myserver``.

.. code-block:: none
	:linenos:
	:emphasize-lines: 4,11

	server myserver
	{
		driver: 'sqlserver';
		connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1';
	}

	database mydb
	{
		driver: 'sqlserver';
		connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=mydb';
		create: '/create.sql' (myserver);
	}

	version 1.0.1
	{
		apply: '/apply.sql';
	}

	create database mydb;

This is useful because the default connection string ``connString`` specifies the database, and if that database does not exist then any login to the server will fail.
Use a script hint to avoid the problem.

See Also
---------------------------------
:ref:`creating-databases`
