# Stacks

Last in First Out. Used in browser history, call stacks, undo/redo etc. More than one way to create a stack. Its just a concept and it has to follow the LIFO rule. 

## Complexity
1. ```push``` and ```pop``` are constant time. (Array implementation is not)

## Implementation

1. **Using Arrays**
```javascript
let a = [1, 2, 3];
a.push(4);
a.pop();
// 4
```

2. **Using Classes**
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}

class Stack {
    constructor() {
        this.first = null;
        this.last = null;
        this.size = 0;
    }
    push(data) {
        let newNode = new Node(val);
        if(!this.first){
            this.first = newNode;
            this.last = newNode;
        } else {
            let temp = this.first;
            this.first = newNode;
            this.first.next = temp;
        }
        return ++this.size;
    }
    pop() {
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
