.. _branch:

Branch
========================================================================================================================
A branch associates a database to its versions, allowing you to create and update several databases using a single statement.

.. code-block :: none

	branch operational
	{
		create: 'create.sql';
	}

	database my_db1
	{
		branch: operational;
	}

	database my_db2
	{
		branch: operational;
	}

	version 1.0.1 in branch operational
	{
		apply: 'apply.sql';
	}

	create databases where branch = operational; // Runs create.sql against both my_db1 and my_db2.
	update databases where branch = operational; // Runs apply.sql against both my_db1 and my_db2.

SQL Current implicitly defines a ``default`` branch.
Databases and versions without a ``branch`` property belong to the ``default`` branch.

Examples
-----------------


See Also
-----------------

* :ref:`branch-statement`
* :ref:`database-statement`
* :ref:`version-statement`
