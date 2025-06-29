.. _drivers:

Drivers
===============================================
A database driver code is a property string that specifies which Python database driver / adapter library to use to connect to the database.
SQL Current has general and specific driver codes.
General driver codes, such as ``postgres`` and ``sqlserver``, will select the latest supported Python driver bundled with SQL Current.
Specific driver codes, such as ``psycopg2`` and ``pymssql``, will select an exact version of the Python driver / adapter library.
This also determines the style and format of the connection string (``connString``) you are allowed to use and the parameters that appear in it.  Different database servers use different parameters.

General Driver Codes
------------------------------
* ``influx``
* ``postgres``
* ``postgresql``
* ``mssqlserver``
* ``mssql``
* ``sqlserver``

Specific Driver Codes
------------------------------
* ``psycopg``
* ``psycopg2``
* ``pymssql``

PostgreSQL Driver Codes
------------------------------
* ``postgres``
* ``postgresql``
* ``psycopg``
* ``psycopg2``

SQL Server Driver Codes
------------------------------
* ``mssqlserver``
* ``mssql``
* ``sqlserver``
* ``pymssql``
