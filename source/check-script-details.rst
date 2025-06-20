.. _check-script-details:

Check Scripts
========================================================================================================================
A check script is something you write as the DBA to verify a create, update, or apply config operation completed successfully.
There are two types of check scripts:

* Check
* Precheck

A **check** script should be run after an update or apply operation.  It verifies the operation was successful.
A **precheck** script should be run before an update or apply operation.  It verifies that the database is ready for the operation.

A check script returns a single-row result set that looks like this:

+-------------------+-------------------+
| error_code        | error_reason      |
+-------------------+-------------------+
| int               | varchar(1024)     |
+-------------------+-------------------+

A successful check script returns a result set where the ``error_code`` value is 0.
If the error code is 0, then the check will pass and SQL Current will continue.

+-------------------+-------------------+
| error_code        | error_reason      |
+-------------------+-------------------+
| 0                 | ''                |
+-------------------+-------------------+

A failed check script returns a result set where the ``error_code`` value is greater than 0.
If the error code is great than 0, then the check will fail and SQL Current will stop and report the failed check.=

+-------------------+-------------------+
| error_code        | error_reason      |
+-------------------+-------------------+
| 100               | 'Missing a table' |
+-------------------+-------------------+

A successful check script written in T-SQL might look like this:

::

	select 0 as error_code, 'Test check failure 1.' as error_reason;

A failed check script written in T-SQL might look like this:

::

	select 100 as error_code, 'Missing a table.' as error_reason;

Your scripts must be written to work with the target database server.

See Also
-----------------
* :ref:`check-config-statement`
* :ref:`check-database-statement`
* :ref:`check-databases-statement`
* :ref:`check-server-statement`
* :ref:`check-servers-statement`
* Error Code
* Error Reason
