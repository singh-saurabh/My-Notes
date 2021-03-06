# Heap & Heap Sort

[Resource Link](https://www.youtube.com/watch?v=HqPJF2L5h9U)

## How to represent a binary tree in an array?

Array must preserve the value of all nodes and the relations ships. We can just fill the array in depth first search manner (level by level) while leaving empty spaces for null nodes.

Consequences:
1. If the binary tree is **complete** -> Array will have no blank spaces. (A binary tree is **complete** if it is a **full** binary tree till max_height-1 and nodes are filled from left to right on the last level.).
2. Let max-height = h -> Length of array required is (2^h -1).
3. Relationship: Let a node x at position i of array (*indexing must from 1*)
	- Left Child: *(2\*i)*
	- Right Child: *(2\* + 1)*
	- Parent: *floor(i/2)*

NOTE: *Height* of a **complete binary tree** is *log(n)* [base 2 (of course)] [n=number of nodes].

## Max and Min Heap

Max Heap: A complete binary tree with every node having value greater than (or equal to) all its descendents.

Same for min heap (less than or equal to).

### Insertion in Max Heap (Upheap)

Steps:
1. Insert element at the first available position in array (that is first empty node going left to right in heap's last level).
2. Upheap. Lets say `curr` points to the last element (that is the element inserted), follow the steps below in a loop till curr become the root of heap (`while(curr>0)`) or loop breaks:
	- If the element at `curr` greater than its `curr_root = floor(curr/2)`)
		- Swap value at curr_root and curr.
		- Update `curr = curr_root`
	- Else `break;`

### Deletion in Max Heap (Downheap)

NOTE: Deletion means that a element is taken out. You must always take out the `max element` only from a `max heap` (cause that is the purpose of the heap, priority queue). The following algorithm taken out the root element only.

Steps:
1. Delete the root, i.e. consider arr[0] as empty. (you can store it for returning)
2. Heap_Size -= 1
3. Let `curr = 0` (i.e. root of heap). Set value at curr = Value at last node (arr[Heap_size-1]).  (considering indexing from 0)
4. Downheap:
	- Loop the following steps `while(curr<Heap_Size)` or the loop breaks:
		- If value at curr is max of itself at its children -> `break;`
		- Else:
			- Find max of chilren.
			- Swap values max of child with curr.
			- Make curr point at the swapped child.

### Heapify

Basically this converts a complete binary tree into a min/max heap. This can be useful to convert a given array into a heap without inserting it one by one using upheap. (just a bit simple implementation of creating a heap (or element insertions, you can say that) using Downheap).

Algorithm: Keep reading nodes from back of array (that is bottom to top for a heap) and Downheap. See [link](https://youtu.be/HqPJF2L5h9U?t=2623).

## Heap Sort

Given an array arr to sort. Convert it into a heap.
- Method1: Read elemets and insert in heap using insert function as given above.
- Method2: Pass the array to heapify function.

Now, we have a heap (say max_heap).

Now, lets say name of array representing heap is `heap_arr`. Just keep deleting elements one by one till the `heap_size` comes down to 1. At each deletion, save the deleted element at `heap_size` position of array. In this manner you will simply fill up the array `heap_arr` with elements max to min from back to front, i.e. array got sorted in increasing order.