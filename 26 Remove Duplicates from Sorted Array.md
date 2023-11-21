# 26. Remove Duplicates from Sorted Array

[https://leetcode.com/problems/remove-duplicates-from-sorted-array/](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

## Easy Enough [self / hint from net ]

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
    # driver    
        
        dummy_list = []
				# make a dummy list and add only unique elements to it
				# initally thought about a list_dict.keys() approach but a dummy list works jus the same
        for i, num in enumerate(nums):
            if num not in dummy_list:
                dummy_list.append(num)
								# append unique numbers
        
        nums[:] = dummy_list
				# replace the list with the new one
				## nums = dummy_list[] doesnt replace the list, nums[:] does.
        return len(nums)
				# return new length of the list
```

## A Just a Bit More Concise Code:

```python
def removeDuplicates(self, nums: List[int]) -> int:
		nums[:] = sorted(set(nums))
		# set() produces an unordered list of unique elements
		# sorted() sorts a list in an ascending manner
		# nums[:] replaces a list (( simply 'nums = __ ' doesnt ))
		return len(nums)
		# return length of the array
```

## What I learned:

- Man, built in functions are fun