![GitHub package.json version](https://img.shields.io/github/package-json/v/thzero/rocket_tools-server)
![David](https://img.shields.io/david/thzero/rocket_tools-server)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# rocket_tools

An API layer to manage rocket tools.  The following features are available currently

* Social login authentication via Google

## Project setup

The server application is a Fastify server application.  The server application provides the API for use by the companion client application (https://github.com/thzero/rocket_tools-client).

### Requirements

#### Mongo

Mongo is required as the server side data source.

* Install the MongoDb (either locally or in the cloud) server
  * Recommendation is MongoDb Atlas (https://www.mongodb.com/cloud/atlas) for development/sandbox
* Create a new MongoDb database in the Mongo server
* Restore the default rocket_tools MongoDb
  * Use the following MongoDb CLI tool to restore the default database located at (https://github.com/thzero/rocket_tools-database)

```
.\bin\mongorestore --host <mongodb host name> --ssl --username <mongo user name> --password <mongo user password> --authenticationDatabase admin -d production <location of default database>
```

Recommended tools for managing Mongo database
* MongoDb Compass (https://www.mongodb.com/products/compass)
* Robo3T (https://robomongo.org)

#### Firebase

Google Firebase (https://firebase.google.com) provides the social based authentication; currently only Google social accounts are supported.

* Add a new project
* Setup **Authentication**, enabled Google in the **Sign-in method**.
* Get the Firebase SDK configuration
  * Go to Project Overview->Settings->Service accounts
  * Select **Node.js** option
  * Click **Generate new private key**

#### Configuration

* Setup the configuration found in the config\development.json
  * Note that this is ignored in the .gitignore
* Configuration looks like the following

```
{
    "app": {
        "auth": {
          "apiKey": "<generate a GUID as key in standard nomeclature '#######-####-####-####-############'>",
          "claims": {
            "check": false,
            "useDefault": false
          }
        },
        "cors": {
            "origin": "*"
        },
        "db": {
            "atlas": {
                "connection": "<mongo connection string>",
                "name": "<environment name>"
            }
        },
        "logging": {
            "level": <see https://github.com/pinojs/pino/issues/123 for logging levels>,
            "prettify": <true of false if you want prettify, if true requres 'pino-prettify' as a dependency>
        },
        "port": <port to run the server on>
    }
}
```

#### NPM Dependencies

Install the NPM dependencies for the client.

```
npm install
```

Other global dependencies required

```
npm -g i nodemon
```

#### Submodules

Install the submodule dependencies for the client.

```
git submodule add https://github.com/thzero/rocket_tools-common "common"
```

### Compiles and hot-reloads for development

#### NPM CLI

Run the application server locally in debug mode with hot reloading via Nodemon.

```
npm run debug
```

#### Visual Code

Install VisualCode, open the 'server' folder via 'Open Folder'.

Using the Menu->Run->Start Debugging will launch the application in debug mode with hot reloading via Nodemon
