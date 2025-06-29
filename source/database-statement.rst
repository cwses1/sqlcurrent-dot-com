.. _database-statement:

``database``
========================================================================================================================
Defines a database.

.. code-block :: none

	database mydb
	{
		create: 'create_script_path.sql';
		branch: topology;
		connString: 'server=myserver;database=mydb;user=sa;password=sandy;autocommit=1';
		dir: './mydb';
		driver: 'sqlserver';
		reset: 'reset_script_path.sql';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
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

If this property is used, it must appear exactly once.

If this property is used, it must reference a defined **branch** and you define a **branched database**.

If this property is not used, you define a **standalone database**.

``connString``
-----------------------
The connection string for this database.

* :ref:`connstring-concept`
* :ref:`postgresql-connstring`
* :ref:`sql-server-connstring`

``create``
-----------------------
The path to the reset file for this database.

You can list this property several times.

``driver``
-----------------------
A code that specifies the Python driver / adapter to use to connect to the database.
The driver code can be general or very specific, and should be easy to guess for users starting out.
This also determines the style and format of the connection string (``connString``) you are allowed to use and the parameters that appear in it.  Different database servers use different parameters.

.. code-block:: none

	database
	{
		driver: 'sqlserver';
	}

For more information, see :ref:`drivers`.

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

Define a standalone PostgreSQL database
*********************

.. code-block :: none

	database postgresqldb
	{
		driver: 'postgresql';
		connString: 'postgresql://postgres:postgres@127.0.0.1/binningtool';
		create: './create.sql';
	}

For more information about working with PostgreSQL databases, see the following:
* :ref:`postgresql-notes`
* :ref:`postgresql-connstring`

Define a standalone SQL Server database
*********************

.. code-block :: none

	database sqlserverdb
	{
		driver: 'sqlserver';
		connString: 'server=myserver;database=mydb;user=sa;password=sandy;autocommit=1';
		create: './create.sql';
	}

For more information about working with SQL Server databases, see the following:
* :ref:`sql-server-notes`
* :ref:`sql-server-connstring`

Define a branched database
*********************

.. code-block :: none

	branch operational
	{
		create: './create_tables.sql';
	}

	database branched_db
	{
		branch: operational;
		connString: 'server=myserver;database=branched_db;user=sa;password=sandy;autocommit=1';
		driver: 'sqlserver';
		create: './create_db.sql';
	}

	version 1.0.1 for branch operational
	{
		apply: './apply_version_1.0.1.sql';
	}

For more information about working with branched databases, see the following:
* :ref:`branch-concept`
* :ref:`branch-statement`
* :ref:`creating-databases`
