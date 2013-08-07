# Mocha+Testem generator [![Build Status](https://secure.travis-ci.org/callumlocke/generator-mocha-testem.png?branch=master)](http://travis-ci.org/callumlocke/generator-mocha-testem)


## Getting Started

Install:

    npm install -g generator-mocha-testem

### Usage

    yo mocha-testem
    testem

### How to use with generator-webapp

This assumes you're starting a new project.

* `mkdir myproject && cd myproject`
* `yo webapp`
* Delete the `test` directory: `rm -rf test`
* `yo mocha-testem`
* Run `testem`. It should launch new Chrome and Firefox processes, which you can minimise. You can now use Testem for TDD in the usual way ([see docs](https://github.com/sideroad/grunt-testem)).
* You can run `grunt-server` in another terminal at the same time.
* In your spec runner (`test/index.html`), add script tags for your implementation code, which should look something like this: `<script src="../app/scripts/foo.js"></script>`. Script tags for spec files should look like this: `<script src="specs/foo-test.js"></script>`.

#### Optional: add the grunt-testem plugin

This lets you use Testem in CI mode during your build process. It launches browsers, runs your tests in them, and closes them afterwards.

* Remove grunt-mocha: `npm uninstall -D grunt-mocha`
* Add grunt-testem: `npm install -D grunt-testem`
* In your Gruntfile...
  * remove the entire config entry for `mocha`, and remove the `test` target of `connect`
  * find `grunt.registerTask('test'...`, remove the `connect:test` subtask, and change `'mocha'` to `'testem'`
  * add this config entry:

```javascript
        testem: {
            main: {
                src: [ 'testem.json' ],
                dest: 'tests.tap'
            }
        }
```

Edit the `launch_in_ci` list of browsers in your `testem.json` if necessary. Now try running `grunt test`.

#### Coffeescript

More steps are probably needed to get this working with Coffeescript... Instructions will appear here when I've worked it out myself. PRs welcome.


## Contribute

See the [contributing docs](https://github.com/yeoman/yeoman/blob/master/contributing.md)


## License

[BSD license](http://opensource.org/licenses/bsd-license.php)
