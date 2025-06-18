.. _database-statement:

``database``
========================================================================================================================

Defines a database. ::

	database
	{
		:ref:`database-statement-branch`:
		branch: topology;
		
		connString: 'Server=myserver;Database=heavywork_topology111;user=sa;Password=sandy;autocommit=1';
		driver: 'sqlserver';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
		dir: 'heavywork_topology';
		create: 'create_heavywork_topology.sql' (serverConnString);
		create: 'create_heavywork_topology_user.sql';
		reset: 'reset_heavywork_topology.sql' (serverConnString);
	}

.. _database-statement-branch:

``branch``
-----------------------
The branch this database belongs to.

::

	database
	{
		branch: topology;
	}

A database that belongs to a branch is a **branched database**.  Otherwise, it is a **standalone database**.  See :ref:`concepts-section` for more information.

This property is optional.

If used, this property can appear exactly once.

.. _database-statement-connString:

``connString``
-----------------------
The connection string for this database.

.. _database-statement-create:

``create``
-----------------------
The path to the reset file for this database.

You can list this property several times.

``driver``
-----------------------
A code that specifies the Python driver / adapter to use to connect to the database.  The driver code can be general or very specific, and should be easy to guess for users starting out.
::
	database
	{
		driver: 'sqlserver';
	}

General Driver Codes
************
* ``postgres``
* ``postgresql``
* ``sqlserver``
* ``mssqlserver``
* ``mssql``
* ``influx``

Specific Driver Codes
************
* ``psycopg2``
* ``pymssql``

This also determines the style and format of the connection string (``connString``) you are allowed to use and the parameters that appear in it.  Different database servers use different parameters.

``dir``
-----------------------
The directory that contains scripts for this database.

You can use this property once.

``reset``
-----------------------
The path to the reset file for this database.

You can list this property several times.

``serverConnString``
-----------------------
A special connection string 

You can use this property once.



Examples
-----------------------

Simple Database Definition
*********************
::

	database
	{
		branch: topology;
		connString: 'Server=192.168.10.170;Database=heavywork_topology111;user=sa;Password=sandy;autocommit=1';
		driver: 'sqlserver';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
		dir: 'heavywork_topology';
		create: 'create_heavywork_topology.sql' (serverConnString);
		create: 'create_heavywork_topology_user.sql';
		reset: 'reset_heavywork_topology.sql' (serverConnString);
	}



Database in a branch with 
*********************
::

	database
	{
		branch: topology;
		connString: 'Server=192.168.10.170;Database=heavywork_topology111;user=sa;Password=sandy;autocommit=1';
		driver: 'sqlserver';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
		dir: 'heavywork_topology';
		create: 'create_heavywork_topology.sql' (serverConnString);
		create: 'create_heavywork_topology_user.sql';
		reset: 'reset_heavywork_topology.sql' (serverConnString);
	}
