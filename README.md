<img width="740" alt="Screen Shot 2024-05-15 at 9 10 07 PM" src="https://github.com/AliceGonzalez/MoneyManagementApp/assets/144973566/f6e6ab8a-f854-475c-a858-ccbc5b94f7c7">
<img width="871" alt="Screen Shot 2024-05-15 at 9 12 35 PM" src="https://github.com/AliceGonzalez/MoneyManagementApp/assets/144973566/73aea307-f2c6-48e0-8f86-75a467591c1b">
<img width="880" alt="Screen Shot 2024-05-15 at 9 20 29 PM" src="https://github.com/AliceGonzalez/MoneyManagementApp/assets/144973566/74f8ebf2-a2fc-4924-a58b-d359af256f8f">
<img width="889" alt="Screen Shot 2024-05-15 at 9 20 59 PM" src="https://github.com/AliceGonzalez/MoneyManagementApp/assets/144973566/32988426-86f9-45c5-b4b4-b9fee8ee4c02">
<img width="1154" alt="Screen Shot 2024-05-15 at 9 10 55 PM" src="https://github.com/AliceGonzalez/MoneyManagementApp/assets/144973566/59adfc40-ee54-46df-b2a0-02a299af63a4">
<img width="881" alt="Screen Shot 2024-05-15 at 9 13 16 PM" src="https://github.com/AliceGonzalez/MoneyManagementApp/assets/144973566/760bf1af-60d9-40e3-b82c-25880a4ffcdc">


Project Structure
Node is required for generation and recommended for development. package.json is always generated for a better development experience with prettier, commit hooks, scripts and so on.

In the project root, JHipster generates configuration files for tools like git, prettier, eslint, husky, and others that are well known and you can find references in the web.

/src/* structure follows default Java structure.

.yo-rc.json - Yeoman configuration file JHipster configuration is stored in this file at generator-jhipster key. You may find generator-jhipster-* for specific blueprints configuration.

.yo-resolve (optional) - Yeoman conflict resolver Allows to use a specific action when conflicts are found skipping prompts for files that matches a pattern. Each line should match [pattern] [action] with pattern been a Minimatch pattern and action been one of skip (default if omitted) or force. Lines starting with # are considered comments and are ignored.

.jhipster/*.json - JHipster entity configuration files

npmw - wrapper to use locally installed npm. JHipster installs Node and npm locally using the build tool by default. This wrapper makes sure npm is installed locally and uses it avoiding some differences different versions can cause. By using ./npmw instead of the traditional npm you can configure a Node-less environment to develop or test your application.

/src/main/docker - Docker configurations for the application and services that the application depends on

Development
Before you can build this project, you must install and configure the following dependencies on your machine:

Node.js: We use Node to run a development web server and build the project. Depending on your system, you can install Node either from source or as a pre-packaged bundle.
After installing Node, you should be able to run the following command to install development tools. You will only need to run this command when dependencies change in package.json.

npm install
We use npm scripts and Webpack as our build system.

Run the following commands in two separate terminals to create a blissful development experience where your browser auto-refreshes when files change on your hard drive.

./mvnw
npm start
Npm is also used to manage CSS and JavaScript dependencies used in this application. You can upgrade dependencies by specifying a newer version in package.json. You can also run npm update and npm install to manage dependencies. Add the help flag on any command to see how you can use it. For example, npm help update.

The npm run command will list all of the scripts available to run for this project.

PWA Support
JHipster ships with PWA (Progressive Web App) support, and it's turned off by default. One of the main components of a PWA is a service worker.

The service worker initialization code is commented out by default. To enable it, uncomment the following code in src/main/webapp/index.html:

<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('./service-worker.js').then(function () {
      console.log('Service Worker Registered');
    });
  }
</script>
Note: Workbox powers JHipster's service worker. It dynamically generates the service-worker.js file.

Managing dependencies
For example, to add Leaflet library as a runtime dependency of your application, you would run following command:

npm install --save --save-exact leaflet
To benefit from TypeScript type definitions from DefinitelyTyped repository in development, you would run following command:

npm install --save-dev --save-exact @types/leaflet
Then you would import the JS and CSS files specified in library's installation instructions so that Webpack knows about them: Note: There are still a few other things remaining to do for Leaflet that we won't detail here.

For further instructions on how to develop with JHipster, have a look at Using JHipster in development.

Building for production
Packaging as jar
To build the final jar and optimize the moneyapp application for production, run:

./mvnw -Pprod clean verify
This will concatenate and minify the client CSS and JavaScript files. It will also modify index.html so it references these new files. To ensure everything worked, run:

java -jar target/*.jar
Then navigate to http://localhost:8080 in your browser.

Refer to Using JHipster in production for more details.

Packaging as war
To package your application as a war in order to deploy it to an application server, run:

./mvnw -Pprod,war clean verify
JHipster Control Center
JHipster Control Center can help you manage and control your application(s). You can start a local control center server (accessible on http://localhost:7419) with:

docker compose -f src/main/docker/jhipster-control-center.yml up
Testing
Client tests
Unit tests are run by Jest. They're located in src/test/javascript/ and can be run with:

npm test
Spring Boot tests
To launch your application's tests, run:

./mvnw verify
Others
Code quality using Sonar
Sonar is used to analyse code quality. You can start a local Sonar server (accessible on http://localhost:9001) with:

docker compose -f src/main/docker/sonar.yml up -d
Note: we have turned off forced authentication redirect for UI in src/main/docker/sonar.yml for out of the box experience while trying out SonarQube, for real use cases turn it back on.

You can run a Sonar analysis with using the sonar-scanner or by using the maven plugin.

Then, run a Sonar analysis:

./mvnw -Pprod clean verify sonar:sonar -Dsonar.login=admin -Dsonar.password=admin
If you need to re-run the Sonar phase, please be sure to specify at least the initialize phase since Sonar properties are loaded from the sonar-project.properties file.

./mvnw initialize sonar:sonar -Dsonar.login=admin -Dsonar.password=admin
Additionally, Instead of passing sonar.password and sonar.login as CLI arguments, these parameters can be configured from sonar-project.properties as shown below:

sonar.login=admin
sonar.password=admin
For more information, refer to the Code quality page.

Using Docker to simplify development (optional)
You can use Docker to improve your JHipster development experience. A number of docker-compose configuration are available in the src/main/docker folder to launch required third party services.

For example, to start a mysql database in a docker container, run:

docker compose -f src/main/docker/mysql.yml up -d
To stop it and remove the container, run:

docker compose -f src/main/docker/mysql.yml down
You can also fully dockerize your application and all the services that it depends on. To achieve this, first build a docker image of your app by running:

npm run java:docker
Or build a arm64 docker image when using an arm64 processor os like MacOS with M1 processor family running:

npm run java:docker:arm64
Then run:

docker compose -f src/main/docker/app.yml up -d
When running Docker Desktop on MacOS Big Sur or later, consider enabling experimental Use the new Virtualization framework for better processing performance (disk access performance is worse).

For more information refer to Using Docker and Docker-Compose, this page also contains information on the docker-compose sub-generator (jhipster docker-compose), which is able to generate docker configurations for one or several JHipster applications.

Continuous Integration (optional)
To configure CI for your project, run the ci-cd sub-generator (jhipster ci-cd), this will let you generate configuration files for a number of Continuous Integration systems. Consult the Setting up Continuous Integration page for more information.

MoneyManagementApp
Demo Day Project

ignore anything from commit bd21a09aad4c92e984882cc64f0c9dab40605632
