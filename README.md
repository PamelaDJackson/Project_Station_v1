# Project_Station_v1
Sabio Code
# Poor Dawg Application Development Notes

# Server Side
**server.js** acts as the main file or entry point into the application. From here, server.js sets up the necessary configurations such as:

* Serving up static files,
* Handling 404 for static files
* Setting up MongoDB connection
* PassportJS configuration
* Request body parsing and validation
* Registering routes

## App Folder Structure
From here, the /app folder is where most of the server side code lives.  The folder is laid out in a typical MVC like structure with folders for controllers, services and models with an additional folder for routes.  Both the controllers and the services are examples of exporting a contructor function.  This means that any module that wants to _require_ in these modules needs to invoke the module to have access to the functions inside.

### Response Models
Inside of the models/responses folder you will find a set of ES6 classes that allow you to create response objects to send back to your clients.

### Routes
**routes/index.js** is considered the main route file where all routes are to be registered.  Each set of routes will be contained in their own route js file, i.e. api/hackers* routes, would be contained within hackers.routes.js. Each of these route files creates it's own instance of an Express router, which in turn is exported by the file. We can then attach these router instances and their routes to our main router instance inside index.js by requiring the modules.

## Serving static files via Express
To serve static file using express, you need to let express know where those files should be served from.  Using the function express.static, you pass in the name of the directory that contains all your static files.
This starter project serves all static files from the /content directory. To reference these files in your client side code, you only need to prefix /content, i.e. /content/css/style.css.  You can also remove the prefix which would mean you can serve the same css file as /css/style.css.  The fallthrough option makes client errors fall-through as just unhandled requests which allows us to have a 404 handler immediately after our static file serving code.

Reference: https://expressjs.com/en/starter/static-files.html

# Client Side
The client side of this app is powered by React + Redux + React Router. It was originally built using the Create React App and has not been ejected. This app is meant to be a SPA where index.html acts as the parent html file.  Each feature is broken down into its own React container/components (following Dan Abramov's conventions). Containers tend to be more concerned with wiring up data from api/redux, while components tend to be more concerned with visual aspects.

## Modules
The /content/src folder will contain all the react files. There is a index.js file for bootstrapping the app to the html and the App.js which acts as the primary/main module.

`service` folder is for making ajax calls, `config` are modules for configuration, helpers for reusable code throughout, `actions` and `reducers` folders for redux. `theme-scripts` are for scripts that were customized from the theme.

## Routing
There are two components files that control the React Router routes: LayoutRouter and NoLayoutRouter. LayoutRouter is for logged in users' routes while NoLayoutRouter is for users who are not logged in.

## Environment variables
There are two sets of environment variables. One at the root level is for the node app, while the other one at `/content` level is for react app. These .env files are not included in the repo for security reasons.

Reference: https://www.npmjs.com/package/dotenv

# Building for Dev and Production

## Development
API: install nodemon globally and run using  `nodemon` at the root folder
UI: open another shell and run `npm start` at the content folder

## Environment Variables

### Node server
MONGODB_URL=
PORT=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
S3_AWS_BUCKET=
S3_AWS_REGION=
SENDGRID_API_KEY=
HASHER_VALUE=
CLIENT_URL=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
LINKEDIN_CLIENT_ID=
LINKEDIN_CLIENT_SECRET=
WEBSOCKET_PORT_NUMBER=

### React App
REACT_APP_API_URL_BASE=
REACT_APP_ADMIN_DATA_URL=
REACT_APP_MAPS_LAT=
REACT_APP_MAPS_LONG=
REACT_APP_WEBSOCKET_URL=

## Production
For production, run `npm build` inside the `content` folder which will output the static assets into the `content/build` folder. Then the node server will serve the static assets out of that folder.
