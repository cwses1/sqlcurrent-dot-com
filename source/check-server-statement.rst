.. _check-server-statement:

``check server``
========================================================================================================================
Runs check scripts against the specified server.

Syntax Overview
-----------------

::

	check server <server_symbol_name>;


Examples
-----------------

Runs the check script ``check.sql`` against the server to ensure the server is configured correctly.

::

	server nexus
	{
		check: 'check.sql';
	}

	check server nexus;


See Also
-----------------
* :ref:`check-database-statement`
* :ref:`check-databases-statement`
* :ref:`check-servers-statement`
* :ref:`check-script-details`
