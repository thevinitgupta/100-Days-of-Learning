# Building Lynkit ⛓ - Implementing a Custom Error Handler Middleware
Errors are common in applications and before building a complex application, we should have `Error Handlers` in place. 
So, I decided to create a Custom Error class that works according to my needs. 

As we have seen in my Extending the Request Object writeup, Typescript makes it quite easy to create and use custom types and interfaces. Similarly, it provides Class implementations.

## The Old Way of Handling Errors
Whenever there is an error occurring in the server, unless you have a custom error handler, Express.js provides a way to catch the error.

We can send a response to the client with the error message using its default error handler. 

> ### 📌 The reason Express.js is eager to catch all errors is not only handling properly the errors, but also to correctly empty out unused resources after the application starts running again.

The simple way to handle errors is to catch the errors in the controller functions and send them to the Client side with the error codes.

The way to do this is :

<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/01c40f3e-227e-4952-b3a5-1d304cd30acb" height="350px" />
</p>

### But this is not a good practice because of the following 2 reasons : 
1. `Redundant` code for error responses.
2. Too long error messages that are `not User Friendly`.

## Custom Error Handler Class
With a custom class, we can `select what messages to receiv`e and also `specify different types of error` for better scopes to display it.

Now, since ES6 introduced classes, it has become really easy for custom types since we can follow the age old and tested : `Class Based Object Oriented Programming` for custom data.

As for Lynkit, I decide to have the following properties to help me handle error properly in the client side : 
- status
- message
- type
- additionalInfo

For type, we can broadly classify the Errors from a server into the following : `type ErrorType = 'Validation Error' | 'Server Error' | 'Database Error' | 'Credential Error';`

Then we create a class `CustomError` in a file : `src/models/custom-error.model.ts` : 

<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/e20108ed-e740-40a8-b264-531c43778688" height="350px" />
</p>

## Using the above Class 
Now that our custom class is ready, it is now time to implement the error handler.

> In Express, the Error handler middleware takes in 4 arguments, the first one being the `Error` middleware and the rest being : `Request, Response and Next calling function`.
> This is done so that when a `next(xyz)` call is made with any data, it calls the Error middleware skipping the others.

So, we define the handler as follows : 


<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/2992ccd7-21b4-4298-9a40-e8fa1fc5fbbb" height="350px" />
</p>

We can have errors that have not been thrown by the code, so we need to handle those separately as I have done in the else condition above.

And then we need to use it in the app : 
```ts
app.use("/", router);
// define the error handler after all other middlerwares
app.use(errorHandler);
```

## Throwing errors from the Code
Our Error Handler Middleware will catch all the errors thrown in the code and return the response as needed. So an example of using it is as follows : 
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/c943cffb-227e-4dc1-a9ed-79111d5a6a2f" height="350px" />
</p>

### And there you have it - your custom error handling class and middleware that you can configure based on your needs
