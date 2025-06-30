.. _server-statement:

``server`` Statement
========================================================================================================================
Defines a server.

.. code-block :: none

	server my_server
	{
		connString: 'Server=my_server;Database=my_db;user=sa;Password=sandy;autocommit=1';
		create: 'create.sql';
		dir: 'my_server';
		driver: 'sqlserver';
		environment: dev;
		host: 'my_server.sqlcurrent.com';
		reset: 'reset.sql' (serverConnString);
	}

See the following for more information:

* :ref:`server-concept`

``connString``
-----------------
The connection string to the server.

See the following for more information:

* :ref:`connstring-concept`

``create``
-----------------
The path to the server create script.
*Creating* a server means to initialize the server for use.
You might create logins or other prerequisities that the server's databases might need.

See the following for more information:

* :ref:`paths`
* :ref:`create-server-statement`
* :ref:`create-servers-statement`

``dir``
-----------------
The directory that SQL Current starts in to find scripts.

See :ref:`paths` for more information.

``driver``
-----------------
The Python driver / adapter library to use to connect to the server.

See the following for more information:

* :ref:`drivers`

``environment``
-----------------
The environment to which this server belongs.
If this property is not specified then the server will belong to the implicitly-defined ``default`` environment.

See the following for more information:

* :ref:`environments`
* :ref:`environment-statement`

``host``
-----------------
The IP address or resolveable host name of the server.
The ``host`` property may appear redundant since there is already a connection string (``connString``) property, but this is used for construction database connection strings for individual databases.

.. code-block :: none

	server my_server
	{
		host: 'my_server.sqlcurrent.com';
	}

	database my_db1
	{
		connString: 'server={{my_server.host}};database=my_db1;user';
		...
	}

	database my_db2
	{
		connString: 'server={{my_server.host}};database=my_db2;user';
		...
	}

In the above example both ``my_db1`` and ``my_db2`` use the ``host`` property of ``my_server`` in their respective connection string properties.
If the location of ``my_server`` changes then you only need to update the ``host`` property of that server.

``reset``
-----------------
The path to the server reset script.
*Resetting* a server puts the server in a *precreate state* such that you can run the create script against the server again.
You might create logins or other prerequisities that the server's databases might need.

See the following for more information:

* :ref:`paths`
* :ref:`reset-server-statement`
* :ref:`reset-servers-statement`

Examples
-----------------
Define a server with a single create script.
Note how the connection string does not contain a database or schema name.
This is intentional.

::

	server my_server
	{
		driver: 'sqlserver';
		connString: 'Server=my_server;user=sa;Password=sandy;autocommit=1';
		create: './create.sql';
	}

See the following for more information:

* :ref:`creating-databases`


See Also
--------------

* :ref:`create-server-statement`
* :ref:`create-servers-statement`
* :ref:`reset-server-statement`
* :ref:`reset-servers-statement`
* :ref:`check-server-statement`
* :ref:`check-servers-statement`
* :ref:`paths`
* :ref:`drivers`
