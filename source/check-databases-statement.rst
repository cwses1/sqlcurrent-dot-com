.. _check-databases-statement:

``check databases``
========================================================================================================================
Runs check scripts against the specified databases.

Syntax Overview
-----------------

::

	check databases where ... order by ...;


Examples
-----------------

Define two (2) standalone databases, create the databases, and run check scripts against both of them to ensure creation was successful.

::

	database mydb1
	{
		driver: '...';
		connString: '...';
		check: 'check1.sql';
	}

	database mydb2
	{
		driver: '...';
		connString: '...';
		check: 'check2.sql';
	}

	create databases;
	check databases;

See Also
-----------------
* :ref:`check-databases-statement`
* :ref:`check-server-statement`
* :ref:`check-servers-statement`
