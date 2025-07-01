.. _version:

Version
========================================================================================================================
A set of script

A version always belongs to a branch.


Creating
--------------
In a SQL Current context, creating a server means initializing the server for use.
You would normally "create" a server before creating databases in the server.

To create a server, you use the ``create`` property to specify one or more server create scripts.
Then you create the server using the :ref:`create-server-statement` or the :ref:`create-servers-statement`.

.. code-block :: none

	server my_server
	{
		driver: 'postgres';
		connString: 'postgresql://postgres:postgres@127.0.0.1';
		create: './create.sql';
	}

	create server my_server; // Runs the create.sql script, which might create users, roles, logins, databases, etc.

For more information see the following:

* :ref:`creating-servers`
* :ref:`server-statement`
* :ref:`create-server-statement`
* :ref:`create-servers-statement`

Checking
--------------
You can run check scripts against a server to make sure the server is in the correct state.
This can be very helpful to ensure your server create scripts were successful, and to detect changes or misconfigurations later.

.. code-block :: none

	server my_server
	{
		driver: 'postgres';
		connString: 'postgresql://postgres:postgres@127.0.0.1';
		create: './create.sql';
		check: './check.sql';
	}

	check server my_server;

For more information see the following:

* :ref:`check-scripts`
* :ref:`server-statement`
* :ref:`check-server-statement`
* :ref:`check-servers-statement`

Resetting
--------------
Resetting a server puts the server into a pre-create state.
It effectively "undoes" whatever the create scripts do.
If you follow this practice, you should be able to run a ``reset server``, then a ``create server`` statement against the same server without errors.

To reset a server, you use the ``reset`` property to specify one or more server reset scripts.
Then you reset the server using the :ref:`reset-server-statement` or the :ref:`reset-servers-statement`.

.. code-block :: none

	server my_server
	{
		driver: 'postgres';
		connString: 'postgresql://postgres:postgres@127.0.0.1';
		create: './create.sql';
		reset: './reset.sql';
	}

	reset server my_server;

For more information see the following:

* :ref:`server-statement`
* :ref:`reset-server-statement`
* :ref:`reset-servers-statement`

Recreating
--------------
Recreating a server is a reset followed by a create.

The following script

.. code-block :: none

	recreate server my_server;

is shorthand for, and will do the exact same thing as this script:

.. code-block :: none

	reset server my_server;
	create server my_server;

See Also
--------------

* :ref:`creating-servers`
* :ref:`drivers`
* :ref:`paths`
* :ref:`server-statement`
* :ref:`create-server-statement`
* :ref:`create-servers-statement`
* :ref:`check-server-statement`
* :ref:`check-servers-statement`
* :ref:`reset-server-statement`
* :ref:`reset-servers-statement`
