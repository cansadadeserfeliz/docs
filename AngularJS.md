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

[AngularJS MTV Meetup: Best Practices (2012/12/11)](https://www.youtube.com/watch?v=ZhfUv0spHCY)#

## Module

An Angular module is a collection of:
* Controllers
* Directives
* Filters
* Services
* Other configuration information

```javascript
    (function(){
      var app = angular.module('store', []);
    })();
```

[Here's the calling order](http://stackoverflow.com/a/20664122/914332):

1. `app.config()`
2. `app.run()`
3. *directive's compile functions (if they are found in the dom)*
4. `app.controller()`
5. *directive's link functions (again, if found)*


## Expressions

Expressions - how values get displayed within the page.

* Evaluated against an Angular *scope* object.
* No conditionals, loops or exceptions.
* Expressions enclosed in {{ expression }}

## Directives

Directives - HTML annotations that trigger Javascript behaviors.

``ng-app`` - attach the Application Module to the page

```html
    <html ng-app="store">
```

``ng-controller`` - attach a Controller function to the pages

```html
    <body ng-controller="StoreController as store">
```

``ng-show`` / ``ng-hide`` - display a section based on an Expression

```html
    <h1 ng-show="name"> Hello, {{ name }}! <h1>
```

``ng-repeat`` - repeat a section for each item in an Array

```html
    <li ng-repeat="product in store.products"> {{ product.name }} </li>
```

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

```html
    <img src="{{ product.images[0].full }}" />  --> ERROR
```

The browser tries to load images *before* the Expression evaluates.

```html
    <img ng-src="{{ product.images[0].full }}" />  --> ERROR
```

Codepen with example from CodeSchool course: http://codepen.io/vero4ka/pen/OMOvab

## Form validation

[AngularJS form validaion](https://scotch.io/tutorials/angularjs-form-validation)

Add validation to a form:

1. Turn off HTML validations (of browsers):

```html
    <form name="reviewForm" novalidate>
```

2. Mark required fields:

```html
    <input nama="author" required>
```

3. Check if validation works (via form name):

```html
    <div>review form is {{reviewForm.$valid}}</div>
```

4. Prevent the form from getting submitted:

```html
    <form name="reviewForm" ng-submit="reviewForm.$valid && reviewCtrl.addReview(product)" novalidate>
```

5. Show the user why the form isn't valid.

Angular adds some classes:

```html
    <input name="author" type="email" class="ng-pristine ng-invalid" />
```

``ng-pristine`` - the field hasn't been touched.

``ng-invalid`` - the field is not valid.

And on change the class gets updated:

```html
    <input name="author" type="email" class="ng-dirty ng-invalid" />
```

``ng-dirty`` - the field was changed.

When we have a valid email it becomes:

```html
    <input name="author" type="email" class="ng-dirty ng-valid" />
```

So we can use it in our CSS:

```css
    .ng-invalid.ng-dirty {
      border-color: #FA787E;  // red
    }

    .ng-valid.ng-dirty {
      border-color: #78FA89; // green
    }
```

Angular has build-in email, url, numbers (min/max) validation.

## Directives

* Template-expanding Directives
* Expressing complex UI
* Calling events and registering event handlers
* Reusing common components

### Element directive

```html
    <product-title></product-title>
```
```javascript
    app.directive('productTitle', function() {
      return {
        // a configuration object defining how your directive will work
        restrict: 'E',  // directive type - Element
        templateUrl: 'product-title.html'
      };
    });
```

### Attribute directive

```html
    <h3 product-title></h3>
```
```javascript
    app.directive('productTitle', function() {
      return {
        restrict: 'A',  // directive type - Attribute
        templateUrl: 'product-title.html'
      };
    });
```

## Directive Controllers

```html
    <product-panels></product-panels>
```
```javascript
    app.directive('productPanels', function() {
      return {
        restrict: 'E',
        templateUrl: 'product-panels.html',
        controllerAs: 'panels',
        controller: function() {
        
        }
      };
    });
```

## Routing

* [ui.router wiki](https://github.com/angular-ui/ui-router/wiki)
* [ui.router documentation](https://angular-ui.github.io/ui-router/site/#/api/ui.router)
* [AngularJS + UI Router: проверка авторизации и прав доступа](https://habrahabr.ru/post/245049/)

## Dependencies

```html
    // index.html
  
    <script src="angular.js"></script>
    <script src="app.js"></script>
    <script src="products.js"></script>
```
```javascript
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
```

## Services

Allow to get data from API.

``$http`` - fetching JSON tada from a web service

``$log`` - logging messages to the JavaScript console

``$log`` - filter in array

```javascript
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
```

* https://jakearchibald.com/2014/using-serviceworker-today/
* https://css-tricks.com/snippets/css/a-guide-to-flexbox/
* https://github.com/angular-ui/ui-router
* https://github.com/johnpapa/angular-styleguide
* https://github.com/toddmotto/angular-styleguide
* http://www.codelord.net/2015/05/25/dont-use-$https-success/

## Tests

http://www.seleniumhq.org/projects/webdriver/

* [E2E Testing](https://docs.angularjs.org/guide/e2e-testing)
* [Protractor](https://angular.github.io/protractor/#/)
* [AngularJS Testing - Unit Testing Tutorials](http://www.bradoncode.com/tutorials/angularjs-unit-testing/)

## Learning

* [AngularJS Learning](https://github.com/jmcunningham/AngularJS-Learning)

## Related information

* [TypeScript: общие впечатления](https://habrahabr.ru/post/258957/)
* [GulpJS — фантастически быстрый сборщик проектов](https://habrahabr.ru/post/208890/)
* wrench.js - Recursive file operations in Node.js

### ServiceWorker

https://www.chromium.org/blink/serviceworker

A service worker is a script that is run by your browser in the background.

Features: push notifications, the ability to intercept and handle network requests, including programmatically managing a cache of responses.

* [Introduction to Service Worker](http://www.html5rocks.com/en/tutorials/service-worker/introduction/)
* [Is Service Worker Ready?](https://jakearchibald.github.io/isserviceworkerready/)
* [Using ServiceWorker in Chrome today by Jake Archibald](https://jakearchibald.com/2014/using-serviceworker-today/)
* [Jake Archibald's "simple-serviceworker-tutorial"](https://github.com/jakearchibald/simple-serviceworker-tutorial)

* [Manifest File Format](https://developer.chrome.com/extensions/manifest)

### Promises

* [JavaScript Promises](https://www.promisejs.org/)

Promise – это специальный объект, который содержит своё состояние. Вначале `pending` («ожидание»), затем – одно из: `fulfilled` («выполнено успешно») или `rejected` («выполнено с ошибкой»)

* [Что такое Promise?](https://learn.javascript.ru/promise)
* [Обещания JavaScript](https://habrahabr.ru/post/209662/)
