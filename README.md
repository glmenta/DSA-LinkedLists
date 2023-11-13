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

//keep DRY
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}
//This class creates a new node for our linked list 
class LinkedList {
  constructor(val) {
    this.head = {
      value: value,
      next: null
      //very first node in LL points to nothing (null)
    }
    this.tail = this.head;
    //tail === head b/c it is a singular node at this point
    this.length = 1;
  }

//Append => add to our linked list node
  append(val) {
    //create our new node
    const newNode = {
      val: val,
      next: null
    }

    //If we implement our own class for Node we can just do newNode = new Node(val)

    //point tail to new node
    this.tail.next = newNode;
    this.tail = newNode;
    this.length++
    return this;
  }

//Prepend => add to beginning of LL
  prepend(val) {
    const newNode = {
      val: val
      next: null
    }

    //create a pointer that points to our this.head
    newNode.next = this.head;

    //update reference for our head
    this.head = newNode;

    this.length++;
    return this;
  }
}



//instantiate a new linked list here
const myLinkedList = new LinkedList(10)
myLinkedList.append(5)
myLinkedList.append(16)
```
