.. _server-statement:

``server``
========================================================================================================================

Defines a server. ::

	database
	{
		branch: topology;
		connString: 'Server=myserver;Database=heavywork_topology111;user=sa;Password=sandy;autocommit=1';
		driver: 'sqlserver';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
		dir: 'heavywork_topology';
		create: 'create_heavywork_topology.sql' (serverConnString);
		create: 'create_heavywork_topology_user.sql';
		reset: 'reset_heavywork_topology.sql' (serverConnString);
	}

``name``
-----------------


Examples
-----------------


See Also
--------------
:ref:`create-server-statement`
