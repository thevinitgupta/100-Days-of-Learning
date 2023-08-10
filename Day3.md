# GraphQL - The API child of Facebook

GraphQL has been around since 2012(inside of Facebook😅). 

But Facebook made it public in 2015 and since then, it has become one of the most use Back-end architecture. 
 
The question is what exactly is GraphQL?
`Answer` : `GraphQL is a new API standard that provides a more efficient, powerful and flexible alternative to REST`

_Confused?_
<img src="https://media.giphy.com/media/4JVTF9zR9BicshFAb7/giphy.gif"/>

Well in simple terms, `it is used to define how requests are made to an API and how it handles the responses`.

But, how is it related to and even _BETTER_ than REST?
There are few things to consider to make this comparison.

![GraphQL Sample](https://www.apollographql.com/blog/static/graphql-query-79196ebc9ef66116c562969e686a6cf5.png)

## Single Point Of Origin
If you have ever developed a REST API, you know the work it takes to build an endpoint for the user details, another for the blog posts list, another for the followers list, the following list, and it goes on. 

With GraphQL, there is only one endpoint and it does the job. For accessing a set of data, you only need to specify the particular things you need. What a GraphQL server does is that it organizes only the specifics you need and returns the response. 

`Done. No extra data, no multiple endpoints.`

## Rapid Product Iterations
In the fast paced development cycles, there are many versions of the API. 
And every time there is new data, the endpoints have to be reconfigured, redeveloped, re something something. 

<img src="https://media.giphy.com/media/14smAwp2uHM3Di/giphy.gif"/>

With GraphQL, this problem is solved. 

Thanks to the flexible nature of GraphQL, changes on the client-side can be made without any extra work on the server. 

Since clients can specify their exact data requirements, no backend engineer needs to make adjustments when the design and data needs on the frontend change.

## Schema Based Communication
An important step in development is the Integration. And, this is where it all turns around. No integration can be completed without a list of bugs and debugging. 

I guess, bugs are not the developers best friends. Agree?

<img src="https://media.giphy.com/media/ukMiDlCmdv2og/giphy.gif"/>

Since, GraphQL works on a strong type system to define the Schema of queries, there is less chance of error. This is because both the frontend and the backend teams are aware of the definite schema. Thus, the process becomes a whole lot easier.

Now, I am not saying the GraphQL is better than REST in all the ways, but it is definitely worth exploring. 
