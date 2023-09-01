# Building Lynkit - Creating Custom Request Types for Express Server Requests
Express provides a default `Express.Request` type that can be used in building powerful servers. 

Request is an interface that includes the following : 
 - ReqBody
 - ReqQuery
 - ReqParams

But when you are developing a complex application, you need to add different properties to your Request Objects. This is where the age old practice of extending Data Types come in.

For example, I want to `Authorize` requests using JWT in Lynkit. For that I added a `SessionToken` for the requests that need authentication. 
And then to check : `if the client making the request is Authorized or not` I added a middleware that verifies the Tokens. 

When the token is verified, you will need to decode the token before every request, and put in the decoded data somewhere.

> In Javascript, it would have been a simple effort to add an additional property to the request object, as it does not need to strictly follow a certain interface.

### But the story is differet in Typescript 👇
<img src="https://plusreturn.com/wp-content/uploads/2022/02/T8JO8VpD9y.gif"/>

## Our Express App Setup
#### If you have been following me, I have setup the app to receive Requests as follows : 
- Register User and then allow them to login
- Successful Login generates a Session Token using JWT that hashes and stores the following details :
  ```js
  {
     "email": "tthevinitguptaaawa@gmail.com",
     "name": "Vinit Gupta",
     "_id": "64ef2d863c4b2c55efb90590",
     "__v": 0
  }
  ```
- The token is stored in the User's `cookies🍪`
- A Middleware to verify the user's token and extract the details.

The next thing, I had to do was to pass the above extracted details to the `Request Handler` function.
The natural way to to this is to attach the user data to the Request Object. But Request object does not have a User property by default. 

After a lot of headaches, I was able to find 3 ways to accept the user details and let's discuss about it from the worst to the most elegant and `typescript suggested` way.

## 1. Adding in the Callback function itself
The simplest way to add a custom data in any argument is to use the  `& any` syntax. This appends a `user` field in the Request object with the `any` data type : 
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/71a2e4ff-4e10-4010-a6bf-cfa7b0313520" height="350px"/>
</p>


> [!important]
> Use of the above method not recommended

## 2. Local Custom Type
Another way to solve the problem of custom request type is to extend the Request locally as a type.
This ways since it can be defined in the same file we need to extend the `Request Object` in.
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/d26df4a4-49be-4af3-bb2a-cc92620e6ee8" height="350px"/>
</p>

This works, but is a tedious approach as you have to do this for every file that you need the extension to be.

## 3. Extend the request interface to the entire app (BEST Approach)
The Express types provides us the functionality to extend the Globally declared `Express` namespace that contains the `Request interface`. 
This is really a powerful feature and can be used to extend the Express namespace globally (called Augmentation).

The steps are really simple : 
- Create a file with the following extension `*.d.ts`, which are called `Declaration files` and are used to define types. (For best approach, create a folder called `src/types/` and define all the separate types inside this
- We will add the `user` data to the interface, so we name it : `user.d.ts`
- Then we create a user interface :
```index.ts
  interface IUser {
    name: string;
    _id: ObjectId;
    email: string;
  }
```
- Declare a global namespace with the same name as the one you want to extend. This adds on to the already defined one(Augmenting) and add the above defined interface.
```user.ts
declare global {
  namespace Express {
    interface Request {
      user: IUser;
    }
  }
}
```
And now you can use this in multiple places inside your apps.

<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/82bfe067-8f28-4678-b64d-047d6af39ff4" height="350px"/>
</p>


> You can also add other types as per you usage and also declare generic types to extend the capabilities further.

