.. _create-script-execution-order:

Create Script Execution Order
==========================================
Database and branch definitions can contain create scripts via the ``create`` property.

Standalone Database Creation
---------------------------------
A **standalone** database is not associated with a branch.
Let's define a standalone database and run the create command:

::

	database standalone_db
	{
		driver: 'sqlserver';
		connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=standalone_db';
		create: '/create1.sql';
		create: '/create2.sql';
	}

	create database standalone_db;

SQL Current will execute the create scripts in the order they are defined.

* ``/create1.sql`` is executed first.
* ``/create2.sql`` is executed second.

Branched Database Creation
---------------------------------
A **branched** database is any database associated with a branch.
We define a branch, a branched database and run a create command in the following script:

::

	branch customer_branch
	{
		create: '/create3.sql';
		create: '/create4.sql';
	}

	database customer_db
	{
		branch: customer_branch;
		driver: 'sqlserver';
		connString: 'Server=myserver;user=sandy;Password=sandy;autocommit=1;Database=customer_db';
		create: '/create1.sql';
		create: '/create2.sql';
	}

	create database customer_db;

SQL Current will execute the create scripts defined in the database first, and the create scripts defined in the branch second.
In the above script, here's exactly what would happen:

* ``/create1.sql`` is executed first.
* ``/create2.sql`` is executed second.
* ``/create3.sql`` is executed third.
* ``/create4.sql`` is executed last.

This is useful for situations where ``customer_db`` has specific creation logic (such as where the database resides on disk).
Branch creation logic applies to all database.
Typically, branch creation logic will create schema objects that appear in all databases.

See Also
---------------------------------
* :ref:`database-statement`
* :ref:`branch-statement`
* :ref:`create-database-statement`
* :ref:`create-databases-statement`
