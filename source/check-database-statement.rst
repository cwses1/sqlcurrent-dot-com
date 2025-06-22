.. _check-database-statement:

``check database``
========================================================================================================================
Runs check scripts against the specified database.

Syntax Overview
-----------------

Run all check scripts connected to the specified database:

::

	check database <database_symbol>;


Run check scripts for a specific version of the database:

::

	check database <database_symbol> version <version_number>;


Examples
-----------------

Define a standalone database, create the database, then check the database to ensure creation was successful:

::

	database mydb
	{
		driver: '...';
		connString: '...';
		create: 'create.sql';
		check: 'check.sql';
	}

	create database mydb;
	check database mydb;

See Also
-----------------
* :ref:`check-databases-statement`
* :ref:`check-server-statement`
* :ref:`check-servers-statement`
