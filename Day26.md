# Building Lynkit 🔗 - The Lynks Functionality
Lynkit is basically a URL Shortner, so the most important part of this web app is to `create short links for larger ones`. 
To achieve this, we can adapt 2 one of 2 methods : 
- Hash the Original Link directly.
- Create a `short UID` for each link.

I decided to go for the `short UID` method simply for the fact that hashes can be long and it will destroy the main functionality of the app. 

> [!IMPORTANT]
> I have plans to implement caching in the future, so I added a `Click Count` field in the `Lynk Document`.

## Lynk Schema
I designed the Lynk Schema to hold important information : 
- The User ID of the user who create it.
- The Original Link to redirect from the Link
- Short URL to match the Slug of the URL
- Click Count for caching and analytics
- ####  Set the Timestamps option to true to include the CreatedAt and UpdatedAt fields provided by MongoDB
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/417207a7-235a-41a8-8a14-b8742f02f004" height="450px"/>
</p>

## The Shortner
For creating the short version of the link, I decided to use the [Nanoid](https://npmjs.com/nanoid) library in NPM to create Unique, Short IDs for each URL entry.

NanoID provides an Async NanoID generator and an option to provide the length of the ID we need.

 - Install the `nanoid` library from using the following command :
```js
$ npm install nanoid@^3.0.0
```
- Create a new file in the `src/utils` folder called : `shortUrl.ts`
- Add the following code :
```ts
import { CustomError } from "../models/custom-error.model";
import {nanoid} from "nanoid/async"


export const shortUrlGenerator = async (size: number = 7): Promise<string> => {
  try {
    const shortUrl = await nanoid(size);
   return shortUrl;
  } catch (error) {
    console.log(error);
    throw new CustomError(
      "Error creating Short URL",
      500,
      "Server Error",
      null
    );
  }
};

```
> Note 📌 : The line : `size : number = 7` specifies that the function takes in a size argument of type number with default value 7 if not passed
###  If you don't understand the line `throw new CustomError()`, check out my previous blog here : [Custom Error 🚨 Handler](https://thevinitgupta.netlify.app/100DaysofLearning/Day25)

## The Lynk Controller
Now, that our model and the utility function is ready, we need to create a file to handle the requests.
- Inside the `src/controllers` folder create a new file called :
  ```js
  lynk.ts
  ```
- For now, we will add 2 controller functions :
  ```ts
  - create // this adds a new link
  - getUserLinks // gets all the lynks created by the logged in user
  ```

  ### Create function
  The Create Function is used to add a new Lynk document. It works in 3 steps :
  - #### Extracts user `email` and `_id` and checks if the User trying to add a new link is a valid user, if not throws an Error
  ```ts
  const {email, _id, name} = req.user;
  const user = await (await UserModel.findById(_id, {authentication : false})).toJSON();
  if(!user){
    throw new CustomError(`User does not exist`,403,'Credential Error');
  }
  ```
  - #### Extracts the original link from the `req.body` object and creates a `shortID` for the same :
  ```ts
  const {link} = req.body;
  const shortLynk = await shortUrlGenerator(7);
  ```
  - #### Creates a new Lynk Doc and stores it in the Database
```ts
const lynk = new LynkModel({
      userId : user._id, 
      shortLynk,
      originalLynk : link,
});
const savedLynk = await lynk.save();
```
### The complete code : 
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/7815d1eb-711a-472b-863f-a7af021a2015" height="450px"/>
</p>

## Adding it to the Router
Now that the controller is created, add the routes to create a new Lynk.
Follow the previous blogs to create a new router file and a new router object with the controllers. 

The complete code : 
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/10a77f99-2559-425c-9688-4c461befd773" height="450px"/>
</p>

> ![NOTE]
> I have added the `jwtHandler` middleware above to extract the `user` info from the `JWT Token`. You can also read about this the previous blogs.

### The First Lynk document looks like this : 
<p align="center">
<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/d936ac4a-e2b2-4611-826c-e7ea7a89e74c" height="450px"/>
</p>

Now, we will move to the front end of the application.
