## Testing

Unit testing helps maintain clean code.

###Write Tests with Stories
Write a set of tests for every story. Start with an empty test and fill them in as you write the code for the story.

*Why?*: Writing the test descriptions helps clearly define what your story will do, will not do, and how you can measure success.
```javascript
it('should have Avengers controller', function() {
    // TODO
});

it('should find 1 Avenger when filtered by name', function() {
    // TODO
});

it('should have 10 Avengers', function() {
    // TODO (mock data?)
});

it('should return Avengers via XHR', function() {
    // TODO ($httpBackend?)
});

// and so on
 ```

###Testing Library
Use Jasmine or Mocha for unit testing.

*Why?*: Both Jasmine and Mocha are widely used in the Angular community. Both are stable, well maintained, and provide robust testing features.

Note: When using Mocha, also consider choosing an assert library such as Chai. I prefer Mocha.

###Test Runner
Use Karma as a test runner.

###Stubbing and Spying
Use Sinon for stubbing and spying.

###Headless Browser
Use PhantomJS to run your tests on a server.

###Code Analysis
Run JSHint on your tests.

###Alleviate Globals for JSHint Rules on Tests
Relax the rules on your test code to allow for common globals such as describe and expect. Relax the rules for expressions, as Mocha uses these.

Why?: Your tests are code and require the same attention and code quality rules as all of your production code. However, global variables used by the testing framework, for example, can be relaxed by including this in your test specs.

/* jshint -W117, -W030 */
Or you can add the following to your JSHint Options file.

"jasmine": true,
"mocha": true,

###Organizing Tests
Place unit test files (specs) side-by-side with your client code. Place specs that cover server integration or test multiple components in a separate tests folder.

