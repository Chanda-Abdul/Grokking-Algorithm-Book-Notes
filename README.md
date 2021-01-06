# Grokking-Algorithm-Book-Notes
My notes while reading the Grokking Algorithm Book.  

https://livebook.manning.com/book/grokking-algorithms/

https://www.amazon.com/Grokking-Algorithms-illustrated-programmers-curious/dp/1617292230


# Chapter 1. Introduction to Algorithms and Binary Search

- `O(n)` = Linear Time => Simple Search
- `O(n*log n)` = Fast Sorting Algorithm => Quicksort
- `O(n²)` = Slow  Sorting Algorithm  => Selection Search
- `O(n!)` = really slow algorithm

## Time Complexity of Binary Search

`O(log n)`

- logs are the opposite of exponentials

## How to implement a Binary Search in JavaScript

````
let exampleArray = [1, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59];

const binarySearch = (array, target) => {
  //number of iterations
  let loops = 0
  
  // Define Start and End Index
  let startIndex = 0;
  let endIndex = array.length - 1;
  
  // While Start Index is less than or equal to End Index
  while(startIndex <= endIndex) {
  
    // Define Middle Index (This will change when comparing )
    let middleIndex = Math.floor((startIndex + endIndex) / 2);
    
    // Compare Middle Index with Target for match
    if(target === array[middleIndex]) {
      loops ++
      return `Target was found at index ${middleIndex} in ${loops} iterations`;
    }
    
    // Search Right Side Of Array
    if(target > array[middleIndex]) {
      console.log("Searching the right side of Array")
      loops ++
      
      // Assign Start Index and increase the Index by 1 to narrow search
      startIndex = middleIndex + 1;
    }
    
    // Search Left Side Of Array
    if(target < array[middleIndex]) {
      // Assign End Index and increase the Index by 1 to narrow search
      console.log("Searching the left side of array")
      loops ++
      endIndex = middleIndex - 1;
    }
    
    // Not found in this iteration of the loop. Looping again.
    else {
      loops ++
      console.log("Not Found this loop iteration. Looping another iteration.")
    }
  }
  
  // If Target Is Not Found
  console.log("Target value not found in array");
}

binarySearch(exampleArray, 37)
````

- see more https://github.com/ChandaHubbard/DSA-Searching


# Chapter 2 - Sort Selection

- computer's memory is like a giant set of drawers `O(n²)`

- linked lists vs. arrays, for storing multiple elements

  - `O(1)` => constant time
  - `O(n)` => linear time
  
|   | Arrays| Lists|
|---|---|---|
|Reading|O(1)|O(n)|
|Insertion|O(n)|O(1)|
|Deletion|O(n)|O(1)|

### Arrays
- random access
- elements are stored next to each other
- allows fast read
- all elements should be the same type

### Lists
- sequential access
- elements everywhere, each elements stores the address of the next element
- allows fast insertion and deletion

## How to implement an Array in JavaScript

````let array = [1, 2, 3]````

### Array Class
````
class Array { 
  
    // Create constructor 
    constructor() {   
      
        // It store the length of array. 
        this.length = 0;  
          
        // Object to store elements. 
        this.data = {};  
    } 
} 
````

* see more https://github.com/ChandaHubbard/DSA-Arrays

## How to implement a Linked List in JavaScript

This is what a linked list looks like in JavaScript

````
const list = {
    head: {
        value: 6
        next: {
            value: 10                                             
            next: {
                value: 12
                next: {
                    value: 3
                    next: null	
                    }
                }
            }
        }
    }
};
````
create the Node class

