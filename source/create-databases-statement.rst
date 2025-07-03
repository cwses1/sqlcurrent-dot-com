.. _create-databases-statement:

``create databases``
========================================================================================================================
Executes database create scripts for the specified set of databases.

Syntax Overview
-----------------

.. code-block :: none

	create databases [in branch <branch_name>]
	[where <whereClause>] 
	[order by <orderByClause>]
	;


Examples

Create databases only in the specified branch:

.. code-block :: none

	create databases;

-----------------
Create every database across all solutions and environments.
This is an extremely powerful command.
Very rarely would you do this.

.. code-block :: none

	create databases;

See Also
-----------------
* :ref:`creating-databases`
* :ref:`creating-servers`
* :ref:`create-database-statement`
