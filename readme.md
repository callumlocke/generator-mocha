# Mocha+Testem generator [![Build Status](https://secure.travis-ci.org/callumlocke/generator-mocha-testem.png?branch=master)](http://travis-ci.org/callumlocke/generator-mocha-testem)

This is a fork of [generator-mocha](https://github.com/yeoman/generator-mocha), modifed to work with [Testem](https://github.com/airportyh/testem). ([See differences](https://github.com/callumlocke/generator-mocha-testem/compare/yeoman:master...master).)

Works well with [generator-webapp](https://github.com/yeoman/generator-webapp).

## Getting Started

    npm install -g generator-mocha-testem


## Usage

    yo mocha-testem

What this does:
* creates `test` directory (similar to generator-mocha's, but modified to work through the Testem server)
* creates `testem.json`
* adds some lines to your `.gitignore`

Now run `testem`, and it should launch some browsers and run your tests.


## How to use with generator-webapp

* `mkdir myproject && cd myproject`
* `yo webapp`
* Delete the `test` directory: `rm -rf test`
* `yo mocha-testem`

You can now run `testem` and `grunt server` at the same time in different terminals, and you'll have a live-reloading webapp and live-reloading test results at the same time.

In your spec runner (`test/index.html`), add your script tags in this form:
* application scripts: `<script src="../app/scripts/foo.js"></script>`
* test scripts: `<script src="specs/foo-test.js"></script>`


### Optional: add the grunt-testem plugin

Follow these instructions to use Testem in CI mode during your build process. It launches each browser in turn, runs your tests, and closes them afterwards, then proceeds to the next step (e.g. build) only if everything was green.

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

Now try running `grunt test` (or just `grunt`).

You can configure which browsers it launches by editing the `launch_in_ci` section in `testem.json`.


### Coffeescript

_(Not yet tested.)_

When running `grunt server` in a webapp project, CoffeeScripts are compiled to `.tmp`. So if you want to unit-test a `*.coffee` file, the script tag in your `test/index.html` will need to look like this: `<script src="../.tmp/scripts/foo.js"></script>`.

(I haven't yet looked into using CoffeeScript for test files yet. More steps will be needed. Suggestions/PRs welcome.)


## Contribute

See the [contributing docs](https://github.com/yeoman/yeoman/blob/master/contributing.md)


## License

[BSD license](http://opensource.org/licenses/bsd-license.php)
