# Building Lynkit - Integrating the Frontend with Backend
For the last 4 days, I have taken 2 days off and the rest 2 days I have working on design of Profile section of frontend and Integrating the Frontend with Backend.

## Profile Section
For the profile section, I took inspiration from the `Github UI` and provided the following functionalities : 
- Update Profile Photo(🚨 This needs to be added to the backend)
- Update Password and Name
- Email Verification (This also needs to be added to backend)

![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/5e129b71-0f06-4db4-9037-c4a2a6172e9e)

The Lynks created by the users can also be viewed along with the `number of clicks` on each lynk : 

![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/ccef4fd9-da3a-42a6-9214-1932cdb5e715)

## Frontend Integration
This is one the most important part of the development process. 
The steps that I followed are explained in this 👉 [Youtube Video 🧠](https://www.youtube.com/watch?v=a5Krfkfl9MM)

I have connected the login functionality so far. The login process works as follows : 
![Login](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/5c2e82cc-65ef-4341-8a46-6b2140e9c3bb)

There are a few important configurations that need to be done for a secure cookie storage. Also, we need to configure the `CORS` policy. 

### CORS setup
```tsx
app.use(cors({
    credentials : true,
    origin : "http://localhost:5173"
}));
```
The origin specifies the base URLs to be allowed to access the resources.

### Issue with storing Tokens in Cookies
Cookies, just like any other client resource can be accessed by any external JS Scripts. This makes storing the `JWT Tokens` a potential issue. 
```js
document.cookies
-> {"lynkit-toke" : "3dvshr4hsggs-=3gsghfsnin94werfds"}
```
### To resolve this there are mainly 2 solutions 
#### 1. Delete the tokens after every session : 
This is not good for User Experience, since this will cause the user to login every time he/she closes their tab.
And since it is stored in `session-storage`, it can still be accessed by external script when the user logs in.

#### 2. Make the Cookies unreadble by external scrips ✅✅
This is the recommended method, as this solves the above issue and the user does not get logged out everytime.

But how do we do this??

### Securing Cookies using the `http-only` flag 🚩
When a cookie is set with the httpOnly flag, it tells the browser that this cookie should not be accessible via client-side scripts. The browser enforces this by ensuring that the cookie is only sent to the server with HTTP requests and is not exposed to JavaScript running on the client side.

> [!Important]
> `httpOnly` flag can be set on the server only while sending the cookies.

The code looks like this : 
```ts
res.status(201).cookie("lynkit-token", token, {
  httpOnly: true,
  expires : new Date(new Date().getTime() + 30*24*60*60*1000)
}).json({
  message: "Loggin Successful",
  });
```
I have set the `expires` property to be 30 days. This is also recommended for secure websites.

Once this is done, we also need to set credentials as `true` while sending requests from `axios` or `fetch`.
```tsx
const { data, status } = await axios.post("http://localhost:3003/auth/login", body, {
        headers: {
          'Content-Type': 'application/json'
        },
        withCredentials: true,
      });
```

### The result looks somethig like this : 
![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/765ab848-bc5e-41ff-a971-8d665a4860fd)
