---
layout: article
title: Trees, Binary Trees, and Binary Search
show_edit_on_github: false
tags: DSA interview-prep
cover: https://paper-attachments.dropbox.com/s_15ED02664217C73ABAFFC9BD2192FED4B19AC4EE33613FC4B13C956AC770B84D_1595781841045_image.png

---

This post is part of a series on Data Structures and Algorithms (DSA). The series is a collection of notes that I read for interview prep as a refresher from originally learning the concepts in my undergrad. So while the concepts covered in these posts can be a good first-entry into DSA, some concepts are touched on in passing and the deep levels of detail (beyond that which is necessary as a job-hunt refresher) are largely ommitted.

The `DSA` tag can be used to find other blog posts on DSA concepts.

---

You know them, you love them.

A graph connects nodes. Nodes are labelled with data, and contain references to other nodes.
A tree is a recursive data type.



![](https://www.researchgate.net/profile/Nicholas_Zerbel/publication/329029668/figure/fig1/AS:694428989661184@1542576181506/Example-of-a-search-tree-data-structure-with-key-structural-components-labelled_W640.jpg)


The maximal depth of a tree is its ***height***.


# Binary Tree

A binary tree consists of nodes which have at most two children.


## Complete Trees as Arrays

A binary tree is complete if every level, except possibly the last, is completely filled, and all the leaves on the last level are placed as far to the left as possible.

By being complete, not only can we guarantee *balance* and therefore minimum height of floor(log2(n)), but we can actually store these trees straightforwardly as arrays, because the nodes of the tree are complete without gaps, they act contiguously.


![A complete binary tree represented as an array](https://paper-attachments.dropbox.com/s_9B2ACF6BAE0B1357CF15B6234DDEF9E905C7083167AC0F29B2E2441E67837F43_1595856139659_image.png)


Notice that this time we have chosen to start the array with index 1 rather than 0. This has several computational advantages. The nodes on level i then have indices $$$$*2i , · · · , 2i+1 −1.* The level of a node with index *i* is *floor(log2(i))*. The children of a node with index i, if they exist, have indices 2i and 2i + 1. The parent of a child with index i has index i/2 (using integer division).

We can take those mathematical concepts and easily pass them into algorithms to get children/parents/levels just by knowing the index *i*.

**Note**: This array-storage is not feasible for most Binary trees, as you’ll break the tree’s completeness easily. These are best used for Binary Heaps.

---

# Binary Search Trees
A Binary Search Tree is a Binary tree where the left node key is smaller than the parent key, and right child node key is larger than the parent key.




![](https://miro.medium.com/max/1194/1*ziYvZzrttFYMXkkV9u66jw.png)


BST excel at local search. Search in a list/array is O(n). A sorted **array** can search in log time thanks to Binary Search.
Unfortunately, updating a sorted array is hard. Insertion & removal of new cells is an O(n) operation due to propagating changes forwards/backwards.

With a linked list, we can insert/remove in O(1) if we have a node already referenced, but we cannot search in log time even if the linked list is sorted, because unlike an array, we have no guaranteed hard coded notion of where the middle of the list lies. There is no ‘middle’ pointer, and no ‘quarters’ pointers. etc. etc.


## Basic Operations

**Find(n)**
Find a key in the data structure.
Compare n with the root key, and then search the left or right subtrees based on whether n is greater or smaller than the root.
If the key does not exist in the tree, the algorithm will navigate to the location it *would* be, and either search left or right child, and find null.

**Next(n)**
Find the next highest element in the data structure.
In a sorted array this is trivial, look at the next one.

In a binary tree, we have two cases:

Case 1: n has a right-child. It is obvious that the next greatest element will be rightwards of n, so we will depth-first search the left route of N’s child to find the deepest left-only child.


![](https://paper-attachments.dropbox.com/s_15ED02664217C73ABAFFC9BD2192FED4B19AC4EE33613FC4B13C956AC770B84D_1595781523677_image.png)


Case 2: n has no right child. n might be the greatest node on its SIDE of the tree, so we’d have to traverse up the tree and start delving down the other side of the tree.
Traverse up to the parents until we hit a node for which nodekey > n:


![](https://paper-attachments.dropbox.com/s_15ED02664217C73ABAFFC9BD2192FED4B19AC4EE33613FC4B13C956AC770B84D_1595781841045_image.png)



## Insertion

We follow the same logic for find(n). Find(n) traverses the tree by comparing n with the keys, and navigates to the place where it would find the new key.
We insert the key at the place where find(n) looks for it but throws null.



## Node Deletion

Node Deletion is more nuanced than insertion.

If we were to naively create a fresh BST with the target node absent, then we would have to insert n nodes to a fresh tree. Recall that inserting one node costs O(log(n)), thus inserting n nodes costs O(nlog(n)). This is worse than just deleting from a sorted array. We can do better.

 

![](https://paper-attachments.dropbox.com/s_15ED02664217C73ABAFFC9BD2192FED4B19AC4EE33613FC4B13C956AC770B84D_1595805169797_image.png)


There are broadly 3 cases:

1. Delete a leaf: simply delete it
2. Delete a node with only one subtree: Simply replace the deleted node with its child.
3. Delete a node which has two subtrees.

To delete a node which has two subtrees, we will replace it with the next highest key in the right-subtree. X in the diagram is the next-highest key in the delete-node’s right subtree.
We then replace X with the child of X, in this case Y.


![](https://paper-attachments.dropbox.com/s_15ED02664217C73ABAFFC9BD2192FED4B19AC4EE33613FC4B13C956AC770B84D_1595805360317_image.png)



## Time Complexity of Insertion and Search

Item insertion and search in a BST will take `treeheight + 1` operations, this is because by definition we traverse down the full height of the tree to either find/insert or reject the operation. 

So what is the height of a BST?

Well, it can be a long chain. Then height would be n-1 (we measure height from 0 indexing, hence the -1). This is a poorly balanced tree.

A balanced tree can have a minimum height of log(n)
This is also the average height: log(n)

**Thus insertion and search into a** ***balanced*** **tree has** **O(log(n))** **operations.**

This search complexity is equal to that of binary search over a sorted array, except the insertion of a new node in a BST also requires O(log(n)) whereas the array insertion needs O(n) steps.


![Left: A poorly balanced tree.      Right: A balanced tree](https://media.geeksforgeeks.org/wp-content/uploads/Node_height.jpg)



