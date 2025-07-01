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
A physical file containing database verification logic.  Typically, a check script will look for the existence of a table or column.

A check script must return a result set that looks like this:

+-------------------+-------------------+
| error_code        | error_reason      |
+-------------------+-------------------+
| 100               | 'Missing a table' |
+-------------------+-------------------+

See also:

* Error Code
* Error Reason

Config
-----------------------
Custom script logic that is applied to a specific server or database.

For example, you may want to configure the QA environment with a specific set of users for your application.

::

	apply config qa_users to databases where environment = qa;

Create
-----------------------
The act of setting up a database or server for use.
Successful creation of a database implies the database is at 1.0.0.
Successful creation of a server means that the server is configured correctly.

The word "create" in this context can vary based on where your starting point is:

* If the database does not exist then your create scripts must manage the physical setup of the database and the objects within.
* If the database exists then your create scripts only need to manage the objects.
* If the database exists and some of the objects already exist then your create scripts only need to manage the new objects.

SQL Current supports all of these situations.

Note that for a create operation you might not actually be creating anything - you might just be configuring the server or database.
Instead, think of this as a setup and configuration step, especially in the case of servers.

Create Database
-----------------------
The act of setting up a database such that its version is 1.0.0.
A created database can be updated.

Create Server
-----------------------
The act of setting up a server using the :ref:`create-server-statement` or :ref:`create-servers-statement` statement.
Servers are not versioned.

Connection String
-----------------------
The set of parameters used to connect to a database, formatted as a single-line string.
Different databases will use different connection strings.

Database
-----------------------
Contains the schema objects that changes with time.
Databases are versioned.
SQL Current keeps track of each database version.

Database Administrator
-----------------------
Whoever manages the database.
This is commonly abbreviated as DBA.

DBA
-----------------------
Whoever manages the database migrations.
This is short for Database Administrator.

Environment
-----------------------
Associates a server or a database with an isolated segment of your solution.

Init
-----------------------
When you ``init`` a database or server, SQL Current will create the set of opinionated directories where it will look for scripts.

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
A physical file containing database verification logic.
Typically, a precheck script will verify the conditions before an update is run against the database.  This is to avoid errors.

A check script must return a result set that looks like this:

+-------------------+-------------------+
| error_code        | error_reason      |
+-------------------+-------------------+
| 100               | 'Missing a table' |
+-------------------+-------------------+

See also:

* Error Code
* Error Reason

Recreate
-----------------------
The act of resetting a database, then creating it.
This destroys everything and "take you back to square one."

Reset
-----------------------
The act of resetting a database.
This destroys everything and leave your database in a state before it was created.

Revert
-----------------------
The act of undoing a version update.
You may need to revert an update due to a failed deployment.
You can use the :ref:`revert-database-statement` or :ref:`revert-databases-statement` to do this.

Server
-----------------------
A single server may contain several databases.

For more information about servers, see :ref:`server`.

Solution
-----------------------
Groups topology constructs at an application or project level.
A solution may span several environments.

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

For more information see the following:

* :ref:`version`
* :ref:`version-statement`
