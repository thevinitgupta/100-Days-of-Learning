# Building Lynkit - URL Shortener Day 1 : Setting up ExpressJS Server with Typescript
Lynkit will be a full stack URL shortener application built using `ReactJS, NodeJS, Typescript, MongoDB and Redis` for caching.

The first step is building the REST API using ExpressJS with Typescript and MongoDB.

## Setup for ExpressJS to use Typescript
 - Create a new folder and run : 
```js
npm init -y
```
This initialized an npm respository with default options. 

 - Next, step is to install the necessary dependencies to run Typescript.
> 📌 The dependencies needed for running Typescript will only be needed during development, so we will install them as `DevDependencies` using the following command :
```js
npm install -D typescript nodemon ts-node
```

When these are installed, we need to configure the environment.

- Next, we need to configure typescript, so create a new file : `tsconfig.json` in the root directory and add the following :
  ```json
  {
    "compilerOptions" : {
        "module": "Node16", //Specifies the target module system - ensures generated code is compatible with Node.js
        "moduleResolution": "node", // Determines how compiler resolves module imports - uses Node.js resolution strategy
        "baseUrl": "src", // sets the base directory for module resolution
        "outDir": "dist", // generated JavaScript files will be placed in the dist directory
        "sourceMap": true, // Source maps enable browser debugging of transpiled TypeScript
        "noImplicitAny": true // throws an error if TypeScript cannot determine the type of a variable
    },
    "include": ["src/**/*"] // specifies which files to include in the compilation process, set to include all TypeScript files under the src directory and its subdirectories
  }
```
```
 - Now we need to configure `nodemon` to run with typescript. Create a `nodemon.json` file and add the following code :
```json
{
    "watch" : ["src"], // which folder to watch for changes
    "ext" : ".ts,.js", // which extensions to watch for changes to restart the server
    "exec" : "ts-node ./src/index.ts" // the script nodemon execute
}
```

And there you have it, you are ready to develop your express server in typescript.
