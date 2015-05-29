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

###Manually Identify Route Resolver Dependencies
Use `$inject` to manually identify your route resolver dependencies for Angular components.

##Minification and Annotation
###ng-annotate
Use ng-annotate for Gulp or Grunt and comment functions that need automated dependency injection using /** @ngInject */

###Use Gulp or Grunt for ng-annotate
Use gulp-ng-annotate or grunt-ng-annotate in an automated build task. Inject /* @ngInject */ prior to any function that has dependencies.

##Exception Handling
###decorators
Use a decorator, at config time using the $provide service, on the $exceptionHandler service to perform custom actions when exceptions occur.

###Exception Catchers
Create a factory that exposes an interface to catch and gracefully handle exceptions.

###Route Errors
Handle and log all routing errors using `$routeChangeError`.

##Naming
###Naming Guidelines
Use consistent names for all components following a pattern that describes the component's feature then (optionally) its type. My recommended pattern is feature.type.js. There are 2 names for most assets:
* the file name (avengers.controller.js)
* the registered component name with Angular (AvengersController)

###Feature File Names
Use consistent names for all components following a pattern that describes the component's feature then (optionally) its type. My recommended pattern is feature.type.js.
 ```javascript
/**
 * recommended
 */

// controllers
avengers.controller.js
avengers.controller.spec.js

// services/factories
logger.service.js
logger.service.spec.js

// constants
constants.js

// module definition
avengers.module.js

// routes
avengers.routes.js
avengers.routes.spec.js

// configuration
avengers.config.js

// directives
avenger-profile.directive.js
avenger-profile.directive.spec.js
 ```
###Test File Names
Name test specifications similar to the component they test with a suffix of spec.
 
###Controller Names
Use consistent names for all controllers named after their feature. Use UpperCamelCase for controllers, as they are constructors.

###Controller Name Suffix
Append the controller name with the suffix Controller.

###Factory Names
Use consistent names for all factories named after their feature. Use camel-casing for services and factories. Avoid prefixing factories and services with `$`.

###Directive Component Names
Use consistent names for all directives using camel-case. Use a short prefix to describe the area that the directives belong (some example are company prefix or project prefix).

###Modules
When there are multiple modules, the main module file is named app.module.js while other dependent modules are named after what they represent. For example, an admin module is named admin.module.js. The respective registered module names would be app and admin.

###Configuration
Separate configuration for a module into its own file named after the module. A configuration file for the main app module is named app.config.js (or simply config.js). A configuration for a module named admin.module.js is named admin.config.js.

###Routes
Separate route configuration into its own file. Examples might be app.route.js for the main module and admin.route.js for the admin module. Even in smaller apps I prefer this separation from the rest of the configuration.

##Application Structure LIFT Principle
###LIFT
Structure your app such that you can Locate your code quickly, Identify the code at a glance, keep the Flattest structure you can, and Try to stay DRY. The structure should follow these 4 basic guidelines.

Why LIFT?: Provides a consistent structure that scales well, is modular, and makes it easier to increase developer efficiency by finding code quickly. Another way to check your app structure is to ask yourself: How quickly can you open and work in all of the related files for a feature?

When I find my structure is not feeling comfortable, I go back and revisit these LIFT guidelines

* `L`ocating our code is easy
* `I`dentify code at a glance
* `F`lat structure as long as we can
* `T`ry to stay DRY (Don’t Repeat Yourself) or T-DRY

###Locate
Make locating your code intuitive, simple and fast.

###Identify
When you look at a file you should instantly know what it contains and represents.

###Flat
Keep a flat folder structure as long as possible. When you get to 7+ files, begin considering separation.

###T-DRY (Try to Stick to DRY)
Be DRY, but don't go nuts and sacrifice readability.

##Application Structure
###Overall Guidelines
Have a near term view of implementation and a long term vision. In other words, start small but keep in mind on where the app is heading down the road. All of the app's code goes in a root folder named app. All content is 1 feature per file. Each controller, service, module, view is in its own file. All 3rd party vendor scripts are stored in another root folder and not in the app folder. I didn't write them and I don't want them cluttering my app (bower_components, scripts, lib).

