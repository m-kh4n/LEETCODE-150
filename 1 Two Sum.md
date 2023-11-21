# 1. Two Sum

[https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

## Classic Nested Loop:

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
						# initializing j from i+1 so that it doesnt repeat
                if nums[i]+nums[j]==target:
                    return [i,j]
```

## The O(n) Solution:

```python
class Solution(object):
    def twoSum(self, nums, target):
        hashmap = {}
				# making a hashmap to store elements and their indices as we skim through the array for a matc
        for i in range(len(nums)):
				# enumerating through the array
            if (target-nums[i]) in hashmap:
						# if the element adding up to the target is in the hashmap
							# thats our result for the array
                return [hashmap[target-nums[i]], i ]
            hashmap[nums[i]]=i
						# meaning that if match is not found, 
							# then we are simply appending the new key value pair to the hashmap
```

## What I Learned:

- Dynamic solutions are always the most innovative