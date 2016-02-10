# Angular.JS

Designed by Misco Hevery. First released in June 2012.

[An application skeleton for a typical AngularJS web app](https://github.com/angular/angular-seed).

    app/                    --> all of the source files for the application
      app.css               --> default stylesheet
      components/           --> all app specific modules
        version/              --> version related components
          version.js                 --> version module declaration and basic "version" value service
          version_test.js            --> "version" value service tests
          version-directive.js       --> custom directive that returns the current app version
          version-directive_test.js  --> version directive tests
          interpolate-filter.js      --> custom interpolation filter
          interpolate-filter_test.js --> interpolate filter tests
      view1/                --> the view1 view template and logic
        view1.html            --> the partial template
        view1.js              --> the controller logic
        view1_test.js         --> tests of the controller
      view2/                --> the view2 view template and logic
        view2.html            --> the partial template
        view2.js              --> the controller logic
        view2_test.js         --> tests of the controller
      app.js                --> main application module
      index.html            --> app layout file (the main html template file of the app)
      index-async.html      --> just like index.html, but loads js files asynchronously
    karma.conf.js         --> config file for running unit tests with Karma
    e2e-tests/            --> end-to-end tests
      protractor-conf.js    --> Protractor config file
      scenarios.js          --> end-to-end scenarios to be run by Protractor

[Yeoman project generator](http://yeoman.io/)

[AngularJS MTV Meetup: Best Practices (2012/12/11)](https://www.youtube.com/watch?v=ZhfUv0spHCY)

Create an application:

```javascript
    (function(){
      var app = angular.module('store', []);
    })();
```

## Expressions

Expressions - how values get displayed within the page.

* Evaluated against an Angular *scope* object.
* No conditionals, loops or exceptions.
* Expressions enclosed in {{ expression }}

## Directives

Directives - HTML annotations that trigger Javascript behaviors.

``ng-app`` - attach the Application Module to the page

    <html ng-app="store">

``ng-controller`` - attach a Controller function to the pages

    <body ng-controller="StoreController as store">

``ng-show`` / ``ng-hide`` - display a section based on an Expression

    <h1 ng-show="name"> Hello, {{ name }}! <h1>

``ng-repeat`` - repeat a section for each item in an Array

    <li ng-repeat="product in store.products"> {{ product.name }} </li>

*Two-way data binding*: ``ng-model`` directive.

**Modules** - Where our application components live.

**Controllers** - Where we add application behavior. 
Controllers help us to get data on to the page. Controllers are where we
define our app's behavior by defining functions and values.

## Filters

Formatting with filters.

    {{ data | filter:options }}
    {{ '1388123412323' | date:'MM/dd/yyyy @ h:mma' }} --> 12/27/2013 @ 12:50AM
    {{ 'octagon gem' | uppercase }} --> OCTAGON GEM
    {{ 'My Description' | limitTo:8 }} --> My Descr
    {{ data | orderBy:'-price' }}  --> sorts from most expensive to least expensive
  
## Images

    <img src="{{ product.images[0].full }}" />  --> ERROR
  
The browser tries to load images *before* the Expression evaluates.

    <img ng-src="{{ product.images[0].full }}" />  --> ERROR

Codepen with example from CodeSchool course: http://codepen.io/vero4ka/pen/OMOvab

## Form validation

Add validation to a form

1. Turn off HTML validations (of browsers):

    <form name="reviewForm" novalidate>

2. Mark required fields:

    <input nama="author" required>

3. Check if validation works (via form name):

    <div>review form is {{reviewForm.$valid}}</div>

4. Prevent the form from getting submitted:

    <form name="reviewForm" ng-submit="reviewForm.$valid && reviewCtrl.addReview(product)" novalidate>
  
5. Show the user why the form isn't valid.

Angular adds some classes:

    <input name="author" type="email" class="ng-pristine ng-invalid" />
  
``ng-pristine`` - the field hasn't been touched.

``ng-invalid`` - the field is not valid.

And on change the class gets updated:
 
    <input name="author" type="email" class="ng-dirty ng-invalid" />
  
``ng-dirty`` - the field was changed.

When we have a valid email it becomes:

    <input name="author" type="email" class="ng-dirty ng-valid" />

So we can use it in our CSS:

    .ng-invalid.ng-dirty {
      border-color: #FA787E;  // red
    }

    .ng-valid.ng-dirty {
      border-color: #78FA89; // green
    }
  
Angular has build-in email, url, numbers (min/max) validation.

## Directives

* Template-expanding Directives
* Expressing complex UI
* Calling events and registering event handlers
* Reusing common components

### Element directive

     <product-title></product-title>
  
    app.directive('productTitle', function() {
      return {
        // a configuration object defining how your directive will work
        restrict: 'E',  // directive type - Element
        templateUrl: 'product-title.html'
      };
    });
  
### Attribute directive

    <h3 product-title></h3>
  
    app.directive('productTitle', function() {
      return {
        restrict: 'A',  // directive type - Attribute
        templateUrl: 'product-title.html'
      };
    });
  
## Directive Controllers

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
  
## Dependencies

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
  
## Services

Allow to get data from API.

``$http`` - fetching JSON tada from a web service

``$log`` - logging messages to the JavaScript console

``$log`` - filter in array

    // app.js

    (function(){
      var app = angular.module('store', ['store-products']);
    
      app.controller('storeController', [ '$http', function ($http) {
        var store = this;
        store.products = [];  // so when the page loads there will be no errors
      
        $http.get('/products.json', {apiKey: 'myApiKey'}).success(function(data){
          store.products = data;
        });
      } ]);
    })();


* https://jakearchibald.com/2014/using-serviceworker-today/
* https://css-tricks.com/snippets/css/a-guide-to-flexbox/
* https://github.com/angular-ui/ui-router
* https://github.com/johnpapa/angular-styleguide
* https://github.com/toddmotto/angular-styleguide
* http://www.codelord.net/2015/05/25/dont-use-$https-success/

## Tests

http://www.seleniumhq.org/projects/webdriver/

## Learning

* [AngularJS Learning](https://github.com/jmcunningham/AngularJS-Learning)