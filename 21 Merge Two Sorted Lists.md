# 21. Merge Two Sorted Lists

[https://leetcode.com/problems/merge-two-sorted-lists/description/](https://leetcode.com/problems/merge-two-sorted-lists/description/)

## Code By Noobest Coder on the Block:

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        
        Node1=list1
        Node2=list2
				# copying the nodes for some reason instead of directly running through them

        if Node1.val>Node2.val:
            Node3 = Node1
        else:
            Node3 = Node2
				# why do it inside the loop when you can repeat the same shit outside

        Newhead = Node3
				# does this make sense? no. but i still thought it would somehow work magically
				# the problem this proposes is that if you equate a=b=2 and then change the value of b
					# do you think value of a would change too...?
            
        while Node1.next!=None and Node2.next!=None:
				# run till one of them becomes null
				# tip, instead of using x.a always try to do with x itself in the loop conditions
		        # ( see bottom line for hint for this )

						# assign whichever node is bigger and increment
            if Node1.val>Node2.val:
                Node3.next = Node1
                Node1 = Node1.next
            else:
                Node3.next=Node2
                Node2 = Node2.next
            Node3=Node3.next
        
				# the last of ones
        if Node1==None:
            Node3.next = Node2
        elif Node2==None:
            Node3.next = Node1
            
        return Newhead
				# returning the a=2 when you have made a thousand changes to b

				# so the answer is,
				# instead, you make a and b both point toward c and make all changes in c by starting with b
				# so when you reference the next of a, you have your c intact
```

## The Correct and Concise Way of Merging Two Linked List [self/net]

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        
        newnode = headnode = ListNode()
				# this is some voodoo shit but just accept it
				# newnode and headnode are instance of the same object
				# any change attached to newnode will be reflected in headnode aswell
				# headnode = newnode = ListNode() works too but the above one just looks more sensible, so i keep it
        
        while list1 and list2:
				# meaning while these two pointers both exist. if one dies, loop stops
            if list1.val<list2.val:
						# very intutive
                newnode.next = list1
								# attaching to next instead of newnode itself, as we need to reference newnode.next later
                list1=list1.next
								# increment list1 pointer
            else:
                newnode.next = list2
                list2=list2.next
            newnode = newnode.next
						# incrementing the newnode pointer

        newnode.next = list1 if list1 else list2
				# attaching the remaining list to next
				# if both lists are dead, None value will be assigned to the next
        return headnode.next
				# return next of headnode (voodoo shit)
```

## What I Learned:

- There’s always a more concise way to write a code but you wont understand it till you haven’t understood the long of it
- Sometimes you just have to accept what works, and remember it if you cant understand it