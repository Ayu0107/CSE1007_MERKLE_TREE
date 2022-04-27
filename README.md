#Ayushi Aggarwal (19BBS0116)

The Merkle tree, also known as the hash tree, is a data structure that is used to verify and synchronise data.
It is also known as Hash tree because it only stores the hashes in its nodes instead of data.
It's a data structure in which each non-leaf node is a hash of its children. All of the leaf nodes are the same depth and are positioned as far to the left as feasible.
It employs hash functions to preserve data integrity. 
Merkle trees are in a binary tree, so it requires an even number of leaf nodes. If there is an odd number of transactions, the last hash will be duplicated once to create an even number of leaf nodes.

![image](https://user-images.githubusercontent.com/62741870/165602882-6797ddcb-d58e-4667-92d6-ef4c4410a59d.png)



Here in this code, we are implementing binary merkle tree.

Algorithm - 

Firstly, we define the node. Like any regular tree, even this has a data field to store the hash and left and right pointers to point to left child and right child of the binary tree.



