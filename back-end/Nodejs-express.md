
# Build a backend using Express.js (Node.js) Windows 10, Node 12.x

### The components of the API
#### 1. Express it self to start serving (receive request, sending response)
#### 2. Route to handle different HTTP methods in distinguished URL
#### 3. Middleware to process the request and response


### Building process
#### 1. Create the directory of your project
Typing ***`mkdir <YOUR PROJECT NAME>`***
For example, I want to use a name of `node-express-api` then I can type ***`mkdir node-express-api`***
Then go to the folder using ***`cd node-express-api`***
```powershell
PS > mkdir node-express-api
PS > cd node-express-api
```

#### 2. Generate a nodejs package.json file
Typing ***`npm init`*** command in powershell, and it may 
require you to input some of the values as follow.
```powershell
PS > npm init                                                 
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (express-api)
version: (1.0.0)
description: Backend API using nodejs expressjs
entry point: (index.js) server.js
test command: start
git repository:
keywords: express API
author: Nathan Yang
license: (ISC)
About to write to ~\package.json:

{
  "name": "express-api",
  "version": "1.0.0",
  "description": "Backend API using nodejs expressjs",
  "main": "server.js",
  "scripts": {
    "test": "start"
  },
  "keywords": [
    "express",
    "API"
  ],
  "author": "Nathan Yang",
  "license": "ISC"
}


Is this OK? (yes) yes


   ╭────────────────────────────────────────────────────────────────╮
   │                                                                │
   │      New patch version of npm available! 6.14.2 -> 6.14.4      │
   │   Changelog: https://github.com/npm/cli/releases/tag/v6.14.4   │
   │               Run npm install -g npm to update!                │
   │                                                                │
   ╰────────────────────────────────────────────────────────────────╯

PS>                                                                                                                             
```
#### 3. Install Express.js
Simply typing ***`npm install express`*** or ***`npm i express`***
```powershell
PS ~\node-express-api> npm install express                                      npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN express-api@1.0.0 No repository field.

+ express@4.17.1
added 50 packages from 37 contributors and audited 126 packages in 2.267s
found 0 vulnerabilities

PS ~\node-express-api> 
```
This means we had installed the express dependencies into your project folder.
You can check it by typing ***`dir`***
```powershell
PS ~\node-express-api> dir                                                      

    directory: ~\node-express-api


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        2020/4/13      6:50                node_modules
-a----        2020/4/13      6:50          14287 package-lock.json
-a----        2020/4/13      6:50            311 package.json


PS ~\node-express-api>   
```
You can see the folder ***`node_modules`*** was added. It contains all the dependencies you installed with ***`npm`***
#### 4. Build the minimum api
##### 4.1 Create the `server.js` file as it has described in the `package.json` file (entry point)
```powershell
PS > touch server.js
PS >
```
##### 4.2 Edit the `server.js` file using Visual Studio Code
```powershell
PS > code server.js
PS >
```
Add content to `server.js` like this
```javascript
// import express package that we need
const express = require('express')

// create the app instance of express
const app = express()

// the simplest route responding HTTP GET method
app.get('/hello', (reqest, response) => {
    response.send('Hello World!')
})

// the code that really starts the app server
// the 8000 means the port the app server is listening
// Locally the server is running on http://localhost:8000/
app.listen(8000, ()=>{
    console.log('Server is running...')
})
```
#### 5. Run it and use browser to see result
Typing `node .\server.js` and enter
```powershell
PS > node .\server.js
server is running...
```
Open your browser and go to `http:\\localhost:8000\hello`
You will see
```chrome
Hello World!
```
# TO BE CONTINUED...
