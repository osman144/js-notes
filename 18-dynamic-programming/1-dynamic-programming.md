# Dynamic Programming
A method for solving a complex problem by breaking it down into a collection of simpler subproblems, solving each of those subproblems just once, and storing their solutions. 

To put it simply, only some problems can be solved with this method, most problems can't be solved with this method. The ones that can be solved with dynamic programming, it can make a huge difference in performance. 

Only works on problems with:
* Optimal substructure and overlapping subproblems 

**Overlapping Subproblems**: A problem has overlapping subproblems if it can be broken down into subproblems which are reused several times. 

**Optimal Substructure**: A problem has optimal substructure if an optimal solution can be constructed from optimal solutions of its subproblems. 

* Fibonacci Sequence, this has overlapping subproblems and optimal subproblems. 
* Shortest Path, finding the optimal solution with weights along the edges. But finding longest path does not exhibit optimal substructure. 

#### Time complexity of Fibonacci solution
Fibonacci tree grows very rapidly with each additional level or value added. Grows at an exponential level: O(2^n) 

Time can reduced with with memoization. 

<img width="605" alt="Screen Shot 2022-03-26 at 1 30 23 PM" src="https://user-images.githubusercontent.com/25594064/160252583-8732c12c-8b13-4683-a933-a23dcb871bd4.png">



### Memoization 
Storing the results of expensive function calls and returning the cached result when the same inputs occur again. 


<img width="498" alt="Screen Shot 2022-03-26 at 2 00 29 PM" src="https://user-images.githubusercontent.com/25594064/160253511-47173ebb-df0b-4747-b54e-31ec7a449a99.png">


<img width="518" alt="Screen Shot 2022-03-26 at 2 02 25 PM" src="https://user-images.githubusercontent.com/25594064/160253566-58489865-91f5-4310-9a30-ce88f1e6a593.png">
