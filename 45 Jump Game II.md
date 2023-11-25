# 45. Jump Game II

[https://leetcode.com/problems/jump-game-ii](https://leetcode.com/problems/jump-game-ii)

## Failed Greedy Approach [Self] :

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        
        if len(nums)==1:
            return 0

        goal = len(nums)-1
				# goal initialized as the last index in the array
        windows = 1
				# windows denote how many sections can we divide a array,
					# such that each is unreachable by next
					# eg. in [2,3,1,1,4] will be divided as [2,|3,1,1,4]
					# we have two windows in the above example, meaning we only require two steps

        for i in range(goal)[::-1]:
				# let i go form last second index to the zero index
            if i+nums[i]<goal:
						# as soon as the goal becomes inaccessible means we are at a new window
						# increment window count and update goal
                windows += 1
                goal = i

        return windows
				# return number of exclusive windows

# why does the code not work :
	# lets take [2,3,1,1,4]
	# if we simply take the condition i+nums[i]<goal
	# the loop will break of at index 2 with value 1 as 3<4
	# but we already know that that is wrong, as the index 1 is again able  to reach 4
		# 1+3 not less than 4. 
	# hence breaking the loop at the first instance of mismatch will result in inaccurate results
```

## Working Greedy [Net] (TWO LOOPS) :

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        
        goal = len(nums) - 1
        steps = 0
        while goal != 0:
				# if we just need to reach the 0th index, we are already there in the start by default
            for i in range(goal):
						# each time the goal is updated, we start from index 0 till the goal index to search for a match
                if i + nums[i] >= goal:
                    steps += 1
                    goal = i
										# soon as we encounter an element able to jump to goal, we make that the new goal
										# increment the step, and move back again
                    break
        return steps
```

## Sliding Window (MOST SUITABLE) [Self/Net] :

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        
        steps = 0
        l = r = 0
        # we are given we always start at index 0, hence we keep the left and right arm both at index 0
				# 'how far can we go with the element at the index 0'

        while r<len(nums)-1:
				# right arm will go till the end of the array and touch it
            farthest = 0
						# this element defines which is the max index the elements between l and r+1 are able to attain
						# this variable essentially will give us value for our next right arm
						# then we will again calculate the farthest again, hence each loop we reset it to 0
            for i in range(l, r+1):
                farthest = max(farthest, i+nums[i])
								# keep updating the farthest regardless
            l = r+1
						# element next to the previous farthest becomes the left arm of the window
            r = farthest
						# the farthest reachable element becomes the right arm
            steps += 1
						# as the farthest takes jump again and again,
							# step will be incremented thill the right arm (the farthest) exceeds the last second index
    
        return steps

# link to sol: https://www.youtube.com/watch?v=dJ7sWiOoK7g
```

## What I Learned :

- Running the test cases on paper helps figure out the exact edge case more effectively