Databases
=========

=======================
Basic MySQL commands
=======================

::

	$ mysql

	# show all databases 
	mysql> show databases;
	+--------------------+
	| Database           |
	+--------------------+
	| information_schema |
	| test               |
	+--------------------+
	2 rows in set (0.00 sec)

	mysql> use test;
	Database changed
	mysql> show tables;
	+-----------------+
	| Tables_in_test  |
	+-----------------+
	| City            |
	| Country         |
	| CountryLanguage |
	| album           |
	| customer        |
	| item            |
	| numerics        |
	| sale            |
	| track           |
	+-----------------+
	9 rows in set (0.00 sec)

	mysql> 

