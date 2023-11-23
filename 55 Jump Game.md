# 55. Jump Game

[https://leetcode.com/problems/jump-game/](https://leetcode.com/problems/jump-game/submissions/?envType=study-plan-v2&envId=top-interview-150)

## Balance Integer [Self] :

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:

        if len(nums)==1:
				# For the edgecase that we already are at the last element basically before even starting the loop
            return True

        i= 0
				# starting the i value from the index itself
        bal = nums[i]
				# our balance is whatever the first element in arrray is
				# if the first element is 0, we cant go anywhere and hence loop doesnt even start
        
        while bal>0 and i<len(nums) :
				# while we still have any amount of balance and while our index stays inbound
            
            if i+bal>=len(nums):
                return True
								# if we take 'bal' number of steps from this index and reach or exceed the final index
									# means we have enough balance to jump till the end, return true
            else:
                if nums[i]>=bal:
                    bal = nums[i]
										# if we havent yet exceeded and but our current element is greater than our balance
											# we update our balance value
                else:
                    bal = bal - 1
										# if the current element is less than our balance value, it really doesnt help,
											# hence we keep our balance intact
            i = i + 1
						# increment the index while the conditions of having balance stays true
        
        return False
				# if loop is completed means either we have lost all our balance and cant go further in the array
					# return failur
```

## Balance Integer OPTIMIZED [Net] :

```python

class Solution:
    def canJump(self, nums: List[int]) -> bool:

        bal = nums[0]
				# initialize balance as previous

        for i in range(1, len(nums)):
				# we iterate through indices in the array, from 2nd element onwards
					# if 1st element was zero and there was some element after it, it will be caught
					# if 1st element was zero or anything and no element after it, loop will not be touched, true returned
            if bal==0:
                return False
								# as soon as balance reaches zero, we return false
            bal = max(nums[i], bal-1)
						# update balance to either the current element value or the new balance, whichever is greater
							# each iteration we spend 1 unit of balance hence its updated to bal-1 if num[i] is not bigger
        
        return True
				# if loop exited without balance reaching 0 and having completed all elements, return true
```

## Greedy Approach [Net] :

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:

        goal = len(nums) - 1
				# set the goal to the last element
				# goal will be updated to value to the left if the leftward value is able to reach the goal
        i = len(nums) - 2
				# initialize the leftside value

        while i>= 0:
				# while the left side value remains equal or greater than i
            if goal <= i + nums[i]:
						# if leftward value, added its index, is able to reach the goal index, update goal
                goal = i    
								
	          i = i - 1
						# iterate backwards on indices
            
        return goal==0
				# if goal value is not zero, means that we weren't able to reach the first index value by goal updation
```

## Greedy OPTIMIZED [Net/Self] :

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        goal = len(nums) - 1
				# goal index is the last index of the array
				
        for i in range(goal)[::-1]:
				# we are iterating between 0 and len(nums)-1, but backwards (with help of [::-1])
				# 'the leftward index' goes from the last index to the 0th index now 
            if goal <= i + nums[i]:
						# if leftward value, added its index, is able to reach the goal index, update goal
                goal = i    
        return goal==0
				# if goal value is not zero, means that we weren't able to reach the first index value by goal updation
```

## What I Learned :

- Its good to take a jab on a problem you think you probably cant solve
- Sometimes you just need to add one line of extra code to avoid one testcase instead of trying to rectify the whole mostly working algorithm, when you are writing code all by yourself