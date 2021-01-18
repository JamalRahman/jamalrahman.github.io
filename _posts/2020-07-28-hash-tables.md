---
layout: article
title: Hash Tables
show_edit_on_github: false
tags: DSA interview-prep

---

This post is part of a series on Data Structures and Algorithms (DSA). The series is a collection of notes that I read for interview prep as a refresher from originally learning the concepts in my undergrad. So while the concepts covered in these posts can be a good first-entry into DSA, some concepts are touched on in passing and the deep levels of detail (beyond that which is necessary as a job-hunt refresher) are largely ommitted.

The `DSA` tag can be used to find other blog posts on DSA concepts.

---

Hash tables allow data to be stored in a more memory intensive, but far quicker, solution than arrays, lists, and trees.

Given a key, could we jump straight to the data for that key without having to search for it or traverse a data structure to reach it?

Data is stored in an array format, whereby each element naturally has its own index. Hash Tables allow us to instantly lookup the element of data at array[index] corresponding to a key, without having to know or find what the index it is first.

**The data, d, is passed through a** ***hash function*** **which spits out an integer. This integer is used as the index corresponding to data, d.**


![Hash Function](https://www.tutorialspoint.com/data_structures_algorithms/images/hash_function.jpg)


To find the data, we simply now probe memory at `array[h(key)]`

Note: We could just use the key as the index, without hashing, but suppose we use a 9-digit ID number for the keys, we’d ostensibly need a 10^9 long array even if most of those permutations are unused. Hashing lets us dramatically cut down the scope of the numbers we use.


----------


## Hash Collision Resolution

Hash tables break down if two keys hash to the same value.

**Separate Chaining**
The most commonly used resolution method. In separate chaining, each element of the hash table is a linked list rather than a single element.


![Separate Chaining](https://he-s3.s3.amazonaws.com/media/uploads/0e2c706.png)


Here, the linked list stores key/value items for any keys which hashed into it; you can now search the linked list for the item which corresponds to the key you’re looking up.

**Linear Probing / Open addressing**

This stores the ‘extra’ keys which match the hash in empty array cells.

![](https://he-s3.s3.amazonaws.com/media/uploads/9c56c0d.jpg)


In this example, `Code Monk` hashes into 2. `Hashing` also hashes into 2, but overflows into 3, the next blank space.

On lookup of `Hashing`, the table will hash it and lookup array[2]. Finding ‘Code Monk’, the table will then look up array[3], and then array[4].. etc, until it either a) finds the key (‘Hashing’) or finds a blank space. A blank space implies that ‘Hashing’ was not present in the table as it was never overflowed into the next blank space.


