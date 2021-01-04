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
