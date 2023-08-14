# What are Proxies and how do they work?
Proxy is simply a server or machine that does something on your behalf. 
In the tech world, proxies are used to handle requests and responses. They can either work on the clients' behalf to send requests to servers or on the server's to handle the incoming requests.

Based on their usage there are 2 major types of proxies : 

## Forward Proxy
A forward proxy sits in between the client and the internet. Every request from a Local Area Network goes to the forward proxy.
It is then forwarded to the respective servers or IP addresses.

![Forward Proxy](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/e258ac45-9bde-4248-9c12-10219ffc19f0)

**Functions of Forward Proxy :**
 - `Protect client's online identity` by hiding the IP address of the client.
 - `Bypass browsing restrictions` : these are generally called VPN services.
 - `Blocking access to certain content` like the ones used in schools and colleges to restrict certain websites.

## Reverse Proxy
A reverse proxy sits in between the Internet and the backend servers. All requests from the client are directed towards the Reverse Proxy.
The proxy then requests data from the respective servers that are required. A simple example of a reverse proxy is a `Load Balancer`.

![Reverse Proxy](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/250694a7-fae2-43e1-a1b4-8cefce5d5aa6)

**Functions of Reverse Proxy :**
 - `Protects a web service` from potential `attacks` by doing various checks and rate limiting.
 - `Load balancing` so that the load is reduced on individual servers.
 - `Caching the data` so that number of requests on actual servers are reduced.