###Layout
Place components that define the overall layout of the application in a folder named layout. These may include a shell view and controller may act as the container for the app, navigation, menus, content areas, and other regions.

###Folders-by-Feature Structure
Create folders named for the feature they represent. When a folder grows to contain more than 7 files, start to consider creating a folder for them. Your threshold may be different, so adjust as needed.
```javascript
/**
 * recommended
 */

app/
    app.module.js
    app.config.js
    components/
        calendar.directive.js
        calendar.directive.html
        user-profile.directive.js
        user-profile.directive.html
    layout/
        shell.html
        shell.controller.js
        topnav.html
        topnav.controller.js
    people/
        attendees.html
        attendees.controller.js
        people.routes.js
        speakers.html
        speakers.controller.js
        speaker-detail.html
        speaker-detail.controller.js
    services/
        data.service.js
        localstorage.service.js
        logger.service.js
        spinner.service.js
    sessions/
        sessions.html
        sessions.controller.js
        sessions.routes.js
        session-detail.html
        session-detail.controller.js
   ```
   
##Modularity
###Many Small, Self Contained Modules
Create small modules that encapsulate one responsibility.

*Why?*: Modular applications make it easy to plug and go as they allow the development teams to build vertical slices of the applications and roll out incrementally. This means we can plug in new features as we develop them.

###Create an App Module
Create an application root module whose role is pull together all of the modules and features of your application. Name this for your application.

*Why?*: Angular encourages modularity and separation patterns. Creating an application root module whose role is to tie your other modules together provides a very straightforward way to add or remove modules from your application.

###Keep the App Module Thin
Only put logic for pulling together the app in the application module. Leave features in their own modules.

*Why?*: Adding additional roles to the application root to get remote data, display views, or other logic not related to pulling the app together muddies the app module and make both sets of features harder to reuse or turn off.

*Why?*: The app module becomes a manifest that describes which modules help define the application.

###Feature Areas are Modules
Create modules that represent feature areas, such as layout, reusable and shared services, dashboards, and app specific features (e.g. customers, admin, sales).

*Why?*: Self contained modules can be added to the application with little or no friction.

*Why?*: Sprints or iterations can focus on feature areas and turn them on at the end of the sprint or iteration.

*Why?*: Separating feature areas into modules makes it easier to test the modules in isolation and reuse code.

###Reusable Blocks are Modules
Create modules that represent reusable application blocks for common services such as exception handling, logging, diagnostics, security, and local data stashing.

###Module Dependencies
The application root module depends on the app specific feature modules and any shared or reusable modules.

![Modularity and Dependencies](https://raw.githubusercontent.com/johnpapa/angular-styleguide/master/assets/modularity-1.png)

##Startup Logic
###Configuration
Inject code into module configuration that must be configured before running the angular app. Ideal candidates include providers and constants.

*Why?*: This makes it easier to have a less places for configuration.

```javascript
angular
    .module('app')
    .config(configure);

configure.$inject =
    ['routerHelperProvider', 'exceptionHandlerProvider', 'toastr'];

function configure (routerHelperProvider, exceptionHandlerProvider, toastr) {
    exceptionHandlerProvider.configure(config.appErrorPrefix);
    configureStateHelper();

    toastr.options.timeOut = 4000;
    toastr.options.positionClass = 'toast-bottom-right';

    ////////////////

    function configureStateHelper() {
        routerHelperProvider.configure({
            docTitle: 'NG-Modular: '
        });
    }
}
 ```
###Run Blocks
Any code that needs to run when an application starts should be declared in a factory, exposed via a function, and injected into the run block.

*Why?*: Code directly in a run block can be difficult to test. Placing in a factory makes it easier to abstract and mock. 
 
##Angular $ Wrapper Services
###$document and $window
Use `$document` and `$window` instead of document and window.

*Why?*: These services are wrapped by Angular and more easily testable than using document and window in tests. This helps you avoid having to mock document and window yourself.
