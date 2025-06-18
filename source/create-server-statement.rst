.. _create-server-statement:

``create server``
========================================================================================================================

Executes the create scripts listed in the server definition. ::

	server nexus
	{
		driver: 'postgres';
		connString: 'Server=nexus;Database=my_database;user=my_user_id;Password=my_password';
		create: 'create1.sql';
		create: 'create2.sql';
	}

	create server nexus;

See Also
--------------
:ref:`server-statement`
