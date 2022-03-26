# Dijkstra's Algorithm 
Dijkstra's Algorithm is an algorithm for finding the shortest paths between nodes in a graph. That is, we use it to find the shortest distance between two vertices on a graph. Depending on what the graph represents, we can find shortest routes, minimum costs, etc. all using this algorithm.


### Use
* GPS or mapping software, Network Routing, Biology, Airline tickets, etc

## Walking through the Algorithm
<img height="250" width="483" alt="Screen Shot 2022-03-22 at 8 40 57 PM" src="https://user-images.githubusercontent.com/25594064/159604985-b12a519d-5867-4a6b-9abf-df2967d54af3.png">

**Approach**:
1. Every time we look to visit a new node, we pick the node with the smallest known distance to visit first.
2. Once we've moved to the node we're going to visit, we look at each of its neighbors.
3. For each neighboring node, we calculate the distance by summing the total edges that lead to the node we're checking *from the starting node**
4. If the new total distance to a node is less than the previous total, we store the new shorter distance for that node. 

### Dijkstra Implementation with Simple/Naive Priority Queue

#### A Simple Priority Queue
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

#### Dijkstra's
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
  
  Dijkstra(start, finish){
    const nodes = new PriorityQueue();
    const distances = {};
    const previous = {};
    let path = [];
    let smallest;
    
    for(let vertex in this.adjacencyList){
      if(vertex === start){
        distances[vertex] = 0;
        nodes.enqueue(vertex, 0);
      }else{
        distances[vertex] = Infinity;
        nodes.enqueue(vertex, Infinity);
      }
      previous[vertex] = null;
    }
    // as long as there is something to visit
    while(nodes.values.length){
      smallest = nodes.dequeue().val;
      if(smallest === finish){
        // We are done
        // Build up path to return at end
        while(previous[smallest]){
          path.push(smallest);
          smallest = previous[smallest];
        }
      }
      if(smallest || distances[smallest] !== finish){
        for(let neighbor in this.adjacencyList[smallest]){
          // find neighboring node
          let nextNode = this.adjacencyList[smallest][neighbor];
          // calculate new distance to neighboring node
          let candidate = distances[smallest] + nextNode.weight;
          let nextNeighbor = nextNode.node; 
          if(candidate < distances[nextNode.node]){
            // updating new smallest distance to neighbor
            distances[nextNode.node] = candidate;
            // updating previous - how we got to neighbor
            previous[nextNeighbor] = smallest;
            // enqueue in priority queue with new priority
            nodes.enqueue(nextNeighbor, candidate);
          }
        }
      }
    }
    return path.concat(smallest).reverse();
  }
}
```

### Dijkstra Implementation with Binary Heap Priority Queue

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
  
  Dijkstra(start, finish){
    const nodes = new PriorityQueue();
    const distances = {};
    const previous = {};
    let path = [];
    let smallest;
    
    for(let vertex in this.adjacencyList){
      if(vertex === start){
        distances[vertex] = 0;
        nodes.enqueue(vertex, 0);
      }else{
        distances[vertex] = Infinity;
        nodes.enqueue(vertex, Infinity);
      }
      previous[vertex] = null;
    }
    // as long as there is something to visit
    while(nodes.values.length){
      smallest = nodes.dequeue().val;
      if(smallest === finish){
        // We are done
        // Build up path to return at end
        while(previous[smallest]){
          path.push(smallest);
          smallest = previous[smallest];
        }
      }
      if(smallest || distances[smallest] !== finish){
        for(let neighbor in this.adjacencyList[smallest]){
          // find neighboring node
          let nextNode = this.adjacencyList[smallest][neighbor];
          // calculate new distance to neighboring node
          let candidate = distances[smallest] + nextNode.weight;
          let nextNeighbor = nextNode.node; 
          if(candidate < distances[nextNode.node]){
            // updating new smallest distance to neighbor
            distances[nextNode.node] = candidate;
            // updating previous - how we got to neighbor
            previous[nextNeighbor] = smallest;
            // enqueue in priority queue with new priority
            nodes.enqueue(nextNeighbor, candidate);
          }
        }
      }
    }
    return path.concat(smallest).reverse();
  }
}

class Node {
    constructor(val, priority) {
    	// val doesn't matter
	    // heap is constructed using priority
    	this.val = val;
	    this.priority= priority;
    }
}

class PriorityQueue {
    constructor() {
        this.values = []
    }
    /** enqueue method accepts a value and priority, makes a 
    new node, and puts it in the right spot */
    
    // enqueue 
    enqueue(val, priority){
    	let newNode = new Node(val, priority);
    	this.values.push(newNode);
	    this.bubbleUp();
    }
    
    bubbleUp(){
      let index = this.values.length - 1;
	    const element = this.values[index];
      
	    while(index > 0){
		    let parentIndex = Math.floor((index - 1)/2);
		    let parent = this.values[parentIndex];
		    if(element.priority <= parent.priority) break;
		    this.values[parentIndex] = element;
		    this.values[index] = parent;
		    index = parentIndex;
    }
    
    /** dequeue method removes root element, returns it, and rearranges heap 
    using priority */
    
    // dequeue will remove by largest priority first
    dequeue(){
      const max = this.values[0];
	    const end = this.values.pop();
	    if(this.values.length > 0){
		    this.values[0] = end;
		    this.sinkDown();
	    }
	    return max;
    }
    
    sinkDown(){
      let index = 0;
	    const length = this.values.length;
	    while(true){
		    let leftChildIndex = 2 * index + 1;
		    let rightChildIndex = 2 * index + 2;
		    let leftChild, rightChild;
		    let swap = null;
		
		    if(leftChildIndex < length){
			    leftChild = this.values[leftChildIndex];
			    if(leftChild.priority > element.priority){
				  swap = leftChildIndex;
			     }
		    }
    
        if(rightChildIndex < length){
          rightChild = this.values[rightChildIndex];
          if(
             (swap === null && rightChild.priority > element.priority) || 
             (swap !== null && rightChild.priority > leftChild.priority)
          ){
              swap = rightChildIndex;
           }
        }
        if(swap === null) break;
        this.values[index] = this.values[swap];
        index = swap;
	    }
    }
}
```

