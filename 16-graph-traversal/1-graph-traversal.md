# Graph Traversal
Traversal generally means visiting/updating/checking each vertex in a graph. It does not necessarily mean were searching for something. 

Unlike a tree there is no "head" or root starting point. Can choose any point to start from. 

Sometimes usually have to do backtracking or re-visit a node you've already been to unlike a tree. 

**DFS uses a stack data structure in its implementation. BFS will use a queue data structure.**

### Use Case
Graph Traversal Common Uses:
1. Peer to peer networking
2. Web crawlers
3. Find "closest" matches/recommendations
4. Shortest path problems
   * GPS Navigation
   * Solving mazes
   * AI (shortest path to win the game) 

## Depth First Search
Going deep from parent to child down one path before choosing another. Or in the case of a graph structure, following the neighbors and continuing to follow neighbors before backtracking. 

Two ways to implement a DFS: Iterative and Recursive

- When doing DFS, pick a starting point (maybe the lowest value if applicable) and then go down one path, following its neighbors, keep going down one path as this is DFS where we pick a path and follow it to to some destination. 
- DFS = explore as far as possible down one branch before "backtracking".
- For DFS its important to remember where visited so can backtrack as needed. 


### DFS Implementation
```javascript
class Graph {
	constructor(){
	    this.adjacencyList = {};
	}
	
	// adding vertex
	addVertex(vertex){
	    if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
	}
	// adding edge
	addEdge(v1,v2){
	    this.adjacencyList[v1].push(v2);
	    this.adjacencyList[v2].push(v1);
	}
	
	// removing edge
	removeEdge(vertex1, vertex2){
	    this.adjacencyList[vertex1] = this.adjacencyList[vertex1].filter(
	      v => v !== vertex2
	    );
	    this.adjacencyList[vertex2] = this.adjacencyList[vertex2].filter(
	      v => v !== vertex1
	    );
	}
	// removing vertex
	removeVertex(vertex){
	    while(this.adjacencyList[vertex].length){
	    	const adjacentVertex = this.adjacencyList[vertex].pop();
		this.removeEdge(vertex, adjacentVertex);
	    }
	    delete this.adjacencyList[vertex];
	}
  
  // Recursive solution
  depthFirstRecursive(startVertex){
      const result = [];
      const visited = {};
      // preserving the 'this' for adjacency list, context changes in the function         // below
      const adjacencyList = this.adjacencyList;
      
      // IIFE
      (function dfs(vertex){
         if(!vertex) return null;
         visited[vertex] = true;
         result.push(vertex);
         adjacencyList[vertex].forEach(neighbor => {
            if(!visited[neighbor]){
              return dfs(neighbor);
            }
         }) 
      })(start);
      
      return result; 
  }
  
  // Iterative solution
  depthFirstIterative(start){
      const stack = [start];
      const result = [];
      const visited = {};
      let currentVertex;
      
      visited[start] = true;
      while(stack.length){
          currentVertex = stack.pop();
          result.push(currentVertex);
          
          this.adjacencyList[currentVertex].forEach(neighbor => {
            if(!visited[neighbor]){
              visited[neighbor] = true;
              stack.push(neighbor);
            }
          });
      };
      return result;
  }
  
  // BFS 
  breadthFirst(start){
      const queue = [start];
      const result = [];
      const visited = {};
      let currentVertex;
      visited[start] = true;
      
      while(queue.length){
           currentVertex = queue.shift();
	   result.push(currentVertex);
	   
	   this.adjacencyList[currentVertex].forEach(neighbor => {
	   	if(!visited[neighbor]){
		     visited[neighbor] = true;
		     queue.push(neighbor);
		}
	   })
      };
      
      return result;
  }
  
}


```
