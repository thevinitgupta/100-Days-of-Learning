# Building Lynkit - Day 3 Building the MVC Based Architecture
When building a complex Application, we need to follow one or the other design patterns. The most followed one is the `Model View Controller(MVC)` design pattern.

This architecture separates the `data model in the model section`, the `Frontend application` in the `View section(here the ReactJS Application)` and the `Business logic or request handling` into the `Controller` section. 

## User Model 
The most important part of Lynkit is the user that will store the various links. 
Each user needs to have a unique EmailID, a name and some authentication built in. 
For this we are using the following model : 
```user.ts
import mongoose, { Model, Mongoose, Schema } from "mongoose";

const userSchema : Schema = new Schema({
    email : {
        type : String,
        required : true
    },
    name : {
        type : String,
        required : true
    },
    authentication : {
        password : {
            type : String,
            required : true,
            select : false 
        },
        salt : {
            type : String,
            select : false 
        },
        sessionToken : {
            type : String,
            select : false 
        },
        // this defines that while returning the response, password is not returned
    },
});

export const userModel = mongoose.model("User", userSchema);
```

Also, we need to create a Schema based on the Model to store in our MongoDB database which is handled by `mongoose.model` method where we pass in 2 parameters : 
- the name of the model 👉 `User`
- the actual `schema or design of the document` 👉 `userSchema` that we defined above

Now that we have created the `userSchema`, we need to build the controllers to handle the requests. 

## User Controller
As the first step, we are creating only the - `getAllUsers` endpoint which is defined inside an object called `userController` and can be invoked in the routes when defined.
```userController.ts
import {Request, Response} from "express";
import { userModel } from "../models/user";
import { AuthInterface, UserInterface } from '../types/user';
const userController = {
    get : async (_req : Request ,res : Response )=>{
        try {
            const users : Array<UserInterface> = await userModel.find();
            
            res.status(200).json({
                users
            });
        } catch (error) {
            console.log(error)
        }
    },
    post : (req : Request, res : Response) => {

    }
};

export default userController;
```

Here you can see another import in the 3rd line : `UserInterface and AuthInterface` which is defined as interfaces that will be used to create new objects and add features. 

```userTypes.ts
import Document from "mongoose";
export interface AuthInterface {
    password : string,
    salt : string,
    sessionToken : string
}
// ! Extends Document is required to accept MongoDB documents, others it throws Error
export interface UserInterface extends Document{
    email : string,
    name : string,
    authentication : AuthInterface
}
```

The AuthInterface stores the Authentication requirements. 

## First Request
When the server is started using : ```npm start```, we see the following output : 

![Server Running](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/bbf50163-b780-4d57-975f-9fa43b4bd36f)


And on going to the endpoint : `http://localhost:3003/users/` , we get the following result since we have not added any users yet:

![Enpoint Sample](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/b070a30f-4042-4a11-941d-6bba22a6a0ad)
