# Doubly Linked List
Collection of nodes each node containing a value and pointer to the **next** and the **previous** node. Compared to Singly Linked Lists, double linked lists use more memory which equals more flexibility.

- Browser history is organized using doubly linked list type of data structure. 
- Better than Singly Linked Lists for finding nodes and can be done in half the time.
- However, they do take up more memory considering the extra pointer. 

> If a parameter is not passed to a function, that parameter gets the value of undefined.
>https://www.freecodecamp.org/news/copying-stuff-in-javascript-how-to-differentiate-between-deep-and-shallow-copies-b6d8c1ef09cd/

<img width="629" alt="Screen Shot 2021-11-28 at 4 22 51 PM" src="https://user-images.githubusercontent.com/25594064/143788443-b98f3bd8-a52d-48cf-abd5-71675ab64862.png">

## Complexity

Big O of Doubly Linked Lists

1. Search: O(n), technically search is O(N/2) but that's still O(N). 
2. Access: O(n)
3. Delete: O(n) or O(1)
4. Insert: O(n) or O(1)

> Faster than or same speed as singly linked list

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

## Implemetation
```javascript
class Node {
    constructor(val) {
        this.val = val;
        this.prev = null;
        this.next = null;

    }
}

class DoublyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
        this.length = 0;
    }

    push(val) {
        let newNode = new Node(val);
        if (this.length === 0) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            this.tail.next = newNode;
            newNode.prev = this.tail;
            this.tail = newNode;
        }
        this.length++;
        return this.length;
    }
    pop() {
        if(!this.head) return undefined;
        let poppedNode = this.tail;
        if(this.length === 1){
            this.head = null;
            this.tail = null;
        } else{
            this.tail = poppedNode.prev;
            this.tail.next = null;
            poppedNode.prev = null;
        }
        this.length--;
        returned poppedNode;
    }
    shift() {
        // **Removing** a node from the beginning of the Doubly Linked List
        if (this.length === 0) return undefined;
        let oldHead = this.head;
        if(this.length === 1){
            this.head = null;
            this.tail = null;
        } else {
            this.head = oldHead.next;
            this.head.prev = null;
            oldHead.next = null;
        }
        this.length--;
        return oldHead;
    }
    unshift(val) {
        // **Adding** a node to beginning of Doubly Linked List
        let newNode = new Node(data);
        if (this.length === 0) {
            this.head = newNode;
            this.tail = newNode;
        } else {
            this.head.prev = newNode;
            newNode.next = this.head;
            this.head = newNode;
        }
        this.length++;
        return this;
    }
    get(index) {
        // Accessing a node in a Doubly Linked List by its position
        if (index < 0 || index >= this.length) return null;
        let count, current;
        if (index <= this.length / 2) {
            count = 0;
            let current = this.head;
            while(count !== index){
                current = current.next;
                count++;
            }
            return current;
        } else {
            count = this.length - 1;
            current = this.tail;
            while(count !== index){
                current = current.prev;
                count--;
            }
            return current;
        }
    }
    set(index, val) {
        // Replacing the value of a node in a Doubly Linked List
        let foundNode = this.get(index);
        if(foundNode != null){
            foundNode.val = val;
            return true;
        }
        return false;
    }
    insert(index, val) {
        if(index < 0 || index > this.length) return false;
        if(index === 0) return this.unshift(val);
        if(index === this.length) return this.push(val);
        
        let newNode = new Node(val);
        let beforeNode = this.get(index-1);
        let afterNode = beforeNode.next;
        
        beforeNode.next = newNode;
        newNode.prev = beforeNode;
        newNode.next = afterNode;
        afterNode.prev = newNode;
        this.length++;
        return true;
    }
    remove(index) {
        // Removing a node in a Doubly Linked List by a certain position
        if(index < 0 || index >= this.length) return undefined;
        if(index === 0) return this.shift();
        if(index === this.length - 1) return this.pop();
        let removedNode = this.get(index);
        removedNode.prev.next = removedNode.next;
        removedNode.next.prev = removedNode.prev;
        removedNode.next = null;
        removedNode.prev = null;
        this.length--;
        return removedNode;
    }
    reverse() {
        let iterator = this.head;
        while(iterator){
            let temp = iterator.next;
            iterator.next = iterator.previous;
            iterator.previous = temp;
            iterator = iterator.previous;
        }
        let temp = this.head;
        this.head = this.tail;
        this.tail = temp;
    }
    traverse() {
        let iterator = this.head;
        while (iterator) {
            console.log(iterator.data);
            iterator = iterator.next;
        }
        return this.length;
    }
}
```
