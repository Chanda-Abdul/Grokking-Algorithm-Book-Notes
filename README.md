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
- worse case O(n ** 2)=> selection Sort 


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



