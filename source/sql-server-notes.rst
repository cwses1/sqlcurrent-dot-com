.. _sql-server-notes:

SQL Server Notes
=================================

Connection String Notes
---------------------------------
The ``pymssql`` driver does not accept a connection string.
It only accepts individual parameters for connections:

::

	pymssql.connect(server, user, password, database_name)

There are several parameters for a SQL Server connection, and SQL Current supports all of them.

Connection String Format
---------------------------------
For SQL Server, SQL Current uses the same connection string format as ADO.NET:

::

	param1=value1;param2=value2;...param_n=value_n;

Parameter value pairs are separated using the ``=`` character and terminated with a ``;`` character.
Here is an example of a connection string you can use with SQL Server:

::

	server=angelfire.sqlcurrent.com;database=mydb;user=sa;password=sandy;autocommit=1

The parameter names (server, database, user, password, autocommit) are NOT case-sensitive, but the values are.
Here are the most common connection string parameters used when connecting to SQL Server.

``server``
*********************************
The host name or IP address of the SQL Server.

::

	database mydb
	{
		connString: 'Server=192.168.10.170;Database=mydb;user=sqlserver_login;Password=sqlserver_password;autocommit=1';
	}

``database``
*********************************
The name of the database.

``user``
*********************************
For SQL Server authentication, the SQL Server login.

``password``
*********************************
For SQL Server authentication, the SQL Server password.

``autocommit``
*********************************
If you are adding new tables or doing any sort of DDL, then you will almost certainly want to turn ``autocommit`` on.
DDL statements cannot appear in a transaction.
Set this parameter to a ``True`` value (``1``, ``True``, ``y``, ``t``) to turn this on.

Examples
---------------------------------
Example 1.  Define a SQL Server database.

::

	database sqlserver
	{
		driver: 'sqlserver';
		serverConnString: 'server=192.168.10.170;user=sa;password=sandy;autocommit=1';
		connString: 'Server=192.168.10.170;Database=heavywork_topology111;user=sa;Password=sandy;autocommit=1';
		// ...
	}

See Also
---------------------------------
* :ref:`sql-server-connstring`
* :ref:`creating-databases`
* :ref:`database-statement`
* https://pymssql.readthedocs.io/en/latest/index.html
