# Tree Traversal
Traversing a tree means visiting every node on the tree once.

We can use BFS and DFS to traverse the tree. 

## Types:
1. Breadth First Search
2. Depth First Search
	1. DFS PreOrder
	2. DFS PostOrder
	3. DFS Inorder

## BFS:

To implement BFS, we use queues. We start by adding the root node to the queue. Then as long as the queue is not empty we follow the following algorithm:
1. Dequeue a node
2. Add its value to the list
3. Queue its left and right parameters to the queue

```javascript
// Inside Binary Search Class from previous section
    BFS() {
        let node = this.root;
	let queue = [];
	let data = [];
	
	queue.push(node);
	while(queue.length){
		// Shift removes value from queue 
		// Add current node to data;
		node = queue.shift();
		data.push(node.value);
		if(node.left) queue.push(node.left)
		if(node.right) queue.push(node.right);
	}
	return data;
    }
```

## DFS:
https://www.youtube.com/watch?v=WLvU5EQVZqY

We implement DFS recursively. When we encounter a node, we can do things in three different ways

1. PreOrder:

	**Tip**: This one is the "normal" one where you just go down the tree and record the node as you visit it. Print the nodes as you visit them for the first time. 
	1. Add the node value to the list.
	2. Encounter the left node
	3. Encounter the right node
	4. 
<img width="300" alt="Screen Shot 2022-04-03 at 1 14 23 AM" src="https://user-images.githubusercontent.com/25594064/161414451-6745f25b-6ad3-42a6-bc64-a1885bfad7aa.png">

2. PostOrder

	**Tip**: For Post-order, print the nodes when you visit them for the last time or third time.
	1. Encounter the left node
	2. Encounter the right node
	3. Add the node value to the list

3. InOrder

	**Tip**: Only record node once we've visited or "seen" it twice. Print the nodes only when you visit them for the second time. 
	1. Encounter the left node
	2. Add the node value to the list
	3. Encounter the right node

```javascript
// Inside Binary Search Class from previous section
    DFSPreOrder() {
        let list = [];

        function searchRecursive(node) {
            list.push(node.data);
            if (node.left != null) searchRecursive(node.left)
            if (node.right != null) searchRecursive(node.right)
        }
        searchRecursive(this.root);
        return list;
    }
    DFSPostOrder() {
        let list = [];

        function searchRecursive(node) {
            if (node.left != null) searchRecursive(node.left)
            if (node.right != null) searchRecursive(node.right)
            list.push(node.data);
        }
        searchRecursive(this.root);
        return list;
    }
    DFSInOrder() {
        let list = [];

        function searchRecursive(node) {
            if (node.left != null) searchRecursive(node.left)
            list.push(node.data);
            if (node.right != null) searchRecursive(node.right)
        }
        searchRecursive(this.root);
        return list;
    }
```

## BFS vs DFS
Time complexity for all four methods is same as we visit all the nodes once. But BFS takes more memory if we have a really dense tree due to the queue. When traversing, BFS stores the width in the memory whereas DFS stores the depth in the memory.

Space complexity depends on the tree. If wide tree, probably better to use depth first as breadth first may take up a lot of space. If its a deep tree, may be better to use breadth first as depth first could take up a lot of space.

wide tree --> depth first search (DFS)
deep tree --> breadth first search (BFS)

### Summary
- Trees are non-linear data structures that contain a root and child nodes. 
- Binary Trees can have values of any type. But at most two children for each parent.
- Binary Search Trees are a more specific version of binary trees where every node to the left of a parent is less than it's value and every node to the right is greater. 
- Can search through Trees using BFS and DFS. 
