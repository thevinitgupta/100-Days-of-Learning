# Caching explained in less than 5 minutes
Caching is a data storage technique that plays an essential role in the world for designing fast and scalable systems. 

> A cache stores and retrieves data quickly for future use.

This enables faster response time and decreases the load on other parts of the system. An effective cache is easier to read with an efficient storage system. 

## Why do we need caching?
The use of caching is simply what it is designed to be : *be fast*.
Imagine searching for a product or loading a website with data and you are kept waiting for even 1-2 seconds.

<img src="https://media.giphy.com/media/FoH28ucxZFJZu/giphy.gif"/>

You would just move away from the site. Caching helps prevent this as every visit that does not convert into a sale or something that is essential to a service, it is bad for the business.
This happens because data would be fetched at every single step, making the whole internet slow. 

## How does caching work?
There are multiple principles according to which caches work.

 - Caches take the advantage of the term : `locality` which means `storing data closer to where it is needed`. 
 - Caches store `pre-computed` data and serve them when the users demand it, making the website work faster.

Caches achieve this through the following methods : 
### 1. In-Memory Application Cache
This is basically storing data directly in the applications memory, making it a fast and straightforward way. 
But, the downside is that `each server must maintain it's own copy of the cache`, increasing the memory demand and overall cost of the system.

### 2. Distributed In-Memory Cache
We can also use a distributed cache system like `Redis or Memcached` so that all servers can make use of the same cache.

<img height="200" src="https://kinsta.com/wp-content/uploads/2023/06/memcached-vs-redis-illustration.png"/>

### 3. File System Cache
This type of caches store commonly accessed files. A `CDN` is an example of a file system cache that takes advantage of locality.

#### But if caching is so effective and fast, why is everything stored in caches?
Because caches are costly because they use hardware that is fast, but less resilient or simple terms : `they are fast, efficient, costly and loose data overtime`.
They must effectively choose `which data to keep and which data to evict or delete`.

## Caching Policies
Caching policies help the cache to free up space that is needed for newer and more relevant data. 
The commonly used ones are : 
### 1. First in, First out (FIFO)
Like a queue, this caching policy keeps that most recently added data and removes the oldest ones.

### 2. Least Recently Used(LRU)
This caching technique `keeps track` of the data or files that has `most recently been used`. 
This helps it remove the ones that have not been accessed for a long time.

![LRU Cache](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/701c39fe-f6bc-404d-a1dc-b45159b8c582)

### 3. Least Frequently Used(LFU)
This technique keeps track of how frequently a file or data has been used. 
It removes the least frequently used data, `regardless of how recently it has been used`.

![LFU Cache](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/89e25fef-d51c-442a-ac4b-fdc1993e2f39)


## 3 Big questions while designing a Cache
1. `How big` should the cache be?
2. How should the `data be evicted`?
3. `Which expiration policy` should be used?


