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
    
**Directives** - HTML annotations that trigger Javascript behaviors.

``ng-app`` - attach the Application Module to the page

::

  <html ng-app="store">

``ng-controller`` - attach a Controller function to the pages

::

  <body ng-controller="StoreController as store">

``ng-show`` / ``ng-hide`` - display a section based on an Expression

::

  <h1 ng-show="name"> Hello, {{ name }}! <h1>

``ng-repeat`` - repeat a section for each item in an Array

::

  <li ng-repeat="product in store.products"> {{ product.name }} </li>

**Modules** - Where our application components live.

**Controllers** - Where we add application behavior. 
Controllers help us to get data on to the page. Controllers are where we
define our app's behavior by defining functions and values.

**Expressions** - How values get displayed within the page.

Formatting with filters.

::

  {{ data | filter:options }}
  {{ '1388123412323' | date:'MM/dd/yyyy @ h:mma' }} --> 12/27/2013 @ 12:50AM
  {{ 'octagon gem' | uppercase }} --> OCTAGON GEM
  {{ 'My Description' | limitTo:8 }} --> My Descr
  {{ data | orderBy:'-price' }}  --> sorts from most expensive to least expensive
  
Images.

::

  <img src="{{ product.images[0].full }}" />  --> ERROR
  
The browser tries to load images *before* the Expression evaluates.

::

  <img ng-src="{{ product.images[0].full }}" />  --> ERROR

Codepen with example from CodeSchool course: http://codepen.io/vero4ka/pen/OMOvab

**Add validation to form**:

1. Turn off HTML validations (of browsers)

::

  <form name="reviewForm" novalidate>
  
2. Mark required fields

::

  <input nama="author" required>
  
3. Check if validation works (via form name):

::

  <div>review form is {{reviewForm.$valid}}</div>

4. Prevent the form from getting submitted:

::

  <form name="reviewForm" ng-submit="reviewForm.$valid && reviewCtrl.addReview(product)" novalidate>
  
5. Show the user why the form isn't valid.

Angular adds some classes:

::

  <input name="author" type="email" class="ng-pristine ng-invalid" />
  
``ng-pristine`` - the field hasn't been touched.

``ng-invalid`` - the field is not valid.

And on change the class gets updated:
 
::

  <input name="author" type="email" class="ng-dirty ng-invalid" />
  
``ng-dirty`` - the field was changed.

When we have a valid email it becomes:

::

  <input name="author" type="email" class="ng-dirty ng-valid" />

So we can use it in our CSS:

::

  .ng-invalid.ng-dirty {
    border-color: #FA787E;  // red
  }

  .ng-valid.ng-dirty {
    border-color: #78FA89; // green
  }
  
Angular has build-in email, url, numbers (min/max) validation.

**Directives**

* Template-expanding Directives
* Expressing complex UI
* Calling events and registering event handlers
* Reusing common components

*Element directive*:

::

  <product-title></product-title>
  
  app.directive('productTitle', function() {
    return {
      // a configuration object defining how your directive will work
      restrict: 'E',  // directive type - Element
      templateUrl: 'product-title.html'
    };
  });
  
*Attribute directive*:

::

  <h3 product-title></h3>
  
  app.directive('productTitle', function() {
    return {
      restrict: 'A',  // directive type - Attribute
      templateUrl: 'product-title.html'
    };
  });
  
*Directive COntrollers*:

::

  <product-panels></product-panels>

  app.directive('productPanels', function() {
    return {
      restrict: 'E',
      templateUrl: 'product-panels.html',
      controllerAs: 'panels',
      controller: function() {
      
      }
    };
  });
  
**Dependencies**

::

  // index.html
  
  <script src="angular.js"></script>
  <script src="app.js"></script>
  <script src="products.js"></script>

  // app.js
  
  (function(){
    var app = angular.module('store', ['store-products']);
    
    app.controller('storeController'), function() { ... });
  })();

  // products.js
  
  (function(){
    var app = angular.module('store-products', []);
    
    app.directive('productTitle'), function() { ... });
    app.directive('productPanels'), function() { ... });
  })();
  
**Services**

Allow to get data from API.

``$http`` - fetching JSON tada from a web service

``$log`` - logging messages to the JavaScript console

``$log`` - filter in array

::

  // app.js

  (function(){
    var app = angular.module('store', ['store-products']);
    
    app.controller('storeController'), [ '$http', function ($http) {
      var store = this;
      store.products = [];  // so when the page loads there will be no errors
      
      $http.get('/products.json', {apiKey: 'myApiKey'}).success(function(data){
        store.products = data;
      });
    } ]);
  })();


=======
Ruby
=======

``to_s`` converts values to **s**trings

``to_i`` converts values to **i**ntegers

``to_a`` converts values to **a**rrays

**Exclamation Points.** Methods may have exclamation points in their name, 
which just means to impact the current data, rather than making a copy.

``ticket.sort!`` The exclamation signals that we intend for Ruby to directly 
modify the same array that we've built, rather than make a brand new copy 
that is sorted.

**Square Brackets.** With these, you can target and find things. 
You can even replace them if necessary.

**Chaining methods** lets you get a lot more done in a single command. 
Break up a poem, reverse it, reassemble it: ``poem.lines.to_a.reverse.join``.

Complete list of string methods: http://ruby-doc.org/core-2.3.0/String.html


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
