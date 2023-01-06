# cypress-browserstack
To run Cypress test with BrowserStack

Step 1: Install the BrowserStack CLI. The BrowserStack - Cypress CLI is a command-line tool that is used to enable communication between Cypress and BrowserStack. Use the npm command to install the BrowserStack - Cypress CLI as follows:

Command Line
# Install the BrowserStack Cypress CLI
npm install -g browserstack-cypress-cli

Step 2: Clone the Kitchen Sink app using the following command:

Cypress v10
Cypress v9
# Clone the Kitchen Sink repo
git clone https://github.com/cypress-io/cypress-example-kitchensink.git && cd cypress-example-kitchensink


After you clone the repository, the Cypress project will be in the following structure:

Cypress v10
Cypress v9
app
...
cypress
|-- fixtures
|-- e2e
|-- support
cypress.config.js
...

Step 3: Use the npm command to install dependent node modules required to run the Kitchen Sink example app:

Command Line
npm install

Step 4: Create and configure the browserstack.json file which contains configurations, such as BrowserStack credentials, capabilities, etc., that are required for running the tests. Use the following init command to initialize the app project folder and create a boilerplate browserstack.json file:

Command Line
browserstack-cypress init

After the browserstack.json file is created, modify or add the mandatory configurations that are required to run the Cypress test as shown in the following sample code. The mandatory configurations are BrowserStack credentials, Cypress configuration file, browser-device combinations, and the number of parallels:

Note: Check out the supported devices and browsers to configure the testing combinations.
Cypress v10
Cypress v9
// browserstack.json

{
  "auth": {
    "username": "lasithawijenayak1",
    "access_key": "W2cfhwy7so5wkZFspGyi"
  },
  "browsers": [{
      "browser": "chrome",
      "os": "Windows 10",
      "versions": ["latest", "latest - 1"]
    },
    {
      "browser": "firefox",
      "os": "OS X Mojave",
      "versions": ["latest", "latest - 1"]
    },
    {
      "browser": "edge",
      "os": "OS X Catalina",
      "versions": ["latest"]
    }
  ],
  "run_settings": {
    "cypress_config_file": "./cypress.config.js",
    "cypress_version": "10",
    "npm_dependencies": {
      "npm-package-you-need-to-run-tests-1": "^1.2.1",
      "npm-package-you-need-to-run-tests-2": "^7.1.6-beta.13",
    },
    "project_name": "Cypress Kitchen Sink Example",
    "build_name": "Build no: 1",
    "parallels": 5,
    "exclude": ["some-folder/test.js", "static/*.pdf"],
}

Important: If you are using any external npm packages in your Cypress tests, add those under npm_dependencies in the browserstack.json file.
Step 5: Set up the application server. The Kitchen sink sample app can be tested on BrowserStack using either the localhost website or using Cypress Kitchen Sink sample app public URL.

Test using public URL
Test using localhost
If you want to run the Cypress test using the Kitchen Sink web app hosted publicly at https://example.cypress.io/, you must replace all localhost URL instances with the public URL in the project folder.

Step 6: In your IDE, open the Kitchen Sink App project.

Step 7: Search the project for http://localhost:8080, and then replace all instances with https://example.cypress.io as shown in the following IDE sample:Cypress kitchen sink replace localhost

Ensure that you replace the instances in all *.spec.js files.

Step 8: Set the following Local configurations to the connection_settings object in your browserstack.json file:

  //browserstack.json
  ...
  "connection_settings": {
          "local": false,
      }
  ...

Step 9: Run the test using the following command:

Command Line
browserstack-cypress run
