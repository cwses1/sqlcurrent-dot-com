.. _recreate-database-statement:

``recreate database``
========================================================================================================================
Resets, then creates a database or server.

.. warning::
	This is a very powerful command that completely obliterates everything in a database.
	
	You should probably never use this in production.


Syntax
-----------------

::
	
	recreate database mydb;

::
	
	recreate server nexus;

Examples
-----------------
::
	
	database
	{
		driver: 'postgres';
		connString: 'Server=myserver;Database=mydb;user=postgres;Password=postgres';
		create: 'create.sql';
		reset: 'reset.sql';
	}

	recreate database mydb;



See Also
-----------------
* :ref:`create-database-statement`
* :ref:`create-databases-statement`
* :ref:`recreate-databases-statement`
* :ref:`reset-database-statement`
* :ref:`reset-databases-statement`
