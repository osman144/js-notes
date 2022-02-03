# Singly Linked List
- A linked list is a data structure that contains a head, tail, and length property. Head is the beginning and tail is the end. 
- Linked lists consists of nodes, and each node has a value and a pointer to another node or null. 
- Train car analogy. Or building analogy, if you want to go to the 5th floor using the stairs, you'll have to start at the first and go through each floor. 
- Singly linked lists are connected in one direction. 

Linked lists are a collection of nodes each node containing a value and pointer to the next node.

### Linked Lists vs Arrays 

- **Linked Lists**: Do not have indexes, connected via nodes with a next pointer, random access is not allowed
- **Arrays**: Indexed in order, there is an order to it. Insertion and deletion can be expensive. Can quickly be accessed at a specific index. 

>In JavaScript, ```undefined``` means a variable has been declared but has not yet been assigned a value.<br>
```null``` is an assignment value. It can be assigned to a variable as a representation of no value

>Javascript is garbage collected, you don't need to delete objects themselves - they will be removed when there is no way to refer to them anymore.

## Complexity
1. Search: O(n)
2. Access: O(n)
3. Delete: O(1), it depends on where were removing from O(N), constant time if removing from beginning of list, but if removing from elsewhere, need to find item right before the tail which involves iterating through the list. 
5. Insert: O(1)

> Singly Linked List are better than arrays when insertion and deletion at the end and at the start is required. Accessing is difficult in linked lists.
> Arrays contain a built in index whereas Linked Lists do not.
> The idea of list data structure that consists of nodes is the foundation for other data structures like Stacks and Queues. 

## Methods
1. ```push(data)```: Works same as ```push``` of array
2. ```pop()```: Works same as ```pop``` of array
3. ```shift()```: Works same as ```shift``` of array
4. ```unshift(data)```: Works same as ```unshift``` of array
5. ```get(index)```: Gets the node at given index
6. ```set(index)```: Sets the node data at given index
7. ```insert(index, data)```: Inserts a node with given data at the given index
8. ```remove(index)```: Removes the node at the index
9. ```reverse()```: Reverses the list
10. ```traverse()```: Logs the list on the console


## Implementation
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class SinglyLinkedList {
    constructor() {
        this.length = 0;
        this.head = null;
        this.tail = null;
    }

    push(val) {
        let newNode = new Node(val);
        if (!this.head) {
            // Empty list
            this.head = newNode;
            this.tail = this.head;
        } else {
            this.tail.next = newNode;
            this.tail = newNode;
        }
        this.length++;
        return this;
    }
    pop() {
        // if no node in list, return undefined
        if (!this.head) return undefined;
        
        // Find the second last node
        let current = this.head;
        let newTail = current;
        while (current.next) {
            newTail = current;
            current = current.next;
        }
        this.tail = newTail;
        this.tail.next = null;
        this.length--;
        if (this.length === 0) {
            this.head = null;
            this.tail = null;
        }
        return current;
    }
    shift() {
        if (!this.length) return undefined;
        let currentHead = this.head
        this.head = currentHead.next
        this.length--;
        if (this.length === 0) {
            this.tail = null;
        }
        return currentHead;
    }
    unshift(val) {
        let newNode = new Node(val)
        if (!this.head) {
            this.head = newNode;
            this.tail = this.head;
        }else{
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }
    traverse() {
        let iterator = this.head;
        while (iterator) {
            console.log(iterator.val);
            iterator = iterator.next;
        }
    }
    get(index) {
        if(index < 0 || index >= this.length) return null;
        let counter = 0;
        let current = this.head;
        while(counter !== index){
            current = current.next;
            counter++;
        }
        return current;
    }
    set(index, val) {
        // Changing the value of a node based on it's position in a Linked List
        let foundNode = this.get(index);
        if(foundNode){
            foundNode.val = val;
            return true;
        }
        return false;
    }
    insert(index, data) {
        if(index < 0 || index > this.length) return false;
        if(index === this.length){
           this.push(val);
           return true;
        }
        if(index === 0) return this.unshift(val);
        let newNode = new Node(val);
        let prev = this.get(index - 1);
        let temp = prev.next;
        prev.next = newNode;
        newNode.next = temp;
        this.length++;
        return true;
    }
    remove(index) {
        if(index < 0 || index > this.length) return undefined;
        if(index === 0) return this.shift();
        if(index === this.length - 1) return this.pop();
        let previousNode = this.get(index - 1);
        let removed = previousNode.next;
        previousNode.next = removed.next;
        this.length --;
        return removed;
    }
    reverse() {
        let node = head, previous,tmp;
        
        while (node) {
          // save next before we overwrite node.next!
          tmp = node.next;

          // reverse pointer
          node.next = previous;

          // step forward in the list
          previous = node;
          node = tmp;
        }
        
        return previous;
    }
}

let list = new SinglyLinkedList()
// do stuff here like list.push("Hello")
```
