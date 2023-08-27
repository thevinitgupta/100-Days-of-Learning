# Building Lynkit - Day 4 User Authentication and Securing Storage
User security is foremost the most important part of any web application. 
But before a User is authorized to use an application, we need to `Authenticated` and that's what I implemented for Lynkit today.

## Before Registering a User
While registering, a user basically needs 2 things : `a unique identifier(here the EmailID)` and a `secure password`.

The frontend application validates both of them and sends a request to the REST API. 

### 💡 A good practice is to Validate the inputs in the Backend even if it has been validated by the frontend.

So, we create a `validator.ts` file in the `utils` folder. It will currently only have the function for validating and email and a secure password : 
```validator.ts
export const validateEmail = (email : string)  => {
    const emailRegex =  /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return emailRegex.test(email);
}

// Conditions : Minimum 8 Characters, Atleast 1 uppercase, 1 lowercase, 1 number and 1 special character from 👉 [@,!,*]
export const validatePassword = (password: string): boolean  =>{
    const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*[@!*])(?=.*\d)[A-Za-z@!*0-9]{8,}$/;
    return passwordRegex.test(password);
}
```

Another thing we need to do is define a function to create a `hash value` from the password before storing.

### Crypto module and hashing the password 🔐
A question might arise here : *Why are we hashing the password for storing?*
For a simple fact : `even if the application is hacked, the hacker won't be able to see the password`

This protects the users from identity theft.

There are several libraries that we can do this with like Crypto, Bcrypt, etc.
For simplicity, we are using the `Crypto` module that comes with the Express Library.

There are 2 things to understand here : `salt` and ` secret-key`. 

Using a salt and a secret key for password hashing is like `adding extra layers of security to protect your passwords`.

### Salt 🧂
Think of a salt 🧂 like a unique ingredient you add to each password before hashing it. Adding a unique salt to each password makes sure that even if two people have the same password, their hashed versions will be different. 
> 📌 This prevents attackers from easily figuring out if multiple users have the same password `just by looking at the hashes`.

For this we use the Crypto module to generate a random string every time a password is added : 
```ts
//randomizer function to generate salt
export const random : Function = () : string =>  crypto.randomBytes(128).toString('base64');
```

### Secret Key 🔑
Imagine you have a special key 🔑 that only you and your trusted friends know about. Similarly, a secret key used in password hashing is a piece of information that only the server knows. It's used to mix the salt and password before hashing. 
```ts
const SECRET = process.env.SECRET_KEY;
```
In summary, using a salt and a secret key makes your passwords more secure by:

**Preventing Same Passwords:** Salting prevents attackers from easily recognizing if two users have the same password just by looking at the hashed values.

**Added Complexity:** The secret key adds complexity to the hashing process, making it much harder for attackers to reverse-engineer the original password even if they have the hashed version.

Combining the above we get a function that generates a hashed password : 
```ts
// masked password generator for storage
export const maskPassword = (salt : string, password : string) : string => {
    return crypto.createHmac('sha256', [salt,password].join('/')).update(SECRET).digest('hex');
}
```
This code creates a secure hash of a combination of salt, password, and a secret, using the SHA-256 algorithm, resulting in a hexadecimal representation.

Now we will use the above validator and hashing in our `signup controller` function.

## Handling user Signup
Since, a `database read/write` takes time to execute, we use an `async` function to add a new user.

A user is added in the following steps : 
 1. The data is extracted from the `Request Body` and checked if present
 2. Data(EmailID and Password) is then validated before storing
 3. The Email is check with previous records to check for `duplicate user creation`.
 4. A `random salt` is generated and the `password is hashed`.
 5. The `user` is saved asynchronously into the database and a confirmation is sent to the user.
> 📌Note : The sessionToken is not created immediately for this use case.

The Signup controller function is as follows : 
```signup.ts
signup : async (req : Request, res : Response) => {
        const { email , name, password } = req.body;
        if(!email || !password || !name) {
            return res.status(400).json({
                message : 'Email/Password/Name missing'
            });
        }
        if(!validateEmail(email)){
            return res.status(400).json({
                message : 'Invalid Email'
            });
        }
        else if(!validatePassword(password)){
            return res.status(400).json({
                message : 'Invalid password'
            });
        }
        //check for existing account with the same email address
        try {
            const userExists = await userModel.findOne({email});
            if(userExists){
                return res.status(400).json({
                    message : 'Email already exists'
                });
            }
            const salt = random();
            const hashedPassword = maskPassword(salt, password);
            const newUser = new userModel({
                email,
                name,
                authentication : {
                    password : hashedPassword,
                    salt
                }
            });
            const savedNewUser = await newUser.save();
            return res.status(200).json({
                message : "New User Created Successfully",
                user : savedNewUser
            }).end();
        } catch (error) {
            console.log(error);
            res.status(500).json({
                message : error.message
            });
        }
    }
```

Do follow ✅✅ for upcoming posts on `User Authorization using JWT` and more.
