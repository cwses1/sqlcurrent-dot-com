.. _config-statement:

``config``
========================================================================================================================
Defines a configuration.
Configurations are additional, arbitrary scripts you can apply to a database or a server.

::

	config qa_users_config
	{
		name: 'QA Users Configuration';
		dir: '/';
		precheck: 'precheck.sql';
		apply: 'apply.sql';
		revert: 'revert.sql';
		check: 'check1.sql';
	}

``name``
-----------------
A friendly name for the configuration.

This property is optional.

``dir``
-----------------
The directory where the script files reside.

This property is optional.
If this property is not used, then the **opinionated** directory is used.  See :ref:`opinionated-paths`.

``precheck``
-----------------
A path to a precheck script.

This property is optional.
You can specify this property any number of times.
The scripts will be run in the order they are specified in the definition.

``apply``
-----------------
A path to an apply script.

This property is optional.
You can specify this property any number of times.
The scripts will be run in the order they are specified in the definition.


``check``
-----------------
A path to a check script.

This property is optional.
You can specify this property any number of times.
The scripts will be run in the order they are specified in the definition.

``revert``
-----------------
A path to a revert script.

This property is optional.
You can specify this property any number of times.
The scripts will be run in the order they are specified in the definition.

Discussion
-----------------


Examples
-----------------


See Also
-----------------
* :ref:`apply-config-statement`
* :ref:`check-config-statement`
* :ref:`precheck-config-statement`
* :ref:`revert-config-statement`
* :ref:`opinionated-paths`
