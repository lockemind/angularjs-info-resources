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

