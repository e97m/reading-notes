# Stacks

A stack is a data structure that consists of Nodes. Each Node references the next Node in the stack, but does not reference its previous.

## Common terminology:

- `push`: put into the stack.
- `pop`: removed from the stack.
- `peek`: view the value of the top Node in the stack.
- **FILO**: First In Last Out, the first item added in the stack will be the last item popped out of the stack.
- **LIFO**: Last In First Out, the last item added to the stack will be the first item popped out of the stack.

<br>

## Edit the stack:

- `push` node to a stack O(1): When adding a Node, you push it into the stack by assigning it as the new top, with its next property equal to the original top.
    1. Creat the node that you want to add.
    2. Assign the `next` property of the new node to reference the same node that top is referencing in the previous node.
    3. Re-assign the reference `top` to the newly added node.

<br>

- `pop` node to a stack O(1): Popping a node off a stack is the action of removing a node from the top. When conducting a `pop`, the top node will be re-assigned to the node that lives below and the top node is returned to the user. Typically, you would check `isEmpty` before conducting a `pop`. This will ensure that an exception is not raised. Alternately, you can wrap the call in a `try/catch` block.
    1. Create a reference named `temp` that points to the same node that `top` points to.
    2. Re-assign `top` to the value that the next property is referencing.
    3. Remove that node safely without it affecting the rest of the stack. Before that, you may want to make sure that you clear out the `next` property in your `current temp` reference. 

<br>

- `Peek` (inspecting the top Node) O(1): Typically, you would check `isEmpty` before conducting a peek. This will ensure that an exception is not raised. Alternately, you can wrap the call in a `try/catch` block. We do not re-assign the `next` property when we `peek` because we want to keep the reference to the next Node in the stack. This will allow the `top` to stay the top until we decide to `pop`.

<br>

<br>

# Queues

## Common terminology:

- `Enqueue`: Nodes or items that are added to the queue.
- `Dequeue`: Nodes or items that are removed from the queue. If called when the queue is empty an exception will be raised.
- `Front`: This is the front/first Node of the queue.
- `Rear`: This is the rear/last Node of the queue.
- `Peek`: When you peek you will view the value of the front Node in the queue. If called when the queue is empty an exception will be raised.

## Edit the Queue:

- `Enqueue` O(1): 
    1. Change the `next` property of the node tou want to add before to point to the node we are adding.
    2. Re-assign the rear reference to point to the new node.

- `Dequeue` O(1): Typically, you would check `isEmpty` before conducting a `dequeue`. This will ensure that an exception is not raised. Alternately, you can wrap the call in a `try/catch` block.
    1. Create a temporary reference type named `temp` and have it point to the same node that front is pointing too.
    2. Re-assign front to the next value that the Node front is referencing.
    3. Return the value of the temp Node that was just removed.

- `Peek` O(1): When conducting a peek, you will only be inspecting the front Node of the queue. Typically, you want to check isEmpty before conducting a peek. This will ensure that an exception is not raised. Alternately, you can wrap the call in a try/catch block. We do not re-assign the next property when we peek because we want to keep the reference to the next Node in the queue. This will allow the front to stay in the front until we decide to dequeue

<br>

## [Reference](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/stacks_and_queues.html)