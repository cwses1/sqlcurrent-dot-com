.. _script-hints:

Script Hints
=================================
A script hint tells SQL Current to use a a different connection string when running a specific script.
This can be very useful for any operation that may require different credentials or parameters, such as create or reset.

Example
---------------------------------
In the following example, when SQL Current runs the create script, it will use the ``connString`` of ``myserver``.

.. code-block:: none
	:linenos:
	:emphasize-lines: 11

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


See Also
---------------------------------
:ref:`creating-databases`
