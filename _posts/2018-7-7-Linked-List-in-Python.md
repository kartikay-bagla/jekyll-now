---
layout: post
title: Linked List Implementation in Python
---

I've started learning different Data Structures and Algorithms. So I began with Linked Lists. It contains basic features like indexing, inserting, removing and a binary search.

Here is the repo with my code - [https://github.com/kartikay-bagla/linked-list-in-python](https://github.com/kartikay-bagla/linked-list-in-python)

Every algorithm in there is either in O(1) or O(n) time.

Here is a step wise explanation for the code:

1.  Created a Node class to store the elements of the linked list
```python
class Node(object):
    """Node class for Linked List. Each node has its data and a reference to the next node."""
    def __init__(self, data):
        """Initializes the data of the node and sets the nextNode to None"""
        self.data = data
        self.nextNode = None
```

2.  Then I added a remove recursive remove method to remove the data from the Node and the next Nodes.
    *   If the data to be removed is in the current node, delete the current node and link the previous node to the next node.
    *   Else call the function again on the next node in the series
```python
def remove(self, data, previous):
    """Removes the data from the linked lists"""
    if self.data == data:
        previousNode.nextNode = self.nextNode
        del self.data
        del self.nextNode
    else:
        if self.nextNode is not None:
            self.nextNode.remove(data, self)
```

3.  Now its time to create the Linked List class which uses the Node class we created previously to store data
```python
class LinkedList(object):
    """Linked Lists implementation in python"""
    def __init__(self):
        """Initalizes the head as None and sets the counter to 0"""
        self.head = None
        self.counter = 0
```

4.  To add elements, there are 2 options with different time complexities.
    *   If we add an element to the start, we can do that in O(1) time. To do this we:
        *   First increase the counter to show keep track of the lenght of the list
        *   Create a Node from the data
        *   Now we check if the linked list is empty i.e. self.head is None then we assign the new Node to self.head
        *   However if that's not the case, we set the current node as the head and link the previous head node as the current node's next node.
    ```python
    def insertStart(self, data):
        """Inserts the data as a node in O(1) time."""
        self.counter += 1
        newNode = Node(data)
        if self.head == None:
            self.head = newNode 
        else:
            newNode.nextNode = self.head
            self.head = newNode
    ```
    *   If we add an element to end or in between, we have to do that in O(n) time. To do that we:
        *   First increase the counter to show keep track of the lenght of the list
        *   Create a Node from the data
        *   Move through the list till we reach the index or the end
        *   When we reach the index specified, we change the data's next node to be the node after the index and we change the index node's next node to be the new node
        *   If we're inserting at index and Node.nextNode is None, we get an Attribute error which is caught and then raises an IndexError to the user
    ```python
    def insertEnd(self, data):
        """Inserts an element in the end of the linked list in O(n) time."""
        self.counter += 1
        if self.head == None:
            self.insertStart(data)
        else:
            newNode = Node(data)
            actualNode = self.head
            while actualNode.nextNode is not None:
                actualNode = actualNode.nextNode
            actualNode.nextNode = newNode

    def insertIndex(self, index, data):
        """Inserts data at index i in O(n) time."""
        actualNode = self.head
        try:
            for i in range(index - 1):
                actualNode = actualNode.nextNode
        except:
            raise IndexError
        self.counter += 1 #Increment the counter
        newNode = Node(data)
        newNode.nextNode = actualNode.nextNode
        actualNode.nextNode = newNode
    ```

5.  To remove elements via data, we use the recursive Node.remove function
```python
def remove(self, data):
    """Removes the data from the linked list in O(n) time."""
    if self.counter == 0:
        raise IndexError  #If the list is empty, return
    else:
        self.counter -= 1   #Else decrement the counter
    if self.head:
        if data == self.head.data:
            self.head = self.head.nextNode
        else:
            self.head.remove(data, self.head)
```
6.  The search function moves through the list checking each element in the list checking for a match and returns the index if a match is found else it returns None
```python
def search(self, data):
    """Returns the index of the first occurence of data in the linked list. Returns None if element not in list"""
    #Check if head is none. If not then check that data = self.head and return 0.
    #Else keep moving on to next nodes and incrementing the index counter
    #return index if element is found else return None
    currentNode = self.head
    index = 0
    if currentNode == None:
        return None

    if data == currentNode.data:
        return index 
    else:
        while currentNode.nextNode is not None:
            currentNode = currentNode.nextNode
            index += 1
            if data == currentNode.data:
                return index
        return None
```

7.  The rest are trivial functions to extend the usability of the Linked List module which are self explanatory

I'll be covering more and more Data Structures as I keep learning them so stay tuned!