````
class ListNode {
  constructor(data) {
    this.data = data
    this.next = null
  }
}
````
create the linked list class
````
class LinkedList {
  constructor(head = null) {
    this.head = head
  }
}
````
insert `2` as the list head and `5` as the next node
```
let node1 = new ListNode(2)
let node2 = new ListNode(5)
node1.next = node2

let list = new LinkedList(node1)

list.head.next.data//returns 5
````
 - Linked list methods
    - `size()`
    - `clear()`
    - `getLast()`
    - `getFirst()`
* see more https://github.com/ChandaHubbard/DSA-LinkedList

# Chapter 3 - Recursion 

"Loops may acheive a performance gain for your program. Recursion may acheive a performance gain for your programmer.  Choose which is more important in your situation."
- Recursion is when a function calls itself
  - base case => when the function doesnt call itself, prevents infinite loop
  - recursive case => when the function calls itself
- a stack has two operations `.push()` and `.pop()`
- All function calls go onto the call stack
- the call stack can get very large which can take up a lot of memory.


## Time Compelexity

O(n) or linear for recurisve functions

## How to implement a recursive function in JavaScript

````
function fact(x) {
  if (x == 1) { 
    return 1
    }
  else { 
    return x * fact(x-1)
    }
}
````

- see more https://github.com/ChandaHubbard/DSA-Recursion

# Chapter 4 - Quicksort

- Implement a Quicksort function using a divide-and-conquer approach
  - divide-and-conquer are recursive algorithms
  - figure out the base case(simplest solution)
  - divide or decrease your problem until it becomes the base case
- quicksort is a sorting alogorithm that is much faster than selection sort
  - pivot
  - partitioning( sub-array < pivot, pivot, sub-array > pivot)
  -inductive-proofs


## Time Compelexity
- speed depends on the pivot point
- on average O(n log n) => merge-sort
- worse case O(n²) => selection Sort 


## How to implement a quicksort algorithm in JavaScript

````
function swap(items, leftIndex, rightIndex){
    var temp = items[leftIndex];
    items[leftIndex] = items[rightIndex];
    items[rightIndex] = temp;
}


function partition(items, left, right) {
    var pivot   = items[Math.floor((right + left) / 2)], //middle element
        i       = left, //left pointer
        j       = right; //right pointer
    while (i <= j) {
        while (items[i] < pivot) {
            i++;
        }
        while (items[j] > pivot) {
            j--;
        }
        if (i <= j) {
            swap(items, i, j); //swapping two elements
            i++;
            j--;
        }
    }
    return i;
}

function quickSort(items, left, right) {
    var index;
    if (items.length > 1) {
        index = partition(items, left, right); //index returned from partition
        if (left < index - 1) { //more elements on the left side of the pivot
            quickSort(items, left, index - 1);
        }
        if (index < right) { //more elements on the right side of the pivot
            quickSort(items, index, right);
        }
    }
    return items;
}

const items = [5,3,7,6,2,9];
const sortedArray = quickSort(items, 0, items.length-1)
console.log(sortedArray)
````

* see more https://github.com/ChandaHubbard/DSA-Sorting

* see more https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/sorting/quick-sort

# Chapter 5 - Hash Tables

Hash tables are a powerful data structure because they’re so fast and they let you model data in a different way.
- You can make a hash table by combining a hash function with an array.
- Collisions are bad. You need a hash function that minimizes collisions.
- Hash tables have really fast search, insert, and delete.
- Hash tables are good for modeling relationships from one item to another item.
- Once your load factor is greater than 0.7, it’s time to resize your hash table.
- Hash tables are used for caching data (for example, with a web server).
- Hash tables are great for catching duplicates.

## Hash Functions
A <b>hash function</b> is a function where you put in a string and you get back a number.
- The hash function consistently maps a name to the same index. 
- Put a hash function and an array together, and you get a data structure called a hash table.
- Arrays and lists map straight to memory, but hash tables are smarter. They use a hash function to intelligently figure out where to store elements.
- in JavaScript hash tables are objects
- A good hash function distributes values in the array evenly.
- A bad hash function groups values together and produces a lot of collisions.

## Implementation
```
class HashMap {
  constructor (initialCapacity=8) {
    this.length = 0;
    this._hashTable = [];
    this._capacity = initialCapacity;
    this._deleted = 0;
  }
  
