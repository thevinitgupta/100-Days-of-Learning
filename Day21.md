# Building Lynkit - Logging in a user and generating a session token using JsonWebTokens
Now that the user is registered and user data is stored in the database securely 🔐, the next step is to let a user login using their email and password.

For authentication a user everytime they login, a `sessionToken` is generated and stored in the user's `cookies`, which will be passed from the front end everytime a request is made.


![Login Workflow](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/48e07ac1-a9d5-4f29-a177-b36e06380a3d)

## Tokens using Json Web Tokens
Json Web Tokens or JWTs are a standard way of authenticating a user by signing their details using a secret key and then hashing it.

In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

- Header
- Payload
- Signature

Therefore, a JWT typically looks like the following.

`xxxxx.yyyyy.zzzzz`

For creating a JWT token, we define a function in `authentication.ts` file in the utils folder : 
```auth.ts
// jwt token generator
export const generateJWTToken = async (user : object) => {
    const jwtSecret = process.env.JWT_PRIVATE_KEY;

    try {
        const jwtToken = await jwt.sign(JSON.stringify(user), jwtSecret);
        return jwtToken;
    } catch (error) {
        if(error instanceof JsonWebTokenError ){
            throw new Error("Error Creating token");
        }
        else{
            console.log(error);
        }
    }
}
```

Now that the utility function is ready, the next step is to use it in the login controller function.

## Login Controller
- **Retrieve User Data:**
  Extract the email and password from the request's body.
  If either email or password is missing, send a 400 Bad Request response with a message indicating missing fields.

- **Validate Email:**
  Use the validateEmail function to check if the provided email is valid.
  If the email is invalid, send a 400 Bad Request response with an "Invalid Email" message.

- **Find 🔎 User in Database:**
  Use the userModel to search for a user with the provided email.
  If no user is found, send a `400 Bad Request` response with a "Email does not exist" message.

- **Check Password:**
  Extract the salt from the user's stored authentication data.
  Hash the provided password using the maskPassword function with the user's salt.
  Compare the hashed password with the stored hashed password. 🔐
  If the passwords don't match, send a 403 Forbidden response with an "Invalid Password" message.

- **Generate Token and Set Cookie🍪 :**
  If the password is valid, create a user data object  🚨 excluding the authentication details.
  Generate a JSON Web Token (JWT) using the generateJWTToken function.
  Set the JWT as an HTTP-only cookie named `lynkit-token`.

- **Redirect User:**
The user is Redirected to the `/user` route to indicate a successful ✅ login.

```login.ts
 async (req : Request, res : Response) =>{
        const {email, password} = req.body;
        if(!email || !password) {
            return res.status(400).json({
                message : 'Email or Password missing'
            });
        }
        if(!validateEmail(email)){
            return res.status(400).json({
                message : 'Invalid Email'
            });
        }
        try {
            const user = await userModel.findOne({email});
            if(!user){
                return res.status(400).json({
                    message : 'Email does not exist'
                });
            }
            else {
                const salt = user.authentication.salt;
                const hashedPassword = maskPassword(salt, password);
                if(hashedPassword!=user.authentication.password){
                    return res.send(403).json({
                        message : "Invalid Password"
                    });
                }
                const userData = {
                    ...user.toJSON()
                };
                delete userData.authentication;
                const token = await generateJWTToken(userData);
                res.cookie("lynkit-token",token, {
                    httpOnly : true
                });
                console.log("cookie Set")
                return res.redirect("/user")
            }
        } catch (error) {
            console.log(error);
            return res.status(500).json({
                message : error.message
                });
        }

    }
```

