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
