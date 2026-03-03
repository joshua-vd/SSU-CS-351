Name: Joshua Vasquez Diaz 

# Project 1 Analysis and Reporting

## 1. Which program is fastest? Is it always the fastest?

The fastest program is alloca.cpp, with malloc.cpp being very close behind. However, it was not always significantly faster. As the size of the data per node increased, the performance difference between the programs shrank. At large data sizes, memory access and hashing operations dominated the runtime, making the choice of allocation method less significant. 

## 2. Which program is slowest? Is it always the slowest?

The slowest program is the list.cpp and new.cpp. However, they were not dramatically slower in all cases. As the node data size increased significantly, the performance gap between all programs decreased. At larger data sizes, hashing and memory access dominated execution time, reducing the relative impact of allocation overhead.

## 3. Was there a trend in program execution time based on the size of data in each Node? If so, what, and why?

Yes, there was a trend. When the data size in each node goes up, the execution time for all programs go up too. This is because with bigger nodes, the prgram has to deal with initializing and hashing way more data per node. I also notice that when nodes are large, the difference between the programs become less noticeable because the hashing process takes over as a main factor.  


## 4. Was there a trend in execution time based on the length of the blockchain? 
Yes, there was a trend. As the blockchain gets longer, the runtime increaes pretty much in a staright line. When they went from 100k to 1M nodes, the time increased by about 7 to 9 times, which makes sense because extra nodes need to be allocated and its byte hashed once. 


## 5. Consider heap breaks, what's noticeable? Does increasing the stack size affect the heap? Speculate on any similarities and differences in programs?

What is noticeable is the number of heap breaks didn't go up as the number of blocks increased, and it was the same for all programs. Increasing the stack size does not affect the heap because they are separate. Making the stack bigger mainly helps programs that ise a lot of stack memory and doesn't directly affect heap growth or reduce heap brk() calls. The similarities and differences in programs: all the programs had some heap activity at the start, but they all only needed one heap expansion in these tests. Malloc/new probably use the heap a lot for node data, while alloca uses the stack more. But the breaks metric did not show that difference because the heap allocator handle everything with just one expansion.  

## 6. Considering either the malloc.cpp or alloca.cpp versions of the program, generate a diagram showing two Nodes. Include in the diagram
    - the relationship of the head, tail, and Node next pointers.
    - show the size (in bytes) and structure of a Node that allocated six bytes of data
    - include the bytes pointer, and indicate using an arrow which byte in the allocated memory it points to.

head                        tail
|                           |
v                           v
+-----------+    next    +-----------+    next
|  Node 1   | ---------->|  Node 2   | --------> NULL
+-----------+            +-----------+
 
In a 64-bit system: 
next  : Node*     (8 bytes) 
bytes : uint8_t*  (8 bytes)    
size  : int       (4 bytes)   
padding            (4 bytes)

Total Node size = 24 bytes 

Example: Node 1 allocated 6 bytes of data


Node 1:
 bytes  ----+
            |
            v
       +----+----+----+----+----+----+
data -> | b0 | b1 | b2 | b3 | b4 | b5 |
       +----+----+----+----+----+----+
         ^
         |
      bytes points to b0 (the first byte)

In the example, Node 1 has allocated 6 bytes of data, and the bytes pointer in Node 1 points to the first of those 6 bytes. 


## 7. There's an overhead to allocating memory, initializing it, and eventually processing (in our case, hashing it). For each program, were any of these tasks the same? Which one(s) were different?

For all programs they had the same tasks of building a linked list of nodes, initializing/filling the bytes for each node, traversing the nodes and hashing/processing the bytes, and freeing/cleaning up memeory.
Different tasks (where overhead differs): 
Allocation method:
- alloca: stack allocation (very fast, but limited by stack size)
- malloc: heap allocation via C allocator
- new: heap allocation via C++ operator new (often built on malloc but may differ)
- list: likely uses a container allocator / extra node wrapper overhead / extra indirection
Bookkeeping overhead: heap allocators and containers typically add metadata, alignment, and sometimes indirection, impacting small node sizes more 
Memory locality: allocations patterns that are more or less cache-friendly, which can affect traversal and hashing speed.  

## 8. As the size of data in a Node increases, does the significance of allocating the node increase or decrease?

As the size of data in a Node increases, the significance of allocating the node decreases because the cost of initializing and hashing the larger node dominates the total runtime. 


