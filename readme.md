This is an example meteor app to show that `spacejam + mocha` is not reliable right now.

The circle.yml and .travis.yml executes 10 times the same test and sometimes there are dependencies injection error that crash the app, when the browser (phantomjs) opens the test page.  

    # I20160708-16:04:29.809(0)? registerSourceMap../web.browser/app/app.js
    # I20160708-16:04:29.810(0)? Add source map for file ../web.browser/app/app.js.map
    # I20160708-16:04:29.810(0)? registerSourceMap../web.browser/app/app.js
    # phantomjs: Error: Cannot find module 'meteor/practicalmeteor:mocha/meteor/src/index.js'
    #     http://localhost:4096/packages/modules-runtime.js?hash=b7370236eeaf57e8f4ac703424bc831028392451: 439
    # or
    # phantomjs: TypeError: undefined is not an object (evaluating 'Package['practicalmeteor:chai'].chai')
    #     http://localhost:4096/packages/practicalmeteor_sinon.js?hash=d51f09b72f5e645e87a6101ca90a5e06f108616d: 1
    # or
    # phantomjs: TypeError: undefined is not an object (evaluating 'Package['practicalmeteor:loglevel'].loglevel')
    #    http://localhost:4096/packages/practicalmeteor_mocha.js?hash=0c7bae1a756c9691267ec935a8d6a4e081df9cf6: 9

See logs on https://travis-ci.org/serut/meteor-coverage-app-exemple/branches and https://circleci.com/gh/serut/meteor-coverage-app-exemple
Good luck with that @practicalmeteor !!!

This app contains
- a meteor app v1.3.4.4
- all packages updated to their last version except
> $ meteor update --allow-incompatible-update  
> The following top-level dependencies were not updated to the very latest version available:
> * practicalmeteor:mocha 2.4.5_5 (2.4.5_6 is available)  

- use the lastest version of spacejam (using the tarball https://github.com/practicalmeteor/spacejam/tarball/windows-suppport)
- an internal package of the app that uses tinytest and mocha
- it covers these types of test:
    - meteor test            --driver-package practicalmeteor:mocha-console-runner
    - meteor test --full-app --driver-package practicalmeteor:mocha-console-runner
    - meteor test-packages   --driver-package practicalmeteor:mocha-console-runner
    - meteor test-packages
