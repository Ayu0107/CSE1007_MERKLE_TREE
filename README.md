#Ayushi Aggarwal (19BBS0116)

The Merkle tree, also known as the hash tree, is a data structure that is used to verify and synchronise data.
It is also known as Hash tree because it only stores the hashes in its nodes instead of data.
It's a data structure in which each non-leaf node is a hash of its children. All of the leaf nodes are the same depth and are positioned as far to the left as feasible.
It employs hash functions to preserve data integrity.

Here in this code, we are implementing binary merkle tree.

Algorithm - 

Firstly, we define the node. Like any regular tree, even this has a data field to store the hash and left and right pointers to point to left child and right child of the binary tree.

