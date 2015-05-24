# Angular Style Guide
based on [johnpapa's angular-styleguide](https://github.com/johnpapa/angular-styleguide)
## Single Responsibility
### Rule of 1
Define 1 component per file.

```javascript
  /* recommended */

  // app.module.js
  angular
      .module('app', ['ngRoute']);
  ```

  ```javascript
  /* recommended */

  // someController.js
  angular
      .module('app')
      .controller('SomeController', SomeController);

  function SomeController() { }
  ```

  ```javascript
  /* recommended */

  // someFactory.js
  angular
      .module('app')
      .factory('someFactory', someFactory);

  function someFactory() { }
  ```

## IIFE
### Javascript closures

Wrap Angular components in an Immediately Invoked Function Expression (IIFE).