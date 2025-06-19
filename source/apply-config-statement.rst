.. _apply-config-statement:

``apply config``
========================================================================================================================

Summary
-----------------
Applies a configuration to one or more databases or servers.
This statement has several forms.

Syntax Overview
-----------------

Apply a configuration to a single, named database:

::

	apply config <config_symbol_name> to database <database_symbol_name>;

Apply a configuration to a single, named server:

::

	apply config <config_symbol_name> to server <server_symbol_name>;

Apply a configuration to a set of databases:

::

	apply config <config_symbol_name> to databases where ... order by ...

Apply a configuration to a set of servers:

::

	apply config <config_symbol_name> to servers where ... order by ...

Examples
-----------------

::

	database qa_db
	{
		...
	}

	config qa_users
	{
		apply: 'insert_qa_users.sql';
	}

	apply config qa_users to database qa_db;

Discussion
-----------------


See Also
-----------------
:ref:`revert-config-statement`
