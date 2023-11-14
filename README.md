## Notes:

### Pointer => Reference in Memory

### JS has no inherent LL; But we create it through a class.

### Singly vs Doubly:
    -Singly => better if its for fast insert/deletion but slower if bigger data 
    -Doubly => Can traverse forward/backward, deleting does not require to start from head and requires more memory
    
### Singly Linked Lists
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

//printList => create arr for our LL
printList() {
  const array = [];
  let currNode = this.head;

  //keep looping until we are at the tail
  while (currNode !== null) {
    array.push(currNode.val)

    //reassign currNode for our iteration to keep going
    currNode = currNode.next
  }
  return array;
}

//Insert =>Add in between nodes/certain index
  //traverse until we hit index, create new node, create new node pointer old node in that target index, change idx.next to newnode
  insert(idx,val) {
    //case if we are inserting at the beginning:
    if (idx === 0) {
      this.prepend(val);
      return this.printList()
    //case if we are inserting at an index beyond/equal to our LL length 
    } else if (idx >= this.length) {
      return this.append(val)
    }
    const newNode = new Node(val)

    //traverseToIndex takes in the previous index/node before our target index
    const leadNode = this.traverseToIndex(idx - 1)
    const holdPointer = leadNode.next;
    leadNode.next = newNode;
    newNode.next = holdPointer
    this.length++
    return this.printList();
  }

//remove an index
  remove(idx) {
    //grabs node of the idx to the left of the target idex
    const leadNode = this.traverseToIndex(idx - 1)
    const removeNode = leadNode.next;
    leadNode.next = removeNode.next;
    this.length--
    return this.printList();
  }

  traverseToIndex(idx) {
    let counter = 0;
    let currNode = this.head;

    while(counter !== idx) {
      currNode = currNode.next
      counter++
    }
    return currNode
  }

  reverse() {
    if (!this.head.next) {
      return this.head;
    }

    let firstNode = this.head;
    this.tail = this.head;
    let secondNode = this.head.next;

    //Loop goes as long as our node exists
    while (secondNode !== null) {
      //var to store reference for our node's pointer val (next node)
      const temp = secondNode.next;
      //point our node back to the previous node (flip the arrow)
      secondNode.next = firstNode
      //reassign our 
      firstNode = secondNode;
      secondNode = temp;
    }
    this.head.next = null;
    this.head = firstNode;
  }
}



//instantiate a new linked list here
const myLinkedList = new LinkedList(10)
myLinkedList.append(5)
myLinkedList.append(16)
myLinkedList.prepend(1) 1 -> 10 -> 5 -> 16
myLinkedList.insert(2,99) 1 -> 10 -> 99 -> 5 -> 16
myLinkedList.insert(20,69) 1 -> 10 -> 99 -> 5 -> 16 -> 69
```

### Doubly Linked Lists

```
  class DoublyLinkedList {
    constructor(val) {
      this.head = {
        val: val,
        next: null,
        prev: null
      }
      this.tail = this.head;
      this.length = 1;
    }
    append(val) {
      const newNode = {
        val: val,
        next: null,
        prev: null
      }
      newNode.prev = this.tail,
      this.tail.next = newNode
      this.tail = newNode
      this.length++
      return this;
    }
    prepend(val) {
      const newNode = {
        val: val,
        next: null,
        prev: null
      }
    //create a pointer that points to our this.head
    newNode.next = this.head;
    this.head.prev = newNode;

    //update reference for our head
    this.head = newNode;

    this.length++;
    return this;
    }

//Insert =>Add in between nodes/certain index
  //traverse until we hit index, create new node, create new node pointer old node in that target index, change idx.next to newnode
  insert(idx,val) {
    //case if we are inserting at the beginning:
    if (idx === 0) {
      this.prepend(val);
      return this.printList()
    //case if we are inserting at an index beyond/equal to our LL length 
    } else if (idx >= this.length) {
      return this.append(val)
    }
    const newNode = {
        val: val,
        next: null,
        prev: null
    }

    //traverseToIndex takes in the previous index/node before our target index
    const leadNode = this.traverseToIndex(idx - 1)
    const follower = leadNode.next;
    leadNode.next = newNode;
    newNode.next = follower

    newNode.prev = leadNode
    follower.prev = newNode

    this.length++
    return this.printList();
    }

//remove an index
  remove(idx) {
    //grabs node of the idx to the left of the target idex
    const leadNode = this.traverseToIndex(idx - 1)

    if (!leadNode || !leadNode.next) {
      return this.printList();
    }
    const removeNode = leadNode.next;
    const nextNode = removeNode.next;

    leadNode.next = nextNode;

    if (nextNode) {
      nextNode.prev = leadNode;
    }

    this.length--
    return this.printList();
  }
}
```
