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
