.. _getting-started-section:

Getting Started
===============================================



Open a shell / console / terminal in a directory and ensure your computer can find the sqlcurrent command: ::

	% sqlcurrent

You should see output like this: ::

	USAGE:
	sqlcurrent <file>

Create A Script File
-----------------------

This example script creates objects in a PostgreSQL database. ::

	database mydb
	{
		driver: 'postgres';
		connString: 'host=127.0.0.1 port=5432 dbname=mydb user=postgres password=postgres';
		create: './create.sql';

	}

	create database mydb;

Run The Script
-----------------------

Run the following command in your shell / console / terminal: ::

	% sqlcurrent script.txt

Congratulations!  You have run your very first script.
