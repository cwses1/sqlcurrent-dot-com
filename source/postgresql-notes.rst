.. _postgresql-notes:

PostgreSQL Notes
=================================
Psycopg 3 is the default driver for PostgreSQL.

::

	database postgres_server
	{
		driver: 'postgres'; // Uses the psycopg3 driver.
		connString: 'postgresql://postgres:postgres@127.0.0.1/my_pg_db';
		// ...
	}

SQL Current also supports psycopg2.  If you want to use the psycopg2 driver you must explicitly specify it as follows:

::

	database postgres_server
	{
		driver: 'psycopg2'; // Uses the psycopg2 driver.
		connString: 'postgresql://postgres:postgres@127.0.0.1/my_pg_db';
		// ...
	}

Both the psycopg3 and the psycopg2 drivers define their own connection string format, which SQL Current passes directly to the driver.
SQL Current does not define its own connection string format for PostgreSQL.

Connection String Format
---------------------------------
This is documented here:

https://www.psycopg.org/psycopg3/docs/api/connections.html#psycopg.Connection.connect

and the complete list of parameter keywords is listed here:

https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-PARAMKEYWORDS

Examples
---------------------------------

Define a PostgreSQL database.

::

	database mydb
	{
		driver: 'sqlserver';
		connString: 'postgresql://postgres:postgres@127.0.0.1/mydb';
		// ...
	}

See Also
---------------------------------
* :ref:`database-statement`
* https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-PARAMKEYWORDS
* https://www.psycopg.org/psycopg3/docs/api/connections.html#psycopg.Connection.connect
