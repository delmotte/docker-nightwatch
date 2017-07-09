Dockerfile for [Nightwatch](http://nightwatchjs.org/) test execution
================================================================================

Based on [caltha/protractor](https://bitbucket.org/rkrzewski/dockerfile), this image contains a fully configured environment for running Nightwatch tests under the Chromium browser.

Installed software
------------------
   * [Xvfb](http://unixhelp.ed.ac.uk/CGI/man-cgi?Xvfb+1) The headless X server, for running browsers inside Docker
   * [node.js](http://nodejs.org/) The runtime platform for running JavaScript on the server side, including Nightwatch tests
   * [npm](https://www.npmjs.com/) Node.js package manager used to install Nightwatch and any specific node.js modules the tests may need
   * [Selenium webdriver](http://docs.seleniumhq.org/docs/03_webdriver.jsp) Browser instrumentation agent used by Nightwatch to execute the tests
   * [OpenJDK 8 JRE](http://openjdk.java.net/projects/jdk8/) Needed by Selenium
   * [Chromium](http://www.chromium.org/Home) The OSS core part of Google Chrome browser
   * [Nightwatch](http://nightwatchjs.org/) An end-to-end test framework for web applications
   * [Supervisor](http://supervisord.org/) Process controll system used to manage Xvfb and Selenium background processes needed by Nightwatch

Running
-------
In order to run tests from a CI system, execute the following:
```
docker build -t docker-nightwatch .
docker run --rm -v <test project location>:/project <docker id>
```
The container will terminate automatically after the tests are completed.

Your nightwatch.json must specify the no-sandbox option for Chrome to cleanly run inside Docker :

```
exports.config = {
    // ...
     "test_settings": {
        // ...
        "desiredCapabilities": {
            "browserName": "chrome",
            "marionette": true,
            "chromeOptions": {
                "args": [
                    "no-sandbox"
                ]
            }
        }
        // ...
    }
    // ...
};
```
