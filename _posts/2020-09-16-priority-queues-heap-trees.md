---
layout: article
title: Priority Queues & Heap Trees
show_edit_on_github: false
tags: DSA interview-prep

---

This post is part of a series on Data Structures and Algorithms (DSA). The series is a collection of notes that I read for interview prep as a refresher from originally learning the concepts in my undergrad. So while the concepts covered in these posts can be a good first-entry into DSA, some concepts are touched on in passing and the deep levels of detail (beyond that which is necessary as a job-hunt refresher) are largely ommitted.

The `DSA` tag can be used to find other blog posts on DSA concepts.

---

A priority queue is a generalisation of the standard queue data structure.
There is no front and back of the queue, instead we have a bag of elements with assigned priorities.

We extract elements from the queue in priority-order.

Priority Queues are used by:

- Dijkstra’s & Prim’s MST
- Heap Sort
- Huffman’s Algo

**Why we need a special data structure for Priority queues.**
If we wanted to use regular arrays for our priority queue, we can insert in O(1) but to find the max element, we need O(N).
If we wanted to use sorted arrays for our priority queue, we can extract the max in O(1) but to ***insert*** costs O(N): Why? We can find the location to insert in O(logn) with binary search but we must shift back the rest of the array which costs O(N).
Similarly, inserting into a sorted linked list costs O(N), extracting from an unsorted linked list costs O(N).

There is a data structure which allows us to implement a priority queue with log time operations:


# Binary Heap


A binary max-heap is a binary tree where the value of each node is at least the values of its children.

![Binary heap](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/1200px-Max-Heap.svg.png)


**Finding highest priority: O(1)**
Now to implement getMax() we only need to serve the root of the tree, in O(1) time.

**Inserting a new element: O(log(n))**

First, naively insert the element to an empty location.

![](https://paper-attachments.dropbox.com/s_9BC4A5FEE7EF6E63AE48FEADF3EE8E25939F91049D15ACA433ABF0B789142D86_1595856721235_delet.png)


Here 32 is inserted under 7, violating the heap property. Bubble ’32’ up the tree by swapping it with its parent until it naturally reaches the correct hierarchy. E.g - Swap 7 & 32, Swap 29 & 32.

Sifting is O(tree-height) which is O(log(n)) for a balanced, complete tree.


**Extract Max priority: O(log(n)) for balanced trees**

The procedure for deleting a node is similar to inserting a node in that it uses *bubbling.*  First we will delete a root node.

Removing a node will break the tree into two trees, so we need to fill the gap when we remove a node - we can easily fill the gap with a leaf, ideally the latter-most leaf (in a complete tree).

Suppose we wish to extract the top priority element in the queue, we want to get ’42’ and remove it from the data structure. We replace it with a leaf node.

![12 will be moved up to the root](https://paper-attachments.dropbox.com/s_9BC4A5FEE7EF6E63AE48FEADF3EE8E25939F91049D15ACA433ABF0B789142D86_1595859873733_image.png)


(Note the above is suboptimal as the tree is not complete. We would always swap the last leaf possible if we want to preserve completeness.)

When 12 is swapped up to become the root, it lies above 29 & 18 which violates the Heap on two fronts. We will bubble down 12 until it is below everything greater than itself.

![](https://paper-attachments.dropbox.com/s_9BC4A5FEE7EF6E63AE48FEADF3EE8E25939F91049D15ACA433ABF0B789142D86_1595859972352_image.png)


We bubble down the 29 route not the 18 route because 29 is greater than 18. We always select the largest child when such a conflict occurs. (If we swapped 12 with 18, we’d only need to swap 18 with 29, as 18 would sit on top of 29 which is incorrect!)


![The final heap](https://paper-attachments.dropbox.com/s_9BC4A5FEE7EF6E63AE48FEADF3EE8E25939F91049D15ACA433ABF0B789142D86_1595860071996_image.png)


**Delete a non-root node**

First, change the target node to be priority $$\infty$$, then bubble it up to the root. Now delete the root as per the Extract Max algorithm.



# Heaps as Arrays

Heaps should be complete binary trees.
This allows us to extract max by array[1] and extract the ‘final’ leaf by calling array[n]. It also guarantees balance & log time operations.

Remember: we index heaps starting from 1 because it lets our arithmetic/algorithms work really nicely, just by knowing the index, $$i$$, of one node:

![](https://paper-attachments.dropbox.com/s_9BC4A5FEE7EF6E63AE48FEADF3EE8E25939F91049D15ACA433ABF0B789142D86_1595860605435_image.png)


This lets us traverse a binary tree in an array without pointers between nodes, we just directly address array memory by calculating where the next node would lie.


## Ensuring Completeness

What operations change the *shape* of the tree? **Insert** & **ExtractMax**
Note that deleting a non-root node essentially invokes ExtractMax, so this also changes the shape but we can fix it via ExtractMax itself.

**Complete Insertion**

Make sure to insert a lead node in the leftmost position, i.e. - at the end of the array. Trivial

**Complete Extraction**

Make sure to swap the root node with the **last leaf,** i.e - the final array element. Also trivial.



## Building a new Heap from scratch

Rearranging an array of items into heap tree form can be done efficiently using ‘bubble down’. 

First note that, if we have the n items in an array a in positions 1, . . . , n, then all the items with an index greater than n/2 will be leaves, and not need bubbling down. Therefore, if we just bubble down all the non-leaf items a[n/2],..., a[1] by exchanging them with the larger of their children until they either are positioned at a leaf, or until their children are both smaller, we obtain a valid heap tree


![](https://paper-attachments.dropbox.com/s_9BC4A5FEE7EF6E63AE48FEADF3EE8E25939F91049D15ACA433ABF0B789142D86_1595862344128_image.png)


