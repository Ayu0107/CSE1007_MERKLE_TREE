# MERKLE TREE

The Merkle tree, also known as the hash tree, is a data structure that is used to verify and synchronise data.
It is also known as Hash tree because it only stores the hashes in its nodes instead of data.
It's a data structure in which each non-leaf node is a hash of its children. All of the leaf nodes are the same depth and are positioned as far to the left as feasible.
It employs hash functions to preserve data integrity. 
Merkle trees are in a binary tree, so it requires an even number of leaf nodes. If there is an odd number of transactions, the last hash will be duplicated once to create an even number of leaf nodes.

![image](https://user-images.githubusercontent.com/62741870/165602882-6797ddcb-d58e-4667-92d6-ef4c4410a59d.png)



## ARCHITECTURE

Creating a Merkel Tree from a given list of alphabets.

The bottom most layer of the tree would contain all the letters as the leaf nodes.

![image](https://user-images.githubusercontent.com/62741870/165681995-482f9d4f-5937-436b-9d2a-b8b520f55fc8.png)

The layer above contains its hash values.

![image](https://user-images.githubusercontent.com/62741870/165682150-ac3d18a9-a051-474f-b42a-6f14c3557458.png)

The nodes in the layer after the second layer are contains the hash value of the child nodes. Generally we take two nodes from the second layer and combine them to form another node. We can take more than two nodes as well but binary merkel trees is the simplest of them all and increasing the degree of nodes only increase the computation and algorithms complexity.

If we have even number of nodes, we take 2 consecutive nodes and form the parent layer. But if we have odd number of nodes, we take two consecutive nodes until one is left to form the parent layer, and then we repeat the remaining node by copying the hash to the parent layer.

![image](https://user-images.githubusercontent.com/62741870/165682250-24d436d7-4b47-4aca-bbbe-28cdbc10cce4.png)

Similarly the fourth layer is formed using the values of the third layer.

![image](https://user-images.githubusercontent.com/62741870/165682333-1c1adb29-964c-42f4-90e3-921d39425bac.png)

The final layer or the root of the Merkel Tree is formed by hash value of the last two nodes remaining in top most layer. In any case, odd or even leaf nodes, we will always have two nodes in the top most layer.

![image](https://user-images.githubusercontent.com/62741870/165682390-9df00fcb-84ed-4a0b-be58-3e59aa862426.png)

## VERIFICATION

In case of a hash chain we would need the entire list of data to verify that C’ is correct. In Merkel Tree we only need the hashes. Following diagram illustrates how we can verify, C’ without other data objects available with us.

![image](https://user-images.githubusercontent.com/62741870/165683431-dcea2a23-d73c-42cf-b57d-a14f4807c7ef.png)

1. Find the position of the C’ in the list. Probably by searching by id.
2. Calculate the the hash of C’
3. Calculate the value of the parent node by hashing the current node with its neighbor ( next if position is odd and previous if position in even) and set the parent as the current node.
4. Repeat step 3 until we find the root
5. Compare the root with the previous root, if they match then C’

Compare the new root with the existing root. If the new root matches then the C’ is essentially C and not tampered.

## PROTOCOL

In various distributed and peer-to-peer systems, data verification is very important. This is because the same data exists in multiple locations. So, if a piece of data is changed in one location, it's important that data is changed everywhere. Data verification is used to make sure data is the same everywhere.

However, it is time-consuming and computationally expensive to check the entirety of each file whenever a system wants to verify data. So, this is why Merkle trees are used. Basically, we want to limit the amount of data being sent over a network (like the Internet) as much as possible. So, instead of sending an entire file over the network, we just send a hash of the file to see if it matches. The protocol goes like this:

Computer A sends a hash of the file to computer B.
Computer B checks that hash against the root of the Merkle tree.
If there is no difference, we're done! Otherwise, go to step 4.
If there is a difference in a single hash, computer B will request the roots of the two subtrees of that hash.
Computer A creates the necessary hashes and sends them back to computer B.
Repeat steps 4 and 5 until you've found the data blocks(s) that are inconsistent. It's possible to find more than one data block that is wrong because there might be more than one error in the data.

Here in this code, we are implementing binary merkle tree.

## STRUCTURE OF BINARY MERKLE TREE

It contains four variables:

It contains a key variable.  
It contains value variable.  
It contains two links.  

Find operation in Merkle tree
This function is used to check whether the given key is present in the merkle tree or not. If it is present then it will return that node else it will return null. This function is used to retrieve data from Git. When we commit a change to a repository in git. Git computes SHA-1 ( SHA-1 produces a 160-bit hash value from an arbitrary length string) over the contents of that directory tree and stores them with metadata. It is stored in .git/objects and gives you back the unique key that now refers to that data object.

## ALGORITHM

## Algorithm of find function in Merkle tree

Step 1: We will take tree and key as parameters.  
Step 2: If the tree is null then we will return null.  
Step 3: If the tree->key is equal to the key we will return the tree.  
Step 4: If the key is smaller than tree->key then we will return find(tree->left, key)  
Step 5: else return find(tree->right, key)  

## Add operation in Merkle tree

This function is used to add a node into the merkle tree. This function is used to insert source code into a git repository. When we commit a change to a repository. Git computes SHA-1 over the contents of that directory tree and stores them with metadata. The metadata includes information such as pointer to parent commit and a commit message as a commit object.

## Algorithm to add a node in Merkle tree.

Step 1: We will take key and value as parameters.  
Step 2: Take the hash(key) and store it in a variable called index.  
Step 3: store (struct node*) arr[index].head in a pointer called tree of datatype node.  
Step 4: create a new node with its key as key and value as value and both links as null.  
Step 5: If the tree is null then assign the new node to the head and increment the size by 1.
Step 6: If the tree is not null then we will check if the key is already present in the tree using the find function.  
Step 7: If the key is already present in the tree then we will update the value.  
Step 8: If it is not present in the tree then we will use the insert function to insert the element. 

## Algorithm of insert function

Step 1: It will take tree and item pointers of node data type as parameters.  
Step 2: If item->key is smaller than tree->key and tree->left is null then assign the item to tree->left.  
Step 3: If item->key is smaller than tree->key and tree->left is not null then call insert function with tree->left and item as parameters.  
Step 4: If item->key is greater than tree->key and tree->right is null then assign the item to tree->right.  
Step 5: If item->key is greater than tree->key and tree->right is not null then call insert function with tree->right and item as parameters.  

## Delete a node from merkle tree

This function is used to delete a node from Merkle tree. If the key given is present in the merkle tree then it will delete the node from the tree. Git remembers all the files you have staged and stores them in a tree structure inside the commit. The nodes of this tree represent your files and directories. This function is used to delete these nodes.

## Algorithm to delete a node in Merkle tree

Step 1: We will take a key as a parameter.   
Step 2: Take the hash(key) and store it in a variable called index.    
Step 3: store (struct node*) arr[index].head in a pointer called tree of datatype node.  
Step 4: If the tree is null then the key is not present.   
Step 5: If the tree is not null then we will check if the key is already present in the tree using the find function.  
Step 6: If the find function returns null then the key is not present in the tree.  
Step 7: If it is not null then we will use the remove function to delete the element.  

## Algorithm of remove function

Step 1: It will take tree and key as parameters.  
Step 2: If the tree is null then return null.    
Step 3: If the key is smaller than the tree->key then tree->left is equal to remove(tree->left, key) and return tree.  
Step 4: If the key is greater than the tree->key then tree->right is equal to remove(tree->right, key) and return tree.  
Step 5: else if the tree->left is equal to null and the tree->right is equal to null then decrement the size and return tree->left.  
Step 6: else if the tree->left is not equal to null and the tree->right is equal to null then decrement the size and return tree->left.  
Step 7: else if tree->left is equal to null and tree->right is not equal to null then decrement the size and return tree->right.  
Step 8: else assign tree->left to a pointer called left of data type node.  
Step 9: While left->right is not equal to null, left is equal to left->right.  
Step 10: tree->key is equal to left->key.   
Step 11: tree->value is equal to left->value.  
Step 12: tree->left is equal to remove(tree->left, tree->key).  
Step 13: Return tree.

## CODE OUTPUT

![image](https://user-images.githubusercontent.com/62741870/165687132-65062974-71e6-4df9-849a-dac8fa4ce21a.png)

Now, if we change the s in Doctor strange to capital letter. Like Doctor Strange like - 

![image](https://user-images.githubusercontent.com/62741870/165687188-7b59ad25-d871-46d5-ab47-4f6a957763c3.png)

We will get complete different output for that data block. So, it means, its parent hash changes and all its ancestors hash value changes in the tree like below. 

![image](https://user-images.githubusercontent.com/62741870/165687284-cfb4c5a0-c40e-48da-885b-6d3d0528ada4.png)



