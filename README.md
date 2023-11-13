## Notes:

### Pointer => Reference in Memory

### JS has no inherent LL; But we create it through a class.
```
let linkedList = {
  head: {
    value: 
    next: => reference another obj in memory (pointer)
}

ex:
10 --> 5 --> 16

let myLinkedList = {
  head: {
    value: 10,
    next: {
      value: 5,
      next: {
        value: 16,
        next: null
      }
    }
}

class LinkedList {
  constructor(val) {
    this.head = {
      value: value,
      next: null
      //very first node in LL points to nothing (null)
    }
    this.tail = this.head;
  }
}

//instantiate a new linked list here
const myLinkedList = new LinkedList(10)

```
