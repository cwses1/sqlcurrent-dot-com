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

.. _apply-config-statement-example-1:

**Example 1.** Configure a QA environment database:

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

.. _apply-config-statement-example-2:

**Example 2.** Configure multiple QA environment databases:

::

	database qa_db1
	{
		...
	}

	database qa_db2
	{
		...
	}

	config qa_users
	{
		apply: 'insert_qa_users.sql';
	}

	apply config qa_users to databases;

.. _apply-config-statement-example-3:

**Example 3.** Configure a server:

::

	server qa_server
	{
		...
	}

	config qa_app_logins
	{
		apply: 'create_qa_app_logins.sql';
	}

	apply config qa_app_logins to server qa_server;

.. _apply-config-statement-example-4:

**Example 4**

Configure multiple servers.

::

	server qa_server1
	{
		...
	}

	server qa_server2
	{
		...
	}

	config qa_app_logins
	{
		apply: 'create_qa_app_logins1.sql';
		apply: 'create_qa_app_logins2.sql';
	}

	apply config qa_app_logins to servers where id like 'qa%';

Discussion
-----------------
When you **apply** a configuration to a database or server SQL Current runs every script for the ``apply`` property in the order that it's defined.
Example 4 above contains 2 scripts that presumably configure the application logins.
Those apply scripts are run from top to bottom.

See Also
-----------------
* :ref:`config-statement`
* :ref:`revert-config-statement`
* :ref:`check-config-statement`
* :ref:`precheck-config-statement`
* :ref:`server-statement`
