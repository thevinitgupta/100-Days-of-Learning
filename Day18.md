# Building Lynkit - Day 2 Setup MongoDB and Making our first request
An important part of any software is the Database and for this we will be using `MongoDB`.

> MongoDB is a `NoSQL document based` data storage system that allows us to create `collections(represeting real world objects)` and storing data of each `instance of the object in a document`.

Previously, we setup our project to use Typescript. Now we need to configure MongoDB and Express server before we make our first request.

## Step 1 : Install dependencies
To start developing the REST API, we need to have some basic libraries setup. This includes : 
- `body-parser`: Middleware for parsing incoming request bodies in Express applications.
- `compression`: Middleware for compressing HTTP responses to improve server performance.
- `cookie-parser`: Middleware for parsing HTTP request cookies in Express.
- `cors`: Middleware for enabling Cross-Origin Resource Sharing in Express apps.
- `dotenv`: Library for loading environment variables from a `.env` file.
- `express`: Web framework for building server-side applications using Node.js.
- `mongoose`: ODM (Object Data Modeling) library for MongoDB and Node.js applications.

Run the following command to install each of these : 
```js

npm install express mongoose body-parser compression cookie-parser cors dotenv

```

## Step 2 : Setup MongoDB and Connect
You have 2 options : either to setup a local MongoDB server or use the free Atlas version. 
#### Click on the video below 👇 for a simple guide to setting up the Atlas version that is accessible all over the world : 
[![MongoDB Setup](https://img.youtube.com/vi/RcxdF3Lzoac/0.jpg)](https://www.youtube.com/watch?v=RcxdF3Lzoac)

Once you have setup MongoDB Atlas by following the video above, you will get a connection string that looks something like this : 
```js
mongodb+srv://${process.env.MONGODB_USERNAME}:${process.env.MONGODB_PASSWORD}@lynkit.9z5assyq.mongodb.net/?retryWrites=true&w=majority
```
You might notice `process.env.MONGODB_USERNAME`. This refers to the `.env` file that is used to store environment secrets.
The library `dotenv` helps us access the variables present in the environment file. 

The mongoose library has various methods that helps us setup a connection with MongoDB and also methods that help use CRUD functionalities. 
For now create a folder `src/connections` and add a `db.ts` file. The connections folder will have files that help us connect with other services like `Redis` in the future for caching.

To setup the connection and listen to errors, add the following code in the `db.ts` file : 
```db.ts
import mongoose from "mongoose";

const connectDB = () => {
 const clusterName = "lynkit";   mongoose.connect(`mongodb+srv://${process.env.MONGODB_USERNAME}:${process.env.MONGODB_PASSWORD}@${clusterName}.9z5gfyq.mongodb.net/?retryWrites=true&w=majority`)
    const db =mongoose.connection;

    db.on("error", (error)=>{
        console.error("Error while connecting to mongoose ❌\n", error);
    });
    
}

export default connectDB;
```
Now, that the connection is set, we are ready to accept requests and handle other setup processes.

## Step 3 : Setup the Express Server along with the other dependencies
The next step is configure your app to handle requests. I am not going to bore you with too much details, but following code will help start handling requests. 

- Create a new file in the `src` folder : `index.ts`.
- Add the following code and your app is ready to handling requests : 
```index.ts
import express from "express";
import cors from "cors";
import compression from "compression";
import cookieParser from "cookie-parser";
import bodyParser from "body-parser";
import mongoose from "mongoose";
import { configDotenv } from "dotenv";
import connectDB from "./connections/db";

const app = express();

app.use(cors({
    credentials : true
}));

configDotenv();

app.use(compression());
app.use(cookieParser());
app.use(bodyParser.json());

connectDB();
const db = mongoose.connection;

db.once("open", ()=>{
    console.log("MongoDB connection established!")
    app.listen(3003, ()=>{
        console.log("server listening on port 3003✅✅");
    });
});

```

To understand the libraries used above 👇 :

#### CORS Middleware (cors):
  CORS stands for Cross-Origin Resource Sharing, it means your server is open to exchanging sensitive data, like cookies, with other domains. This is essential when you want to allow authenticated requests from different websites.

#### Compression Middleware (compression()):
  This line introduces compression() middleware. Think of it as a tool that compresses the data your server sends out. It boosts your app's performance and reduces loading times for users.

#### Cookie Parsing (cookieParser()):
  cookieParser() middleware is like having a decoder for cookies. Cookies are small pieces of data stored by websites in your browser. With this middleware, your Express app can read these cookies and understand what they contain.

#### JSON Body Parsing (bodyParser.json()):
  When your app receives data from a client (like a browser), it often comes in JSON format. bodyParser.json() is like a translator. It takes the incoming JSON data and transforms it into something your app can work with.

There you have it, a server ready to accept requests.
