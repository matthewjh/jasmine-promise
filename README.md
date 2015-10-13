# jasmine-promise

[![Travis CI build status](https://api.travis-ci.org/matthewjh/jasmine-promise.png)](https://travis-ci.org/matthewjh/jasmine-promise)

Write asynchronous tests easier by returning `Promise`s from your spec functions.

Benefits:
* Works with any `then`able. ✓
* Simply return a promise from a test -- no need to call `done` and `done.fail` ✓
* Automatic error handling when using native `Promise`'s'. When writing such tests manually, you have to explictly catch the error with `.catch` and then pass the error to `done.fail` or rethrow. Unhandled `Promise` rejections are gobbled up so if you forget to do this you can miss out on debugging info. ✓
* Works with `it`, `fit`, `beforeEach`, `afterEach`, `beforeAll`, and `afterAll`. ✓

## Installation

Note: only compatible with Jasmine 2 at this point.

````
npm install jasmine-promise --save-dev`
````

Then ensure that the `jasmine-promise` module's `index.js` script is loaded before your tests are loaded. This can be done by either...

manually requiring the module at the top of your test file(s):

````javascript
require('jasmine-promise');

describe('my fancy thing', function () {
	it('should be extra fancy', function () {
		return fancyAsync().then(function (thing) {
			expect(thing).toBeFancy();
		});
	});
});

````

loading it via your test runner e.g. Karma:

````javascript
module.exports = function(config) {
  config.set({

    // base path that will be used to resolve all patterns (eg. files, exclude)
    basePath: '',


    // frameworks to use
    // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
    frameworks: ['jasmine'],


    // list of files / patterns to load in the browser
    files: [
      'node_modules/jasmine-promise/index.js',
      'test/**/*.spec.js'
    ],
````


