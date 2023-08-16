# Microservices for everyone
One of the latest buzz words in the tech world is `Microservices`. 
You might have recently come across this some version of this article : 
![Amazon Moves to Microservices](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zfhnkergldok0ai1y7oy.png)


And you might be wondering what does the word `Microservice` mean actually. But `before understanding the present, one must study the past`. And the past tense of Microservices is `Monolith`.

## The Monolith Architecture
Monoliths mean this : 👇

![Monolith](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n7c0q18l836nt0nuhe2a.jpg)

Yes, but in the tech world it is defined as 
> A software development model that uses one code base to perform multiple business functions

Or in even simpler terms imagine a large website like Amazon(which is actually a large website😅. The different parts of Amazon are : 
 - Users
 - Search
 - Products
 - Shipping
 - Sellers

Now imaging a computer handling the Millions of transactions happening on Amazon every single minute. What will the computer look like?

<img src="https://media.giphy.com/media/cwcA32epxS8WfKH1L4/giphy.gif"/>

Just kidding, servers that large have their optimizing code and cooling systems. But there could be other issues like single point of failure among the different functionalities, scaling issues(costly for more servers) and lack independence among different modules and teams.

And this is where `Microservices` come in.

## What are Microservices exactly?
Microservices are `loosely coupled services`, each handling a `dedicated function` inside a large scale application. For example, the above sections of Amazon can each be a microservice.

![Microservices architecture diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zytfpvt8anbu0l5hn11c.png)


Microservices can talk to each other through systems like Remote Procedure Calls(RPCs), Event Streaming or Message brokers. 

Microservices should follow some protocols for a better functionality : 
 - Each microservice should be `self-contained`.
 - They should be `deployed separately`.
 - They should be `scaled separately` and be `independent of other services.

## Communication in a Microservice Architecture
Microservices means a set of servers that handle separate functionalities. And communication between them is just as important as between the clients and the backend.

### 1. Client to Server
For a large service like Amazon serving Billions of devices, and having a microservice architecture, we cannot put the code to make request to different services on the frontend app or website. *Solution??*

**🏁It is as simply an API Gateway**
The clients make requests to the API Gateway and it's the task of the API Gateway to redirect those requests to different microservices based on the requested data.

![API Gateways in Microservices](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gzenjvzmudvtgxv80sch.png)

> 🚨 But there is an issue. What happens if the data requested needs more than 1 microservice?

### 2. Connecting Microservices
For a large application, the requested data in rarely present on a single microservice. We need a way for different microservices to exchange information. 

There are 3 ways : `Remote Procedure Calls(RPCs), Event Streaming or Message brokers`.

`RPCs` are faster but the impact on other microservices in case of errors in more.

`Event Streaming` provides a more secure transaction, but are slower. 

`Message brokers` are services that allow for secure and faster data exchange but are generally third party services. 

![Communication between Microservices](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/echnb4agu8obg1wsjs6a.png)

## Advantages of using Microservices
Microservices were introduced after Monoliths, so they should have some clear advantages for people for prefer them over the other. 
 - `Tech stack 👨‍💻` : Since each Microservice is self-contained, they can be developed using different tech stack based on the particular requirements. This is easily one of the best points of using microservices.
 - `Separate teams 👨‍👩‍👧‍👧 ` : Separate teams can work on different micro service and move at different speeds without the lock in of any other service. 
 - `Scalability 💻💻` : Based on the usage, we can scale a particular microservice independently, reducing the overhead of scaling. This reduces cost and maintenance issues.
 
But a major `disadvantage` is that building a Microservices architecture is in itself a `difficult task` that requires thorough discussions and development capabilities even for seasoned developers. 

It is therefore better to understand that just because it is a buzz word, doesn't mean you have to do it too. 

Yes, understand what it means is good, but the overhead is too big to build a simple social media website and use microservices. 