    get(key) {
    const index = this._findSlot(key);
    if (this._hashTable[index] === undefined) {
      throw new Error('key error');
    }
    return this._hashTable[index].value;
  }
  
   set (key, value) {
    const loadRatio = (this.length + this._deleted + 1) / this._capacity;
    if (loadRatio > HashMap.MAX_LOAD_RATIO) {
      this._resize(this._capacity * HashMap.SIZE_RATIO);
    }
    //Find the slot where this key should be in 
    const index = this._findSlot(key);
    
    if(!this._hashTable[index]) {
      this.length++;
    }
    this._hashTable[index] = {
      key,
      value,
      DELETED: false
    };
  }
  
    delete(key) {
    const index = this._findSlot(key);
    const slot = this._hashTable[index];
    if (slot === undefined) {
      throw new Error('key error');
    }
    slot.DELETED = true;
    this.length--;
    this._deleted++;
  }
  
  _findSlot(key) {
      const hash = HashMap._hashString(key);
      const start = hash % this._capacity;
      
      for (let  i=start; i<start + this._capacity; i++) {
        const index = i % this._capacity;
        const slot = this._hashTable[index];
        if (slot === undefined || (slot.key === key && !slot.DELETED)) {
        return index;
      }
    }
  }
  
  _resize(size) {
    const oldSlots = this._hashTable;
    this._capacity = size;
    //Reset the length - it will get rebuilt as you add the items back
    this.length = 0;
    this._hashTable = [];
    
    for (const slot of oldSlots) {
      if (slot !== undefined) {
        this.set(slot.key, slot.value);
      }
    }
  }
  
