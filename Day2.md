# Key Data Structures Used Everyday
While learning about data structures and algorithms, the most common question everyone has is :
> Are they really useful in the real world?
The answer is `YES ✅` and here are some of the common use cases.

## Lists or Arrays
The first data structure that we all learn are Arrays, so let's start with that.
By definition, an array is a `contiguous data structure` that holds similar types of data. Also, the data is stored in locations that are in sectors on a disk that are by each other.
This makes access of data fast and somewhat easy, with less chances of missing.They are relatively complicated to update, naturally these are used : 
- Mathematical computing in the form of matrices or Double Dimensional Arrays.
- Storing data in tables.
- To represent pictures in the form of Pixel arrays, which can be used to manipulate images easily.
 ![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/8f247ff5-0649-4981-84fc-504727fa1106)

## Linked Lists  
Linked Lists are different from arrays in the way that the inidividual data is not stored in contiguous memory locations and are linked using address pointers. 
This property makes the Linked List memory efficient and easily updatable. 
![insertion-operation-of-linked-list](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/d4b62a45-9055-486f-8d26-b9030372e670) 
`image by Scaler`

You must have used Twitter or Instagram where on a refresh, the feed updates. Linked lists are used in such places since updating is much easier in Linked Lists compared to arrays.
- Creating social media feeds that are regularly updated.
- Carts and product listings in E-Commerce stores
- Task list applications so that tasks can be added, deleted or edited easily.

## Stacks and Queues
Stacks and queues are like arrays, but follow certain rules for adding new elements and deleting old ones. 

Stacks follow the LIFO(Last in First out) principle, where the elements can only be removed from the end that they are being added. This feature is useful in implementing `UNDO` and `REDO` actions.
So stacks find use in :
- Browser history tabs where users can go back to the previous URL by simply removing the most recent one from the history stack.
- Text editing softwares where each change is stored in the stack and undo operation removes the most recent change, helping us to go back to the previous operation. Also, the removed changes are stored in a separate stack so that we can use the `REDO` operation as well.

![321-10-key-data-structures-we-use-every-day-youtube-mozilla-firefox-2023-08_gTY5Kd0A (online-video-cutter com)](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/58e021c8-f44a-4e57-a757-a7c6a49ca8cd)

Queues follow the FIFO(First in First out) principle, where the elements that were added first are given priority in any task. This is just like the real world queues in offices.
Queues are used in : 
- Printer jobs.
- Sending user actions to games.
- Chat applications where the messages sent first appear first.
![simpsons in queue](https://media.giphy.com/media/l2JdWz78SwGlUV7OM/giphy.gif)


## Trees
Trees are used to represent `hierarchy` in data. 
This means that the parent nodes are greater in value or higher in rank or simply the question where as the children are the answers. Trees are one of the most commonly used data structures due to their flexibility and hierarchical data access. 
The most common use cases are : 
- `Database indexing` where tree nodes point to collections of similar data grouped together for reduced read time trying to read all the data present.
-  `AI Decision Making` where the questions are the parent nodes and based on the answer, more questions are asked eventually reaching a decision point.
-  `File store` is the most common use case where Directories are the parents and subsequent folders are added until the files.
  ![Screenshot 2023-08-09 114518_cleanup](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/c7d7b1b1-72a5-44d9-b9a9-76aa42d192de)

## Hash Tables
Hash tables provide fast data lookup using tables that directly point to the address locations of certain data. Hash tables follow the concept of hashing to store unique IDs for the data and are used to lookup randomly stored data from different locations.
This feature not only makes hash table data access faster but also memory efficient.
Hash tables find usage in :
- `Search Engines` that fetch the various websites using IP addresses based on search strings.
- `Caching` services like Redis servers.
- `Symbol table` in programming language interpreters and compilers
  ![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/a2ccc0b9-db46-4053-bdaa-5870fd8055c0)

  

## Graphs
Graphs are the least heard of the data structures that have become really useful with the rise of Social Media platforms like Facebook and LinkedIn.
Graphs are used to `store connections between different users in the social network` thus giving us important data like friend suggestions, 1st, 2nd or 3rd+ connections on LinkedIn, etc.
Graphs are also used in various path finding algorithms that are used to `generate routes in maps`.
![image](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/6ddae782-4588-4178-ad74-a666fc21d4cb)
