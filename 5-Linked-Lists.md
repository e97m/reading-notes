# Linked Lists

A Linked List is a sequence of Nodes that are connected/linked to each other. The most defining feature of a Linked List is that each Node references the next Node in the link. There are two types of Linked List - Singly and Doubly. We will be implementing a Singly Linked List in this implementation.

The best way to approach a traversal is through the use of a `while()` loop. This allows us to continually check that the `Next` node in the list is not `null`. If we accidentally end up trying to traverse on a node that is `null`, a `NullReferenceException` gets thrown and our program will crash/end. The `Current` variable will tell us where exactly in the linked list we are and will allow us to move/traverse forward until we hit the end.

One characteristic of linked lists is that they are ***linear data structures***, which means that there is a sequence and an order to how they are constructed and traversed. Note that dictionaries,trees and graphs are ***non-linear data structures*** which means traversing them done in different ways.

## BigO

The Big O of time for Includes would be O(n). This is because, at its worse case, the node we are looking for will be the very last node in the linked list. n represents the number of nodes in the linked list. The Big O of space for Includes would be O(1). This is because there is no additional space being used than what is already given to us with the linked list input.

The Big O of time for `insert` would be O(1), and Space efficiency would stay at an O(1). The Big O of time for `append` would be O(n), and Space efficiency would stay at an O(1). The Big O of time for `add_bedore` would be O(1), and Space efficiency would stay at an O(1).

## Array vss Linked List

Array faster in finding elements (becouse of indexes). Linked lists better in terms of customizing the size of it (expand and shrink), also its elements shouldnt be beside eachothers in the memory.

The fundamental difference between arrays and linked lists is that arrays are static data structures, while linked lists are dynamic data structures. A static data structure needs all of its resources to be allocated when the structure is created; this means that even if the structure was to grow or shrink in size and elements were to be added or removed, it still always needs a given size and amount of memory. If more elements needed to be added to a static data structure and it didn’t have enough memory, you’d need to copy the data of that array, for example, and recreate it with more memory, so that you could add elements to it. On the other hand, a dynamic data structure can shrink and grow in memory. It doesn’t need a set amount of memory to be allocated in order to exist, and its size and shape can change, and the amount of memory it needs can change as well.

## Linked List Types:

1. Singly: start at the `head` node, and single track traverse from the root until the last node using `next` reference, which will end at an empty `null` value.
2. Doubly: start at the `head` node, and double tracks: traverse from the root until the last node using `next` reference, and backwards using `prev` reference. It is also ends at an empty `null` value.
3. Circular: is a little odd in that it doesn’t end with a node pointing to a `null` value. Instead, it has a node that acts as the tail of the list (rather than the conventional `head` node), and the node after the tail node is the beginning of the list. This organization structure makes it really easy to add something to the end of the list, because you can begin traversing it at the tail node, as the first element and last element point to one another. Circular linked lists can start to get really crazy because we can turn both a singly linked list and a doubly linked list into a circular linked list!



<br>

Read: [Linked Lists](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-05/resources/singly_linked_list.html)

Read: [What’s a Linked List, Anyway pt1](https://medium.com/basecs/whats-a-linked-list-anyway-part-1-d8b7e6508b9d)

Read: [What’s a Linked List, Anyway pt2](https://medium.com/basecs/whats-a-linked-list-anyway-part-2-131d96f71996)