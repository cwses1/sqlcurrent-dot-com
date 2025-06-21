.. _sql-server-notes:

SQL Server Notes
=================================
The pymssql driver does not accept a connection string.
It only accepts individual parameters for connections.
There are several parameters for a SQL Server connection, and SQL Current supports all of them.
pymsql parameters has its own format

Connection String Format
---------------------------------
``server=192.168.10.170;database=mydb;user=sa;password=sandy;autocommit=1``

``server``
*********************************

``database``
*********************************

``user``
*********************************

``password``
*********************************

``autocommit``
*********************************

Examples
---------------------------------

Define a SQL Server database.

::

	database sqlserver
	{
		driver: 'sqlserver';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
		connString: 'Server=192.168.10.170;Database=heavywork_topology111;user=sa;Password=sandy;autocommit=1';
		// ...
	}

Creating the Physical Database
---------------------------------



See Also
---------------------------------
* :ref:`database-statement`
