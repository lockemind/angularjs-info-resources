# Angular Style Guide
based on [johnpapa's angular-styleguide](https://github.com/johnpapa/angular-styleguide)
## Single Responsibility
### Rule of 1
Define 1 component per file.

## IIFE
### Javascript closures
Wrap Angular components in an Immediately Invoked Function Expression (IIFE).

##Modules
###Avoid Naming Collisions
Use unique naming conventions with separators for sub-modules.

###Definitions (aka Setters)
Declare modules without a variable using the setter syntax.

###Getters
When using a module, avoid using a variable and instead use chaining with the getter syntax.

###Setting vs Getting
Only set once and get for all other instances.

*Why?*: A module should only be created once, then retrieved from that point and after.
  - Use `angular.module('app', []);` to set a module.
  - Use `angular.module('app');` to get a module.

###Named vs Anonymous Functions
Use named functions instead of passing an anonymous function in as a callback.

##Controllers
###controllerAs View Syntax
Use the controllerAs syntax over the classic controller with $scope syntax.

###controllerAs Controller Syntax
The controllerAs syntax uses this inside controllers which gets bound to $scope

###controllerAs with vm
Use a capture variable for this when using the controllerAs syntax. Choose a consistent variable name such as vm, which stands for ViewModel.

###Bindable Members Up Top
Place bindable members at the top of the controller, alphabetized, and not spread through the controller code.

###Function Declarations to Hide Implementation Details
Use function declarations to hide implementation details. Keep your bindable members up top. When you need to bind a function in a controller, point it to a function declaration that appears later in the file. This is tied directly to the section Bindable Members Up Top.

###Defer Controller Logic to Services
Defer logic in a controller by delegating to services and factories.

*Why?*: Logic may be reused by multiple controllers when placed within a service and exposed via a function.

*Why?*: Logic in a service can more easily be isolated in a unit test, while the calling logic in the controller can be easily mocked.

*Why?*: Removes dependencies and hides implementation details from the controller.

*Why?*: Keeps the controller slim, trim, and focused.

###Keep Controllers Focused
Define a controller for a view, and try not to reuse the controller for other views. Instead, move reusable logic to factories and keep the controller simple and focused on its view.

###Assigning Controllers
When a controller must be paired with a view and either component may be re-used by other controllers or views, define controllers along with their routes.
 ```javascript
  /* recommended */

  // route-config.js
  angular
      .module('app')
      .config(config);

  function config($routeProvider) {
      $routeProvider
          .when('/avengers', {
              templateUrl: 'avengers.html',
              controller: 'Avengers',
              controllerAs: 'vm'
          });
  }
  ```

  ```html
  <!-- avengers.html -->
  <div>
  </div>
  ```
  
##Services

###Singletons
Services are instantiated with the new keyword, use this for public methods and variables. Since these are so similar to factories, use a factory instead for consistency.

Note: All Angular services are singletons. This means that there is only one instance of a given service per injector.

##Factories
###Single Responsibility
Factories should have a single responsibility, that is encapsulated by its context. Once a factory begins to exceed that singular purpose, a new factory should be created.

###Singletons
Factories are singletons and return an object that contains the members of the service.

Note: All Angular services are singletons.

###Accessible Members Up Top
Expose the callable members of the service (its interface) at the top, using a technique derived from the Revealing Module Pattern.

###Function Declarations to Hide Implementation Details
Use function declarations to hide implementation details. Keep your accessible members of the factory up top. Point those to function declarations that appears later in the file. 

##Data Services
###Separate Data Calls
Refactor logic for making data operations and interacting with data to a factory. Make data services responsible for XHR calls, local storage, stashing in memory, or any other data operations.

###Return a Promise from Data Calls
When calling a data service that returns a promise such as $http, return a promise in your calling function too.

##Directives
###Limit 1 Per File
Create one directive per file. Name the file for the directive.

###Manipulate DOM in a Directive
When manipulating the DOM directly, use a directive. If alternative ways can be used such as using CSS to set styles or the animation services, Angular templating, ngShow or ngHide, then use those instead. For example, if the directive simply hides and shows, use ngHide/ngShow.

###Provide a Unique Directive Prefix
Provide a short, unique and descriptive directive prefix such as acmeSalesCustomerInfo which would be declared in HTML as acme-sales-customer-info.

###Restrict to Elements and Attributes
When creating a directive that makes sense as a stand-alone element, allow restrict E (custom element) and optionally restrict A (custom attribute). Generally, if it could be its own control, E is appropriate. General guideline is allow EA but lean towards implementing as an element when it's stand-alone and as an attribute when it enhances its existing DOM element.

###Directives and ControllerAs _REVIEW_
Use controller as syntax with a directive to be consistent with using controller as with view and controller pairings.

Use bindToController = true when using controller as syntax with a directive when you want to bind the outer scope to the directive's controller's scope.

Note: bindToController was introduced in Angular 1.3.0.

##Resolving Promises for a Controller
###Controller Activation Promises
Resolve start-up logic for a controller in an activate function.

##Route Resolve Promises
When a controller depends on a promise to be resolved before the controller is activated, resolve those dependencies in the `$routeProvider` before the controller logic is executed. If you need to conditionally cancel a route before the controller is activated, use a route resolver.

Use a route resolve when you want to decide to cancel the route before ever transitioning to the View.

##Manual Annotating for Dependency Injection
###UnSafe from Minification
Avoid using the shortcut syntax of declaring dependencies without using a minification-safe approach.

###Manually Identify Dependencies
Use `$inject` to manually identify your dependencies for Angular components.