# devConnector_v2

Install Packages

* Dependencies *

npm i express express-validator bcryptjs config gravatar jsonwebtoken mongoose request
    * express : our main web framework for the backend.
    * express-validator: for data validation.
    * bcryptjs: for password encryption.
    * config: for global variables.
    * gravatar: for profile gravatars.
    * jsonwebtoken: pass along a token for validation.
    * mongoose: a layer that sits on top of the database so we can interact with it.
    * request: make HTTP requests to another API. (we going to use it for the GitHub repositories)

* Dev Dependencies *

npm i -D nodemon concurrently
    * nodemon: watch our server so that we don't have to refresh it every time we make a change.
    * concurrently: allow us to run our back end Express server and our front end React server at the same time
                    with one single command. 

-------------------------------------------------------------------------------------------------------------------

package.json

change scripts

"scripts": {
    "start": "node server", /* this is the script that Heroku will run when we deploy.*/
    "server": "nodemon server" /* script for development so we don't have to keep refreshing the server
                                  so we 'll run nodemon and the name of the file which is "server"  */
    AFTER we ll have a client script that will run React.
    AND AFTER AFTER a devs script that 'll run both at the same time.
  }


-------------------------------------------------------------------------------------------------------------------

* CONNECT WITH MONGODB *
user: OdysseasAdmin
password: odysseas1991

-------------------------------------------------------------------------------------------------------------------

 * RUN * 

npm run server 
    * starts express server.
    * http://localhost:5000/ or get request POSTMAN to see 

-------------------------------------------------------------------------------------------------------------------

* Interact with database *

We need to create a model for each of our resources.

-------------------------------------------------------------------------------------------------------------------

* User Validation *

We use: express-validator
https://express-validator.github.io/docs/

* Gravatar *
https://www.npmjs.com/package/gravatar

* Bcrypt *
https://www.npmjs.com/package/bcryptjs

* JWT - Json Web Token *
After register a user, we can get a json web token back that has the user id payload.
So after we can send that token back to authenticate an access protected routes.
To do that we going to our own custom middleware.
https://jwt.io/
https://github.com/auth0/node-jsonwebtoken
https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec

-------------------------------------------------------------------------------------------------------------------

* Protect Routes *

We use middleware/auth.js.
Using JWT to verify given token.

-------------------------------------------------------------------------------------------------------------------

* Request dependency *

https://www.npmjs.com/package/request

Example
var request = require('request');
request('http://www.google.com', function (error, response, body) {
  console.log('error:', error); // Print the error if one occurred
  console.log('statusCode:', response && response.statusCode); // Print the response status code if a response was received
  console.log('body:', body); // Print the HTML for the Google homepage.
});

-------------------------------------------------------------------------------------------------------------------

* GitHub API *

go to https://github.com/settings/developers to set up a New OAuth App.


-------------------------------------------------------------------------------------------------------------------
 
React

npx create-react-app client
    *we create a react application in a folder called client

--We don't want to run npm start inside client and after run the server in the back-end.
--So, we'are gonna setup concurrently to do both.

We add some scripts in package.json

"scripts": {
    "start": "node server", /* this is the script that Heroku will run when we deploy.*/
    "server": "nodemon server", /* script for development so we don't have to keep refreshing the server
                                  so we 'll run nodemon and the name of the file which is "server"  */
    AFTER we ll have a client script that will run React.
    AND AFTER AFTER a devs script that 'll run both at the same time.
    "client": "npm start --prefix client", /* it will run it within the client folder */
    "dev": "concurrently \"npm run server\" \"npm run client\""   /* will run both server and the client 
  }

*************************************
*   SO NOW IN ORDER TO START APP:   *
*                                   *
*         npm run dev               *     
*************************************

-----------------------------------------------------

After we need to install some Dependencies in client.

* Dependencies *

npm i axios react-router-dom redux react-redux redux-thunk redux-devtools-extension moment react-moment
    * axios : make http requests
    * redux-thunk: is middleware to allow us to make a synchronous request in our actions
    * moment: time library

------------------------------------------------

*** We also add proxy in package.json in order to be able to make /api/... requests and not http://locahost:5000/api/...
