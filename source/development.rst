Development
===========

==========
Angular.JS
==========

Create an application:

::

    (function(){
      var app = angular.module('store', []);
    })();
    
**Controllers** help us to get data on to the page. Controllers are where we
define our app's behavior by defining functions and values.

::

    var app = angular.module('store', []);
    
    var gem = {
      'name': 'Blablabla',
      'price': 2.95,
      'description': '...',
      'canPurchase': false
    }
    app.controller('StoreController', function(){
      this.product = gem;  // product is a property of our controller
    })

::

    <div ng-controller="StoreController as store">
      <h1>{{ store.product.name }}</h1>
      <h2>{{ store.product.price }}</h2>
      <p>{{ store.product.description }}</p>
      <button ng-show="store.product.canPurchase">Add to cart</button>
    </div>

=======================
Basic MySQL commands
=======================

::

    $ mysql

    # show all databases 
    mysql> SHOW DATABASES;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | test               |
    +--------------------+
    2 rows in set (0.00 sec)

    mysql> use test;
    Database changed
    mysql> SHOW TABLES;
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

    mysql> CREATE DATABASE sales;
    mysql> DROP DATABASE sales;

    # get table structure
    mysql> DESCRIBE City;
    +-------------+----------+------+-----+---------+----------------+
    | Field       | Type     | Null | Key | Default | Extra          |
    +-------------+----------+------+-----+---------+----------------+
    | ID          | int(11)  | NO   | PRI | NULL    | auto_increment |
    | Name        | char(35) | NO   |     |         |                |
    | CountryCode | char(3)  | NO   |     |         |                |
    | District    | char(20) | NO   |     |         |                |
    | Population  | int(11)  | NO   |     | 0       |                |
    +-------------+----------+------+-----+---------+----------------+
    5 rows in set (0.00 sec)

    # count all the rows from table
    mysql> SELECT COUNT(*) FROM Country;
    +----------+
    | COUNT(*) |
    +----------+
    |      239 |
    +----------+
    1 row in set (0.01 sec)

    mysql> SELECT CONCAT("Hey ", title) FROM album;
    +----------------------------+
    | CONCAT("Hey ", title)      |
    +----------------------------+
    | Hey Two Men with the Blues |
    | Hey Hendrix in the West    |
    | Hey Rubber Soul            |
    | Hey Birds of Fire          |
    | Hey Live And               |
    | Hey Apostrophe             |
    | Hey Kind of Blue           |
    +----------------------------+
    7 rows in set (0.00 sec)

    mysql> SELECT CONCAT_WS(":", "1", 2, "3", "4");
    +----------------------------------+
    | CONCAT_WS(":", "1", 2, "3", "4") |
    +----------------------------------+
    | 1:2:3:4                          |
    +----------------------------------+
    1 row in set (0.00 sec)

    mysql> SELECT LPAD(title, 30, ' ') FROM album;
    +--------------------------------+
    | LPAD(title, 30, ' ')           |
    +--------------------------------+
    |         Two Men with the Blues |
    |            Hendrix in the West |
    |                    Rubber Soul |
    |                  Birds of Fire |
    |                       Live And |
    |                     Apostrophe |
    |                   Kind of Blue |
    +--------------------------------+
    7 rows in set (0.00 sec)

    mysql> SELECT RPAD(title, 30, ' ') FROM album;
    +--------------------------------+
    | RPAD(title, 30, ' ')           |
    +--------------------------------+
    | Two Men with the Blues         |
    | Hendrix in the West            |
    | Rubber Soul                    |
    | Birds of Fire                  |
    | Live And                       |
    | Apostrophe                     |
    | Kind of Blue                   |
    +--------------------------------+
    7 rows in set (0.00 sec)

    # Get counties that has no cities
    mysql> SELECT Name FROM Country WHERE Code NOT IN (SELECT DISTINCT CountryCode FROM City);
    +----------------------------------------------+
    | Name                                         |
    +----------------------------------------------+
    | Antarctica                                   |
    | Bouvet Island                                |
    | British Indian Ocean Territory               |
    | South Georgia and the South Sandwich Islands |
    | Heard Island and McDonald Islands            |
    | French Southern territories                  |
    | United States Minor Outlying Islands         |
    +----------------------------------------------+
    7 rows in set (0.31 sec)

    # numbre of cities for each country
    mysql> SELECT CountryCode, COUNT(CountryCode) FROM City GROUP BY CountryCode;
    
Django
======

=============================================
How to set a label for a field that is a method
=============================================

::

	class MyAdmin(...):
		list_display = ('_my_field',)

		def _my_field(self, obj):
			return obj.get_full_name()
		_my_field.short_description = 'my custom label'



=============================================
iPython
=============================================

::

	%load_ext autoreload
	%autoreload 2

Как написать макрос для повторяющихся действий:

::

	In [8]: print 1
	1
	In [9]: print 2
	2
	In [10]: print 34
	34

	In [12]: macro cosa 8 9 10
	Macro `cosa` created. To execute, type its name (without quotes).
	=== Macro contents: ===
	print 1
	print 2
	print 34

	In [13]: cosa
	1
	2
	34

	In [14]: %edit cosa


=============================================
translation
=============================================

::

    for d in app catalog common community contact event festival userprofile; do
    cd $d
    ../manage.py makemessages --all
    cd ..
    done
