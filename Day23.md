# Building Lynkit - Middlewares for Authenticating Routes
When building powerful `APIs`, we need to have certain functions that are run before evaluating the data for particular routes.
This is where `Middlewares` come in. 

![Middlewares in REST APIs](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/06ebfd5b-7cd3-4ffd-8920-dd0b61f339da)


## What are Middlewares?
Middlewares are functions that `have access` to the `request (req), response (res), and the next function` in the Express.js application stack.
> They can modify request and response objects, end the request-response cycle, or call the next middleware in line.

Middlewares are `executed in the order` they are defined.

### Example Scenario
Suppose you're building a simple application to log requests.

```javascript
    // Custom middleware
    const logMiddleware = (req, res, next) => {
      console.log(`Request received at ${new Date()}`);
      next(); 
    };
    // Apply the middleware to all routes
    app.use(logMiddleware);
```

In this example, logMiddleware logs the timestamp when a request is received.

### Using the Middleware:
With the middleware applied, every `incoming request will trigger the logging middleware` before moving to the actual route handler.

### Applying Middlewares
In ExpressJS, use app.use(middleware) to apply middleware to all routes.
**For Specific Paths** : Use app.use(path, middleware) to apply middleware to specific routes.
    Middlewares can also be applied locally to a specific route using the .use method.

## Authentication Middleware in Lynkit
In Lynkit, the profile route should only be accessible to users with a `valid JWT Token`. 
For this reason, we need to check for the validity of token even before searching for it in the database.
> There are 2 steps for implementing this : 
> 1. Extract the token from Request and verify.
> 2. Extract the user data from Token and pass to the next middleware or Request handler

For this create a separate file inside a `middlewares` folder in `src` and add the following code : 
```jwt.ts
const jwtAuthHandler = async (req : Request, res : Response, next : NextFunction) => {
    const token = req.cookies["lynkit-token"];

    const secret =  process.env.JWT_PRIVATE_KEY;

    try {
        const user = await jwt.verify(token, process.env.JWT_PRIVATE_KEY, { algorithms: ['HS256'] });
        if(!user){
            return res.status(400).json({
                message : "Invalid Credentials"
            });
        }
        req.user = user as IUser;

        next();
    } catch (error) {
        console.log(error);
        res.clearCookie("lynkit-token");
        return res.status(500).json({
            message : "Please login again"
        });;
    }
}

export default jwtAuthHandler;
```
You can lookout for the following in the code above : 
- The `token` that was added in the `login-handler` as cookie, is being extracted from the request.
- The `token` is then being verified using the `PRIVATE_KEY` store in the `.env` file by specifying the algorithm.
  > 🚨 Note here that the correct algorithm is very important, otherwise the `jwt.verify` throws an `error if the encryption does not match`.
- If the user is not present in the request, we send the response as `Invalid Credentials` without even needing to search in the database.
- The `next()` function calls the next middleware or request handler as required after adding the `user` to the `Request Object`.

In the next edition, we will see how to modify the already defined `Request` object in `express types module` to include user as well.

