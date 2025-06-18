.. _concepts-section:

Concepts
===============================================

Apply
-----------------------
The act of updating a database to a newer version.

Apply Script
-----------------------
A physical file that contains database-specific instructions.

For PostgreSQL, this could be SQL.
For Microsoft SQL Server, this could be SQL or T-SQL.

Branch
-----------------------
Associates a set of databases and versions.
Databases in the same branch receive the same version updates.
This allows the DBA to perform migrations to several databases in a single command.

Branched Database
-----------------------
A database that belongs to a branch.
Databases in the same branch get the same version updates.

Branching
-----------------------
A technique used to associate a set databases to their versions.
This allows the DBA to perform migrations to several databases in a single command.

Check
-----------------------
The act of running a check script **after** a version has been applied and reporting if the logic passed or failed.

The purpose of a check is to verify that the database has the objects and/or data it's supposed to.

A check script returns an error code and an error reason.  This makes it easy for the DBA.

See also:
* Error Code
* Error Reason

Check Script
-----------------------

See also:
* Error Code
* Error Reason


Config
-----------------------

Create
-----------------------
The act of setting up or initialization a database or server for use.
Successful creation of a database implies the database is at 1.0.0.
Successful creation of a server means that the server is configured correctly.

Create Database
-----------------------
The act of setting up a database such that its version is 1.0.0.
A created database can be updated.

Create Server
-----------------------
The act of setting up a server using the :ref:`create-server-statement` ``create server`` or ``create servers`` statement.
Servers are not versioned.


Connection String
-----------------------
The set of parameters used to connect to a database, formatted as a single-line string.
Different databases will use different connection strings.

Database
-----------------------

A single server may contain several databases.

Database Administrator
-----------------------
Whoever manages the database.

This is commonly abbreviated as DBA.

DBA
-----------------------
Database Administrator

Environment
-----------------------
Associates a server or a database with 

Init
-----------------------

Opinionated Path
-----------------------
This is the directory and file system structure that SQL Current follows when the ``dir`` property is not specified.

Precheck
-----------------------
The act of running a check script **before** a version has been applied.

The purpose of a precheck is to verify that the database is ready to accept the next version.  If something is missing, then the precheck should fail.

A precheck script returns an error code and an error reason.  This makes it easy for the DBA.

See also:
* Error Code
* Error Reason
* Check
* Check Script

Precheck Script
-----------------------

Recreate
-----------------------

Reset
-----------------------

Revert
-----------------------

Server
-----------------------
A single server may contain several databases.

.. _concept-solution:

Solution
-----------------------
Associates topology constructs at an application level.
An application may have several environments.

Standalone Database
-----------------------
A database that does not explicitly belong to a branch.

Tag
-----------------------
Associates additional, metadata to a topology item.
For example, a database may physically be located in the United States.

Topology
-----------------------
How the set of databases, servers, branches, versions, etc. are related to each other and how they are permitted change.

Update
-----------------------
The act of applying a version to a database.

Update Tracking File
-----------------------
A physical file that SQL Current manages for each database.  It contains the history of updates and reverts.  Used to determine the current version of the database.

Version
-----------------------
The state of a database such that it complies with the business requirements.
A certain version of a database may have a table or specific data that previous versions don't have.
Versions are semantic and follow the ``major.minor.patch`` pattern.
