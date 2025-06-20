.. _check-config-statement:

``check config``
========================================================================================================================
Verifies the configuration of a database or server by running the check scripts associated with the config.

::

	check config <config_symbol_name> against database <database_symbol_name>;

::

	check config <config_symbol_name> against databases where ... order by ...;

::

	check config <config_symbol_name> against server <server_symbol_name>;

::

	check config <config_symbol_name> against servers where ... order by ...;

Examples
-----------------

**Example 1.** Check the configuration of the QA database qa_db.

::

	database qa_db
	{
		...
	}

	config qa_users
	{
		apply: 'insert_qa_users.sql';
	}

	check config qa_users against database qa_db;

**Example 2.** Check the configuration of multiple QA databases.

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
		check: 'check_qa_users.sql';
	}

	check config qa_users against databases;

**Example 3.** Check the configuration of a server.

::

	server qa_server
	{
		...
	}

	config qa_app_logins
	{
		check: 'check_qa_app_logins.sql';
	}

	check config qa_app_logins against server qa_server;

**Example 4.** Check the configuration of multiple servers.

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
		check: 'check_qa_app_logins1.sql';
		check: 'check_qa_app_logins2.sql';
	}

	check config qa_app_logins against servers where id like 'qa%';

Discussion
-----------------

See Also
-----------------
* :ref:`config-statement`
* :ref:`apply-config-statement`
* :ref:`precheck-config-statement`
* :ref:`server-statement`
