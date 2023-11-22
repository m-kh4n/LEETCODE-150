# 189. Rotate Array

[https://leetcode.com/problems/rotate-array/](https://leetcode.com/problems/rotate-array/)

## Splicing by Index [Self] :

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        
        k = (k%len(nums)) 
				# getting remainder so we know from which index from the opposite end we are cutting
        k = len(nums)-k
				# subtracking the index from total length to get the index from going forward

        nums[:] = nums[k:] + nums[:k]
				# x|y --> y|x
```

## What I Learned :

- Half of your life’s problems are solved by splicing if you use python for program