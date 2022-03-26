# Dijkstra's Algorithm 

### Use
* GPS or mapping software, Network Routing, Biology, Airline tickets, etc

### Weighted Graph

```javascript
class WeightedGraph {
  constructor(){
    this.adjacencyList = {};
  }
  
  addVertex(vertex){
    if(!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
  }
  addEdge(vertex1, vertex2, weight){
    this.adjacencyList[vertex1].push({node: vertex2, weight});
    this.adjacencyList[vertex2].push({node: vertex1, weight});
  }
}
```

## Walking through the Algorithm
<img height="250" width="483" alt="Screen Shot 2022-03-22 at 8 40 57 PM" src="https://user-images.githubusercontent.com/25594064/159604985-b12a519d-5867-4a6b-9abf-df2967d54af3.png">

**Approach**:
1. Every time we look to visit a new node, we pick the node with the smallest known distance to visit first.
2. Once we've moved to the node we're going to visit, we look at each of its neighbors.
3. For each neighboring node, we calculate the distance by summing the total edges that lead to the node we're checking *from the starting node**
4. If the new total distance to a node is less than the previous total, we store the new shorter distance for that node. 


### A Simple Priority Queue
Notice we are sorting which is O(N * log(N))

```javascript
class PriorityQueue {
  constructor(){
    this.values = [];
  }
  
  enqueue(val, priority){
    this.values.push({val, priority});
    this.sort();
  }
  
  dequeue(){
    return this.values.shift();
   };
   
   sort(){
    this.values.sort((a, b) => a.priority - b.priority);
   };
}
```
