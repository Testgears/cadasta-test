# cadasta-test

#### This repository contains Selenium UI automated test scripts that can be run against a cadasta server.

#### To install the dependencies :

`pip install -r requirements.pip`

#### To configure geckodriver (This is required if you run the tests with firefox version > 48):

 Geckodriver is the new Selenium driver shipped with Firefox 48+ <br/>
 But there are some test cases in cadasta-test which require the Firefox version to be lower than 48. <br/>
 The reason for this is, we use Python Selenium Action classes in some test cases of cadasta-test, <br/>
 but as per [1]W3C Actions API is not yet implemented in geckodriver. <br/>
 [1] https://github.com/mozilla/geckodriver/issues/159 <br/>
 [2] https://github.com/facebook/php-webdriver/issues/359#issuecomment-262073021 <br/>
 So, it is recommend to run tests on Firefox version < 48 until the above[1] is supported by geckodriver. <br/>

If you are running with newer version of firefox (48+) some tests will fail since the geckodriver doesn't support[1].

`Download from https://github.com/mozilla/geckodriver/releases
Unzip it and add to PATH variable`

#### To configure chromedriver (If you run the tests with chrome):

`Download from https://sites.google.com/a/chromium.org/chromedriver/downloads
Unzip it and add to PATH variable`

#### To run the tests :

You can run the Selenium test by executing one of the below two commands. If you give `./runtests` without giving a
server url, the default url http://localhost:8000 will be considered as the server url.

`./runtests`

`./runtests <server-url>`


### Cleaning the Cadasta DB in a local setup

In case if you need to run tests on a local setup with a clean DB, please follow these steps.
 
 Log into VM using `vagrant ssh`. Now you are inside the VM.
 
 Then drop the DB and recreate it using following commands.
 
 `sudo -u postgres psql`
 
 `drop database cadasta;`
 
 `create database cadasta with owner cadasta;`
 
 Type `\q` and then press `ENTER` to quit psql
 
 Now run following Django management commands
 
 `./manage.py migrate`
 
 `./manage.py loadstatic`
 