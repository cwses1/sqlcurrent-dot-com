.. _branch-statement:

``branch``
========================================================================================================================
Defines a branch.
A branch associates a database with versions.
For more information, see :ref:`branch-concept`.

Syntax Overview
-----------------

::

	branch operational
	{
		name: 'operational';
		desc: 'Databases in this branch hold a certain type of database'
		create: 'create.sql';
		reset: 'reset.sql';
		check: 'check.sql';
		dir:
	}

``name``
-----------------

``desc``
-----------------

``create``
-----------------

``reset``
-----------------

``check``
-----------------

``dir``
-----------------

Examples
-----------------

::

	branch operational
	{
		name: 'Operational Branch';
		desc: 'Databases in this branch have a similar schema and hold operational data.'
		create: 'create.sql';
		reset: 'reset.sql';
		check: 'check.sql';
		dir: 'operational_branch';
	}

	branch analytical
	{
		name: 'Analytical Branch';
		desc: 'Databases in this branch are indexed for reporting and analytics.'
		create: 'create.sql';
		reset: 'reset.sql';
		check: 'check.sql';
		dir: 'analytical_branch';
	}

	database op_db1
	{
		branch: operational;
		...
	}

	database op_db2
	{
		branch: operational;
		...
	}

	database report_db1
	{
		branch: analytical;
		...
	}

	database report_db2
	{
		branch: analytical;
		...
	}

	create databases;


See Also
-----------------
