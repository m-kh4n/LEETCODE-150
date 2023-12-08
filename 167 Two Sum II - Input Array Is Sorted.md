# 167. Two Sum II - Input Array Is Sorted

[https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

## L=0, R=len-1 Approach [Self] :

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        
        l = 0
        r = len(numbers) - 1
				# initializing left arm at the extreme left and right at extreme right

        while l<r:
				# we are given that we need TWO numbers which make up EXACTLY the target sum
            if numbers[l]+numbers[r]>target:
                r = r - 1
								# sum being bigger than goal means we need lesser value from the right side (where greater numbers are)
            elif numbers[l]+numbers[r]<target:
                l = l + 1
								# sum being lesser than goal mean we need bigger value from the left side (where lesser numbers are)
            else:
                return [l+1,r+1]
								# we supposed to consider 1-indexed arrray, hence return +1s of [l,r]
```

## What I Learned :

- I’m something of a programmer myself, you know 😏