.. _environment:

Environment
========================================================================================================================
An **environment** groups databases and servers into a single manageable unit. 
In practice, an environment is one of several isolated areas in an application being developed.
An environment can belong to one or more solutions.
You can think of an environment as another subsection under your solution.

SQL Current implicitly defines a ``default`` environment.
Servers and databases that are defined with no ``environment`` property belong to the ``default`` environment.

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

	server nexus
	{
		environment: dev;
		host: 'nexus.sqlcurrent.com';
	}

	database mydb
	{
		server: nexus;
	}

	create databases where environment = dev;

See Also
-----------------
* :ref:`environment-statement`
