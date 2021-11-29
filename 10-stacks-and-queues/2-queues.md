# Queues
FIFO. Used in download managers, printing several documents etc.

## Complexity
1. ```queue``` and ```dequeue``` are constant time. (Array implementation is not)

## Implementation

1. **Using Arrays**
```javascript
let a = [1, 2, 3];
a.push(4);
a.shift();
// 1
```

2. **Using Classes**
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}

class Queue {
    constructor() {
        this.first = null;
        this.last = null;
        this.size;
    }
    enqueue(val) {
        let newNode = new Node(val);
        if(!this.first){
            this.first = newNode;
            this.last = newNode;
        } else {
            this.last.next = newNode;
            this.last = newNode;
        }
        return ++this.size;
    }

    dequeue() {
        if(!this.first) return null;
        
        let temp = this.first;
        if(this.first === this.last){
            this.last = null;
        }
        this.first = this.first.next;
        this.size--;
        return temp.value;
    }
}
```
