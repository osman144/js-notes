# Binary Heap
Binary Heaps are Binary Trees with some rules. Binary Heaps are as compact as possible. Binary heaps have no order to the left or the right unlike a binary search tree. But similar to BSTs, can have up to two children. 

Binary heaps used to implement priority queues and also used with graph traversal algorithms. 


* **Min Binary Heap**: The parent nodes are always smaller than the child nodes. Every child node after the root should be greater. 

* **Max Binary Heap**: The parent nodes are always greater than the child nodes. The root is the largest node in the tree. Every child after the root should be smaller. Each parent has at most two child nodes. The value of each parent node is always greater than its child node. In a max binary heap, the parent is greater than the children but there are no guarantees between sibling nodes. 
	- All the children of each node are as full as they can be and left children are filled out first.   

## Representation
Since heaps are as compact as possible, we can expresss them as an array:
```
				    8
				   / \
				  7   3
				 / \ /
				5  6 2  
				|=> [8, 7, 3, 5, 6, 2]
```
Thus the child nodes and parent nodes are related by index as follows:
Formula for finding the child based off the parent. 
1. If parent is at index n:
* left child is at index 2n + 1
* right child is at index 2n + 2

2. If child is at index n, parent is at Math.floor((n-1)/2)
3. 
<img width="609" alt="Screen Shot 2022-03-09 at 7 43 47 PM" src="https://user-images.githubusercontent.com/25594064/157570660-76afc57b-d62a-4775-8ec1-a0f751c64442.png">

## Implementation
1. **Insert**: Used to insert a value to the heap. First the value is added to the array using ```push```. Then as long as the parent node is smaller then the current node, they are swapped with each other.
2. **Remove**: Used to remove a node from the heap. The node to be removed is swapped with the last node on the array and then removed using ```pop```. Then since a smaller element has risen to the top, this node is trickled down by swapping it with the larger child as long as either of the child has larger value than this node.
```javascript
class MaxBinaryHeap {
    constructor() {
        this.values = []
    }
    parentIndex(index) {
        if (index === 0) return 0;
        return Math.floor((index - 1) / 2)
    }
    parentValue(index) {
        return this.values[this.parentIndex(index)];
    }
    childIndexLeft(index) {
        let final = 2 * index + 1;
        if (final >= this.values.length) return index
        return final;
    }
    childIndexRight(index) {
        let final = 2 * index + 2;
        if (final >= this.values.length) return index
        return final;
    }
    childValueLeft(index) {
        return this.values[this.childIndexLeft(index)];
    }
    childValueRight(index) {
        return this.values[this.childIndexRight(index)];
    }
    insert(value) {
        this.values.push(value)
        let currentIndex = this.values.length - 1;
        while (this.parentValue(currentIndex) < this.values[currentIndex]) {
            [this.values[currentIndex], this.values[this.parentIndex(currentIndex)]] = [this.values[this.parentIndex(currentIndex)], this.values[currentIndex]]
            currentIndex = this.parentIndex(currentIndex);
        }
    }
    remove(value) {
        let currentIndex = this.values.indexOf(value);
        // swap with the last
        [this.values[currentIndex], this.values[this.values.length - 1]] = [this.values[this.values.length - 1], this.values[currentIndex]];
        this.values.pop();
        while (this.values[currentIndex] < this.childValueLeft(currentIndex) || this.values[currentIndex] < this.childValueRigth(currentIndex)) {
            if (this.childValueLeft(currentIndex) > this.childValueRigth(currentIndex)) {
                //swap with left
                [this.values[currentIndex], this.values[this.childIndexLeft(currentIndex)]] = [this.values[this.childIndexLeft(currentIndex)], this.values[currentIndex]];
                currentIndex = this.childIndexLeft(currentIndex);
            } else {
                // swap with right guy
                [this.values[currentIndex], this.values[this.childIndexRight(currentIndex)]] = [this.values[this.childIndexRight(currentIndex)], this.values[currentIndex]];
                currentIndex = this.childIndexRight(currentIndex);
            }
        }
    }
}
```

## Complexity
1. Insertion: log(n)
2. Removal: log(n)
3. Search: O(n)

## Priority Queue
A Priority Queue is a data structure where each element has a priority. Elements with higher priorities are served (retrieved) before elements with lower priorities. 

Generally priority queues are seperate from heaps. They aren't related at all. Priority queue is just a queue with set procedure for how the priority of elements will be handled. They are just an abstract concept and could be implemeted with something like an array, etc. A naive version is to store the elements in a list and iterate over the entire thing to find the highest priority element.

A lower number in this case denotes a higher priority. 
<img width="699" alt="Screen Shot 2022-03-09 at 10 24 52 PM" src="https://user-images.githubusercontent.com/25594064/157589228-5cba2fc9-cbc0-4cd5-bc42-37e9413b2941.png">

Used by the Operating System to execute important tasks first. Emergency room example, someone with a bad wound will be higher priority than someone with a minor ailment. 

Priority Queues are implemented using heaps since the root node is always the largest value. Thus the tasks are queued in a heap and when the root task is performed, it is removed as in above implementation and the next higher values comes to the top and so on. If instead arrays were used, we would take O(n) time to find the max which is slower.

> Project Ideas: Implement a todo list app using priority queue
