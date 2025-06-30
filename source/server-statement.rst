.. _server-statement:

``server``
========================================================================================================================
Defines a server.

.. code-block :: none

	server my_server
	{
		connString: 'Server=my_server;Database=my_db;user=sa;Password=sandy;autocommit=1';
		create: 'create.sql';
		dir: 'my_server';
		driver: 'sqlserver';
		reset: 'reset.sql' (serverConnString);
	}

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
