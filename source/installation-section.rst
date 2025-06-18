.. _setup-section:

Setup / Install
========================================================================================================================

Install Python
---------------------------------------------

SQL Current is written in Python.  You will need to get Python.

https://www.python.org

Clone sqlcurrent Repo
---------------------------------------------
::

	git clone https://github.com/cwses1/sqlcurrent.git


Install ANTLR Python Runtime
---------------------------------------------
::

	pip install antlr4-python3-runtime

Install Python Database Drivers / Adapters
---------------------------------------------

::

	pip install psycopg
	pip install pymssql

SQL Current is now installed.  The next step is to test it.

Test
---------------------------------------------
Open a shell / console / terminal in a directory and ensure your computer can find the sqlcurrent command: ::

	% sqlcurrent

You should see output like this: ::

	USAGE:
	sqlcurrent <file>

You are now ready to move on to the :ref:`tutorial-section`.
