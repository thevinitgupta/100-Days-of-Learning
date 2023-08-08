# Day 1 : RESTful - The API that scales

The frontend and backend connect with each other using APIs or Application Programming Interface. 
APIs basically act as a middle man for the client to talk to the server. 

## The Restaurant Analogy 👨‍🍳
A simple way to understand APIs is to visit a restaurant. You are the `customer` that orders the food and the `chef` prepares the food.
But do you walk upto the chef to say what you wanna eat? No, there is a `waiter`.

The waiter takes your order, asks the chef in the back to prepare your food and then brings it back to you. 

The API is the `waiter` here, you are the `browser` or client and the `chef` is the backend server connected to the database. 

## RESTful APIs
REST or `REpresentational State Transfer` is a loose set of rules that is the common standard for building APIs since the early 2000s. 
The rules can be seen below : 
![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/aeb1dea4-f85e-471e-af09-8ef7629d296e)

Common examples include Stripe, Twillio and Google Maps.

REST APIs are defined by a set of URIs(Uniform Resource Identifiers) that differentiate resources and give the frontend the endpoints for getting the required data.

> An important thing to remember is that the resource should be defined by `nouns` and not verbs. For example, the endpoint for getting products should be :
> ```javascript
> https://example.com/api/v2/products ✅
> https://example.com/api/v2/getAllProducts ❌
> ```

## Types of requests and Stateless servers
There are mainly 4 operations on data : `Create, Read, Update and Delete` or **CRUD** in short. 
REST standards define separate requests for each of them : 
```javascript
CREATE -> POST
READ -> GET
UPDATE -> PUT
DELETE -> DELETE
```
These requests generally have some data encoded with them in the `json` format. The data can include different things like : 
 - Authorization data - including API keys, access tokens, etc.
 - Data needed to be stored on the database.
 - Data needed to be updated.

Also, the requests are accompanied by a response from the server : 
![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/474d991d-1c48-4b86-996e-8a5c54b03b7c)

You can see a number in the response. The numbers represent the status of the response. For example, if the request was successfully executed, servers return `200 - OK` status.
The common responses range as given below : 
![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/8201f5c9-604d-4a8f-bf8f-1c0a2a68b396)

Another important concept of RESTful servers are that `they are stateless` which simply means that subsequent requests should be independent of the previous requests.
This is achieved through not storing data on the server, rather it is stored separately on a database. The database is access through separate server requests.

But, why stateless?
> Stateless servers are highly scalable.

## Pagination and Versioning
An important aspect of RESTful API is to paginate responses in case of large sets of data. This makes the server responses faster and more readable.

```javascript
/product?limit=25&offset=50
```

The above request will send 25 products starting from the 50th one. 

API versioning are also important when releasing newer versions so that the requests can be more accurately read without errors.

