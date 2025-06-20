.. _solution-statement:

``solution``
========================================================================================================================
Defines a solution, which groups several servers, databases, and environments into a single, manageable unit.

Syntax Overview
-----------------

::

	solution <solution_symbol_name>
	{
		name: 'IoT Application';
	}


``name``
-----------------
A friendly name for the solution.


Examples
-----------------

The following example defines two (2) solutions and one server per solution.

::

	solution iot_app
	{
		name: 'IoT Application';
	}

	solution cloud_app
	{
		name: 'Cloud Application';
	}

	server nexus
	{
		host: 'nexus.sqlcurrent.com';
		solution: cloud_app;
		check: '...';
	}

	server proxima
	{
		host: 'proxima.sqlcurrent.com';
		solution: iot_app;
		check: '...';
	}

	check servers where solution = iot_app; // Run check scripts against servers in the iot_app solution only.

	check servers where solution = cloud_app; // Run check scripts against servers in the cloud_app solution only.

	check servers; // Run check scripts all servers regardless of solution.


See Also
-----------------
* :ref:`concept-solution`
* :ref:`database-statement`
* :ref:`environment-statement`
* :ref:`server-statement`
