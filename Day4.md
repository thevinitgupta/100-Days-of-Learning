# API Gateway - The Gatekeepers of Backend

In the realm of modern software development, APIs (Application Programming Interfaces) are the backbone of seamless communication between various services. 

At the core of this interaction lies the API Gateway, which sits in between the client and backend servers, managing various tasks so that the `millions of requests` are handled properly through `load balancing`, proper authentication to `provide secure access` and `caching` data for faster access.
![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/d00ffcc5-db0c-4515-9ec8-7f706f8f3042)


## Functions of API Gateways

API Gateways serve multifaceted functions that simplify development, enhance performance, and bolster security:

- `Request Routing`: Efficiently directs incoming requests to appropriate backend services based on predefined rules.
- `Authentication and Authorization`: Ensures only authorized users gain access to specific resources, enhancing security.
- `Rate Limiting`: Prevents abuse by setting limits on client requests within specified time frames.
- `Caching`: Reduces backend server load by caching responses, optimizing response times for frequently requested data.
- `Request and Response Transformation`: Modifies request and response formats, facilitating communication across diverse systems.
- `Logging and Monitoring`: Provides robust logging and monitoring capabilities, aiding in usage analysis and troubleshooting.

## Data Flow through API Gateway

The journey of data via an API Gateway involves orchestrated steps for efficient communication:

1. **Client Request** : Initiates communication by sending an HTTP request to the API Gateway.
2. **Parameter Validation** : Validates the request data format.
3. **Allow/ Deny List** : Checks for IP address and location and does not allow if these are in the block list.
4. **Authentication/ Authorization** : Authenticates, and checks authorization of the request by validating the tokens and data provided.
5. **Rate Limit** : Prevents abuse by setting limits on client requests within specified time frames
6. **Routing** : Directs the request to the appropriate backend service using defined rules.
7. **Backend Processing** : Processes the request, executing necessary business logic.
8. **Response Processing** : Receives the backend-generated response, possibly modifying it.
9. **Response to Client** : Sends the enriched or transformed response back to the client.

   ![API Gateway working example](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/4c66cca8-3b7a-4e9b-a4f1-8a2b3e096486)


## Real-World API Gateway Services

Prominent services like `Amazon API Gateway, Kong, and Apigee` function as API Gateways, simplifying and optimizing communication, load balancing, security, and analytics.

In conclusion, API Gateways are unsung heroes ensuring smooth interactions between backend systems, enhancing control, security, and user experiences in modern applications.
