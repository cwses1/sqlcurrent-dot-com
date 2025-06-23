.. _environment-statement:

``environment``
========================================================================================================================
Defines an environment.

::

	environment dev
	{
		name: 'Development Environment';
		solution: <solution_symbol_name>;
		solution: iot_app;
	}

``name``
-----------------
The name of the environment.

``solution``
-----------------
The solution the environment belongs to.
An environment can belong to one or more solutions.


Examples
-----------------

::

	solution cloud_app
	{
		name: 'Cloud Application';
	}

	environment dev
	{
		name: 'Development Environment';
		solution: cloud_app;
	}


Discussion
-----------------
An environment can belong to one or more solutions.
Like a solution, an environment groups databases and servers into a single manageable unit.

See Also
-----------------
* :ref:`solution-statement`
* :ref:`environment-concept`
