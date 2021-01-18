---
layout: article
title: Arrays, Lists, Stacks, Queues
show_edit_on_github: false
tags: DSA interview-prep

---

This post is part of a series on Data Structures and Algorithms (DSA). The series is a collection of notes that I read for interview prep as a refresher from originally learning the concepts in my undergrad. So while the concepts covered in these posts can be a good first-entry into DSA, some concepts are touched on in passing and the deep levels of detail (beyond that which is necessary as a job-hunt refresher) are largely ommitted.

The `DSA` tag can be used to find other blog posts on DSA concepts.
# Arrays
----------

Arrays are the most basic Data Structure in Computer Science. An array is a contiguous section of memory. 

- Each array member is a chunk of preset memory size.
- Each element/chunk can be indexed by an integer.


![Data Structure - Array](https://beginnersbook.com/wp-content/uploads/2018/10/array.jpg)


The size of each chunk depends on what data type the array is for.

**Arrays allow for random access. O(1) constant time access to any member in the array.** This is because the array elements are of known width, accessing the nth element can be done by accessing the array[0] memory address plus n*element_size bits along to reach the element stored in memory for array[n].


- Constant time access
- Must be declared with a set size, because the memory is **contiguous**

**2D arrays**
A 2D array is really a single contiguous 1d array in memory. We know the row size, so we can offset our memory access by an entire row’s length to access an element in the second row. 

**Operation Times**

- Adding/Removing an element at the end of the array is an **O(1) operation.**
- Adding/Removing an element in the middle, or at the beginning, of the array is an **O(n) operation** as we have to shift the remaining ‘n’ elements in the array down by one index.
# Lists
----------

A linked list can be of arbitrary length and can store arbitrary data


## Singly Linked List

Each element in a singly linked list has two components: The stored data itself, and a pointer to the memory location of the next list element. 

![Data Structure : Singly Linked list](https://codeforwin.org/ezoimgfmt/secureservercdn.net/160.153.138.219/b79.d22.myftpupload.com/wp-content/uploads/2015/09/Singly-linked-list.png?ezimgfmt=rs:392x193/rscb1)


To access the *mth* element, it takes *m* operations as one must follow each pointer until you do so *m* times. At compile time it is not known where each element will lie in memory.


- Add & Remove front: O(1)
- Add & Remove rear/middle: O(n)

**Tail Pointer**
An optional extra. An additional helper pointer which always points to the last element in the list.
This makes adding an element to the rear O(1) as you can directly address the tail pointer, and find the ‘current last element’, and then point both the ‘current last element’ and the tail pointer itself to the ‘new last element’.
Tail pointers do not reduce the time complexity of *removing* elements, as we must traverse through the list to find the n-1th element.


## Doubly Linked List


![](https://static.javatpoint.com/ds/images/doubly-linked-list2.png)


Each node contains the key (actual data), the next AND prev pointers.


    class Doubly_Linked_List
    {
            node *front;          // points to first node of list
            node *end;           // points to first las of list
            
            public:
            Doubly_Linked_List()
            {
                    front = NULL;
                    end = NULL;
            }
            void add_front(int );
            void add_after(node* , int );
            void add_before(node* , int );
            void add_end(int );
            void delete_node(node*);
            void forward_traverse();
            void backward_traverse();
    };


    struct node
    {
            int data;             // Data
            node *prev;          // A reference to the previous node
            node *next;         // A reference to the next node
    };

Doubly linked lists allow for constant time to insert between nodes or remove a node.

**Note**: It still requires O(n) to find a node, but once you’ve found it, you can remove it and you have pointers forwards *and* backwards to link up the surrounding nodes. In a singly linked list you’d need to O(n) find the node, then O(n) delete it as you have no backwards traversal.


# Stacks & Queues
----------

The stack and the queue are implemented identically to Linked Lists. They are for specific purposes.

A stack follows LIFO (Last in, First out), and a queue follows FIFO (First in, first out). They are programmed in a way that restricts deleting nodes in the middle of the lists and only pushing into and reading out of specific sides.


## Stacks

Pushing onto a stack adds an element to the **beginning** (head) ****of the list.
Popping off a stack gets the element at the **beginning** (head) of the list.

## Queues

Enqueuing adds an element to the end of the list
Dequeuing gets the element from the beginning of the list.

