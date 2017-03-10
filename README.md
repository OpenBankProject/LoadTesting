# LoadTesting

Load testing scripts to run against Open Bank Project

## Tool

Artillery (https://artillery.io) is used for the load testing.

## Using Artillery

Artillery is written in Node.js (but you don’t need to know Node or JS to use it). Grab the appropriate package from 
nodejs.org or install Node.js with your favorite package manager first. Note: Artillery requires Node.js 4 or higher 
(Node.js 6+ is recommended).

Once Node.js is installed, install Artillery with:

    npm install -g artillery

To check that the installation succeeded, run:

    artillery dino

If you see an ASCII dinosaur, the installation has been successful!

## Run a quick test

Artillery has a quick command which allows you to use it for ad-hoc testing (in a manner similar to ab). Run:

    artillery quick --duration 60 --rate 10 -n 20 https://experimental-api.openbankproject.com/

To create 10 virtual users every second for 60 seconds which will send 20 GET requests each.

## Run a test script

Scripts are written in YAML. The load testing scripts have two main parts to them - config and scenarios.

In our tests we simulate a user trying to get their transaction details from the OBP api. In the test script you might 
want to change the token and the URL for the transaction accordingly.
 
The test has three phases:

1. Create 10 virtual users every second for 3 minutes (WARM UP)
2. Ramp up to 50 virtual users a second over another 3 minutes
3. Run at 50 virtual users a second for 25 mins

To run the test script, cd to the directory which has the test script and issue the command:

    artillery run obploadtest.yml
    
## Reading the outputs

While the test is running, intermediate stats will be printed every 10 seconds (by default) and a complete report will 
be printed at the end of the test. To understand the details of the report, please refer to this page 
https://artillery.io/docs/gettingstarted.html#reading-the-output.

It is also possible to generate a graphical report using the following command:

    artillery report artillery_report_20170309_124264.json
    
Here you should replace the file name with the one the test generated for you.

This will generate an html file of the report and display it on your default web browser.




