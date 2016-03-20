---
layout: post
title: Binary Tree
---

Let's talk about data structures, in particular, binary search trees. So let's start with the basics: it is a tree starting at a single point and branching downwards. But, unlike other trees, this tree can only have two children so let's talk about why this is important.

![alt text](https://upload.wikimedia.org/wikipedia/commons/d/da/Binary_search_tree.svg "Binary Search Tree")

In our example above, 8 is the head of the tree (or the 'root'), and all child nodes will be a descendant of this original root node. As we continue down the tree, we can see that the root has two child nodes, 3 and 10. Now this is important to look at carefully--any child that is smaller than its parent is going to branch off to the left, and any child that is larger than its parent will branch off to the right. This is true no matter how far you get into a tree. 

What does this mean and why is it important? Well, this is extremely important when it comes to searches. A search looking for a particular value will never look at more than half our data and each step down the tree will cut out another half. 

Let's look at our tree above as an example. Say we are looking for the value 7, we start at the root ask the root if it's 7. It's not so then we check if the value we are looking for is larger or smaller than the root. 7 is smaller than 8 so we know we must now head down the left side of the tree, this cuts out the entire right side of the tree which we will never have to look at. The same process is repeated again at the 3 node and so on until we reach our goal of 7. Each step eliminates half the data as an option until it hits the correct node. 

