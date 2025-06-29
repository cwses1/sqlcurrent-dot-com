.. _opinionated-paths:

Opinationed Paths
========================================================================================================================
If you do not specify a ``dir`` field in a definition statement, and you do not specify a relative path in for a ``precheck``, ``check``, ``apply`` or ``revert`` script property, then SQL Current will look for the script in the **opinionated** directory.
For example, if you define this database:

::

	database dev_db
	{
		create: 'create.sql';
	}

and run this command:

::

	create dev_db;

then SQL Current will look for ``create.sql`` here:

``./sqlcurrent_sqlscripts/standalone/create/create.sql``


Examples
-----------------


See Also
-----------------
