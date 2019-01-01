# PERT-Enumeration-of-topological-orders

CS 5V81.001.  Implementation of data structures and algorithms  
Fall 2018  
Long Project LP4: PERT, Enumeration of topological orders  

Authors - Team LP101
- Prateek Sarna (pxs180012@utdallas.edu)
- Rahul Nalwade (rsn170330@utdallas.edu) (https://github.com/rahul1947)
- Bhavish Khanna Narayanan (bxn170002@utdallas.edu) (https://github.com/bhavish14)

Project Description
1. Implement enumeration of permutations.
2. Implement enumeration of all topological orders of a given directed graph.
3. Implement the methods in PERT.java.
   - public static PERT pert(Graph g, int[] duration);  
	// Run PERT algorithm on graph g. Assume that vertex 1 is s and vertex n is t.  
	// You need to add edges from s to all vertices and from all vertices to t.  

	   boolean pert();  // non-static method called after calling the constructor
  
Files Included
1. Enumerate.java:  
   - ATTRIBUTES: 
     - T[] arr: Array of elements on which enumeration is to be done.
       n = arr.length
      
     - k: number of elements to be selected (default = n). E.g nPk or nCk.  
   
     - count: counts the number of times visit has been called based on the 
       Approver. 
     
   - APPROVER<T>:  
     - Responsible for selection and de-selection (backtracking) of an 
       element based on certain precedence constraints coded in select() and 
       unselect() methods respectively.
   
     - visit() is called by non-static visit() to print the k elements in the
       arr[0...k-1]
     
   - METHODS:  
     - permute(c): recursive method to visit all valid permutations, where c 
       is number of elements yet to visit.
     - combine(i, c): recursive method to visit all valid combinations, where
       c is the number of element we need to choose from arr[i...n-1].
     - heap(g): recursive method to visit all permutations by a single swap 
       from previous permutation, where first g elements are not frozen, i.e. 
       arr[g...n-1] are frozen, and arr[0..g-1] can only be changed.
     - algorithmL(Comparator c): Knuth's L Algorithm based on Comparator c. 
   
2. EnumerateTopological.java:
   - ATTRIBUTES: 
     - print: boolean if true prints all enumerations, else no printing.
     - selector: Approver of EnumerateTopological itself.
     - Vertex[] A: array of vertices in the Graph.
     
   - SELECTOR extended from APPROVER<T>
     - select(u): selects u, if it has inDegrees = 0.
     - unselect(u): do v.inDegrees++, where edge e = (u,v) exists. 
   
   - METHODS:
     - initialize(): initializes get(u).inDegrees = u.inDegree for all u.
     - enumerateTopological(): based on selector, enumerates all 
       permutations using permute() from Enumerate.
       Returns count of enumerations from Enumerate itself.

3. PERT.java: 
   - PERTVertex:
     - duration: duration of this vertex
     - slack: slack available for this vertex
     - earliestCT: earliest completion time (EC) for this vertex
     - latestCT: latest completion time (LC) for this vertex
   
   - METHODS:
     - initialize(): add edges from source (first vertex) to all vertices, 
       and all vertices to the sink (last vertex).
     - pert(): Implements PERT by computing slack, EC, LC for all vertices.
       Returns true if Graph is not a DAG, false otherwise.
       NOTE: it uses a topological order from DFS.java
   
 
----------------------------------------------------------------------------
RESULTS: 

- Enumerate

  - Permutations: 4 3  
    1 2 3  
    1 2 4  
    1 3 2  
    ...  
    4 1 3  
    4 1 2  
    Count: 24  

  - Combinations: 4 3  
    1 2 3  
    1 2 4  
    1 3 4  
    2 3 4  
    Count: 4  

  - Heap Permutations: 4  
    1 2 3 4  
    2 1 3 4  
    3 1 2 4  
    ...  
    3 2 4 1  
    2 3 4 1  
    Count: 24  

  - Algorithm L Permutations:  
    1 2 2 3 3 4  
    1 2 2 3 4 3  
    1 2 2 4 3 3  
    ...  
    4 3 3 2 1 2  
    4 3 3 2 2 1  
    Count: 180  


Enumerate Topological

 --------------------------------------------------------------------------  
| File          | Output          |   Time (mSec)     | Memory (used/avail)|  
|:-------------:|:---------------:|:-----------------:|:------------------:|  
| dag-07.txt    | 105             | 3                 | 1 MB / 117 MB      |  
| dag-08a.txt   | 118             | 2                 | 1 MB / 117 MB      |  
| dag-08b.txt   | 280             | 3                 | 1 MB / 117 MB      |  
| dag-10.txt    | 20              | 1                 | 1 MB / 117 MB      |  
| dag-50-800.txt| 6193152         | 1426              | 7 MB / 117 MB      |  
 --------------------------------------------------------------------------

PERT

 --------------------------------------------------------------------------  
| File         | Output          |   Time (mSec)     | Memory (used/avail) |  
|:------------:|:---------------:|:-----------------:|:-------------------:|  
| Pert1.txt    | 98 52           | 61                | 6 MB / 245 MB       |  
| Pert2.txt    | 183 20          | 51                | 3 MB / 345 MB       |  
| Pert3.txt    | 596 57          | 157               | 23 MB / 245 MB      |  
| Pert4.txt    | 323 42          | 198               | 24 MB / 245 MB      |  
 --------------------------------------------------------------------------


NOTE: 
- Time and Memory might change, as you run the test the program on a 
  different system, but they could be comparable to the above values.