  static _hashString(string) {
    let hash = 5381
    for (let i = 0; i < string.length; i++) {
      hash = (hash << 5) + hash + string.charCodeAt(i)
      
      hash = hash & hash
    }
    return hash >>> 0
  }
}
```

## Collisions
<b>collisions</b> take place two keys have been assigned the same slot
-  To avoid collisions, you need
  - A low load factor, Load factor measures how many empty slots remain in your hash table.
  - A good hash function
  
## Time Complexity
|   | Averge Case| Worse Case |
|---|---|---|
|Search|O(1)|O(n)|
|Insert|O(1)|O(n)|
|Delete|O(1)|O(n)|
#

* see more https://github.com/ChandaHubbard/DSA-Hashmaps

* see more https://github.com/trekhleb/javascript-algorithms/tree/master/src/data-structures/hash-table

# Chapter 6. Breadth-first search 

- <b>Breadth-first search</b> allows you to find the search distance between two points

- shortest path problems are solved with Breadth-first search
  - moodel the problem as a graph
  - solve the problem using Breadth-first search 

- A <b>graph</b> models a set of connections which are made of nodes and edges
- Breadth-first search is a type of algorithm that runs on graphs
  - is there a path?
  - what is the shortest path?

- a <b>queue</b> is a type of data structure for BFS.
  - enqueue to add or `.push()`
  - dequeue to remove or `.pop()`
- hash tables
- directed graphs(one way)

## Time complexity

- Breadth-first search has a run time of `O(V + E)` where V is Verticies and E is Edges
- Topological sort

## Recap
- Breadth-first search tells you if there’s a path from A to B.
- If there’s a path, breadth-first search will find the shortest path.
- If you have a problem like “find the shortest X,” try modeling your problem as a graph, and use breadth-first search to solve.
- A directed graph has arrows, and the relationship follows the direction of the arrow (rama -> adit means “rama owes adit money”).
- Undirected graphs don’t have arrows, and the relationship goes both ways (ross - rachel means “ross dated rachel and rachel dated ross”).
- Queues are FIFO (First In, First Out).
- Stacks are LIFO (Last In, First Out).
- You need to check people in the order they were added to the search list, so the search list needs to be a queue. Otherwise, you won’t get the shortest path.
- Once you check someone, make sure you don’t check them again. Otherwise, you might end up in an infinite loop.

## Implementation in JavaScript
````
const bfs = (node) => { 
   visited[node] = true;
   queue.equeue(node); 
    while (!queue.isEmpty()) {
        let visiting = queue.dequeue();
        console.log(`we visited ${visiting}`)
        for (let j = 0; j < graphAdj[visiting].length; j++) {
           if ((graphAdj[visiting][j] === 1) && (visited[j] === false)) {  
           visited[j] = true;
           queue.equeue(j);
          }
       }
     }
}
````

Traversal
````
function traverseBFS(root) {
  let queue = [root]
  let res = []
  
  while (queue.length) {      
    let curr = queue.shift()
    res.push(curr.key)
    
    if (curr.right){
      queue.push(curr.right)
    }
    
    if (curr.left){
      queue.push(curr.left)
    }
  }
  
  return res
}
````

* see more https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/tree/breadth-first-search
* see more https://github.com/ChandaHubbard/DSA-Stack-and-Queue

# Chapter 7. Dijkstra’s algorithm

- Breadth-first search will find you the path with the fewest segments (the first graph shown here). What if you want the fastest path instead (the second graph)? You can do that fastest with a different algorithm called <b>Dijkstra’s algorithm</b>.

- There are four steps to Dijkstra’s algorithm:

  - 1.  Find the “cheapest” node. This is the node you can get to in the least amount of time.

  - 2.  Update the costs of the neighbors of this node. 

  - 3.  Repeat until you’ve done this for every node in the graph.

  - 4.  Calculate the final path.
  
- When you work with Dijkstra’s algorithm, each edge in the graph has a number associated with it. These are called weights.

- A graph with weights is called a weighted graph. A graph without weights is called an unweighted graph.

- To calculate the shortest path in an unweighted graph, use breadth-first search. To calculate the shortest path in a weighted graph, use Dijkstra’s algorithm. Graphs can also have cycles

- You can’t use Dijkstra’s algorithm if you have negative-weight edges. Negative-weight edges break the algorithm.
  - you can’t use negative-weight edges with Dijkstra’s algorithm. If you want to find the shortest path in a graph that has negative-weight edges, there’s an algorithm for that! It’s called the Bellman-Ford algorithm

- use hash tables

## Recap
 - Breadth-first search is used to calculate the shortest path for an unweighted graph.
 - Dijkstra’s algorithm is used to calculate the shortest path for a weighted graph.
 - Dijkstra’s algorithm works when all the weights are positive.
 - If you have negative weights, use the Bellman-Ford algorithm.
 
# Implementation in JavaScript
````
djikstraAlgorithm(startNode) {
   let distances = {};

   // Stores the reference to previous nodes
   let prev = {};
   let pq = new PriorityQueue(this.nodes.length * this.nodes.length);

   // Set distances to all nodes to be infinite except startNode
   distances[startNode] = 0;
   pq.enqueue(startNode, 0);
   this.nodes.forEach(node => {
      if (node !== startNode) distances[node] = Infinity;
      prev[node] = null;
   });

   while (!pq.isEmpty()) {
      let minNode = pq.dequeue();
      let currNode = minNode.data;
      let weight = minNode.priority;
      this.edges[currNode].forEach(neighbor => {
         let alt = distances[currNode] + neighbor.weight;
         if (alt < distances[neighbor.node]) {
            distances[neighbor.node] = alt;
            prev[neighbor.node] = currNode;
            pq.enqueue(neighbor.node, distances[neighbor.node]);
         }
      });
   }
   return distances;
}
````

* see more https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/graph/dijkstra

# Chapter 8. Greedy Algoritms

- A greedy algorithm is simple: at each step, pick the optimal move.

- In technical terms: at each step you pick the locally optimal solution, and in the end you’re left with the globally optimal solution.

- power set
  - Sets are like lists, except sets can’t have duplicates.
  - You can do some interesting operations on sets, like union, intersection, and difference.

- approximation algorithm

- factorial function 

- NP-complete
  - Your algorithm runs quickly with a handful of items but really slows down with more items.
  - “All combinations of X” usually point to an NP-complete problem.
 -  Do you have to calculate “every possible version” of X because you can’t break it down into smaller sub-problems? Might be NP-complete.
  - If your problem involves a sequence (such as a sequence of cities, like traveling salesperson), and it’s hard to solve, it might be NP-complete.
  - If your problem involves a set (like a set of radio stations) and it’s hard to solve, it might be NP-complete.
  - Can you restate your problem as the set-covering problem or the traveling-salesperson problem? Then your problem is definitely NP-complete.
  
## Recap
- Greedy algorithms optimize locally, hoping to end up with a global optimum.
- NP-complete problems have no known fast solution.
- If you have an NP-complete problem, your best bet is to use an approximation algorithm.
- Greedy algorithms are easy to write and fast to run, so they make good approximation algorithms.

* see more https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/sets/power-set

* see more https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/sets/knapsack-problem

# Chapter 9. Dynamic programming

- <b>dynamic programming</b>, a technique to solve a hard problem by breaking it up into subproblems and solving those subproblems first.

-  Dynamic programming only works when each subproblem is discrete—when it doesn’t depend on other subproblems. 

- Dynamic programming is useful when you’re trying to optimize something given a constraint. 

- The Feynman algorithm is named after the famous physicist Richard Feynman, and it works like this:
  - Write down the problem.
  - Think real hard.
  - Write down the solution.

## Recap
- Dynamic programming is useful when you’re trying to optimize something given a constraint.
- You can use dynamic programming when the problem can be broken into discrete subproblems.
- Every dynamic-programming solution involves a grid.
- The values in the cells are usually what you’re trying to optimize.
- Each cell is a subproblem, so think about how you can divide your problem into subproblems.
- There’s no single formula for calculating a dynamic-programming solution.

# Chapter 10. K-nearest neighbors

- <b>k-nearest neighbors (KNN)</b> algorithm for classification
  - Classification = categorization into a group
  - Regression = predicting a response (like a number)
  
- Cosine similarity doesn’t measure the distance between two vectors. Instead, it compares the angles of the two vectors.
- KNN is a really useful algorithm, and it’s your introduction to the magical world of machine learning! Machine learning is all about making your computer more intelligent. 
- OCR stands for optical character recognition. It means you can take a photo of a page of text, and your computer will automatically read the text for you. Google uses OCR to digitize books.
  - Generally speaking, OCR algorithms measure lines, points, and curves.
  - Then, when you get a new character, you can extract the same features from it.
  - The first step of OCR, where you go through images of numbers and extract features, is called training. Most machine-learning algorithms have a training step: before your computer can do the task, it must be trained. 
  - Spam filters use another simple algorithm called the Naive Bayes classifier. First, you train your Naive Bayes classifier on some data.
    - Naive Bayes figures out the probability that something is likely to be spam. It has applications similar to KNN.
## Recap
I hope this gives you an idea of all the different things you can do with KNN and with machine learning! Machine learning is an interesting field that you can go pretty deep into if you decide to:
- KNN is used for classification and regression and involves looking at the k-nearest neighbors.
- Classification = categorization into a group.
- Regression = predicting a response (like a number).
- Feature extraction means converting an item (like a fruit or a user) into a list of numbers that can be compared.
- Picking good features is an important part of a successful KNN algorithm.

# Chapter 11. Where to go next

## Binary search tree 
- Searching for an element in a binary search tree takes O(log n) time on average and O(n) time in the worst case. 
- Searching a sorted array takes O(log n) time in the worst case, so you might think a sorted array is better. But a binary search tree is a lot faster for insertions and deletions on average.
 
 |   | Array| Search Tree|
|---|---|---|
|Search|O(log n)|O(log n)|
|Insert|O(n)|O(log n)|
|Delete|O(n)|O(log n)|

- Binary search trees have some downsides too: for one thing, you don’t get random access. You can’t say, “Give me the fifth element of this tree.” Those performance times are also on average and rely on the tree being balanced.
- If you’re interested in databases or more-advanced data structures, check these out:
  - B-trees
  - Red-black trees
  - Heaps
  - Splay trees
  
## Inverted indexes
- a hash that maps words to places where they appear. This data structure is called an inverted index, and it’s commonly used to build search engines.

## The Fourier transform

The Fourier transform is one of those rare algorithms: brilliant, elegant, and with a million use cases. The best analogy for the Fourier transform comes from Better Explained (a great website that explains math simply): given a smoothie, the Fourier transform will tell you the ingredients in the smoothie.[1] Or, to put it another way, given a song, the transform can separate it into individual frequencies.

* See also https://betterexplained.com/articles/an-interactive-guide-to-the-fourier-transform/

## Parallel algorithms

- To make your algorithms faster, you need to change them to run in parallel across all the cores at once!

- It’s well known that you can’t sort an array in O(n) time—unless you use a parallel algorithm! There’s a parallel version of quicksort that will sort an array in O(n) time.

- Parallel algorithms are hard to design. And it’s also hard to make sure they work correctly and to figure out what type of speed boost you’ll see. 

- Overhead of managing the parallelism

- Load balancing

- If you’re interested in the theoretical side of performance and scalability, parallel algorithms might be for you!

## MapReduce

- There’s a special type of parallel algorithm that is becoming increasingly popular: the distributed algorithm. 
- The MapReduce algorithm is a popular distributed algorithm. You can use it through the popular open source tool Apache Hadoop.
- Distributed algorithms are great when you have a lot of work to do and want to speed up the time required to do it. MapReduce in particular is built up from two simple ideas: the `map` function and the `reduce` function
  - The `map` function is simple: it takes an array and applies the same function to each item in the array.
  - With `reduce`, you transform an array to a single item.
  
## Bloom filters and HyperLogLog

- Bloom filters offer a solution. Bloom filters are probabilistic data structures. They give you an answer that could be wrong but is probably correct. Instead of a hash, you can ask your bloom filter if you’ve crawled this URL before. A hash table would give you an accurate answer
- Bloom filters are great because they take up very little space. A hash table would have to store every URL crawled by Google, but a bloom filter doesn’t have to do that. They’re great when you don’t need an exact answer, as in all of these examples. It’s okay for bit.ly to say, “We think this site might be malicious, so be extra careful.”
- HyperLogLog approximates the number of unique elements in a set. Just like bloom filters, it won’t give you an exact answer, but it comes very close and uses only a fraction of the memory a task like this would otherwise take.

## The SHA algorithms

- Another hash function is a secure hash algorithm (SHA) function. Given a string, SHA gives you a hash for that string.
- SHA is a hash function. It generates a hash, which is just a short string. The hash function for hash tables went from string to array index, whereas SHA goes from string to string.
- SHA generates a different hash for every string.
- SHA is also useful when you want to compare strings without revealing what the original string was. 
- You can convert a password to a hash, but not vice versa.
- If you make a small change to a string, Simhash generates a hash that’s only a little different. This allows you to compare hashes and see how similar two strings are

## Diffie-Hellman key exchange

- Diffie-Hellman has two keys: a public key and a private key. 
  - The public key is exactly that: public. You can post it on your website, email it to friends, or do anything you want with it. You don’t have to hide it. When someone wants to send you a message, they encrypt it using the public key. 
  - An encrypted message can only be decrypted using the private key. As long as you’re the only person with the private key, only you will be able to decrypt this message
  
## Linear programming

- Linear programming is used to maximize something given some constraints. 
  - For example, suppose your company makes two products, shirts and totes. 
    - Shirts need 1 meter of fabric and 5 buttons. 
    - Totes need 2 meters of fabric and 2 buttons. 
    - You have 11 meters of fabric and 20 buttons. 
    - You make $2 per shirt and $3 per tote. 
    - How many shirts and totes should you make to maximize your profit?
- Linear programming uses the Simplex algorithm. 
