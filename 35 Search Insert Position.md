# 35. Search Insert Position

[https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)

## Noob just goes for linear search [Self]

```python
class Solution:

    def searchInsert(self, nums: List[int], target: int) -> int:
        for i in range(len(nums)):
				# iterate through all the indices of the list
            if nums[i]>=target:
						# as soon as we reach an element greater than the target, return the index
                return i
        return len(nums)
				# if no such index found means list ends before reaching target value, so return len(nums)
```

## UNWORKING BINARY SEARCH BY ME [Self]

```python
class Solution:
		# couldnt define the search function outside like in C, had to define it inside
    def searchInsert(self, nums: List[int], target: int) -> int:

        def binsearch(nums, i, j):
				# the audacity to define a function within a function
            if i+1 == j:
						# if i and j have become consecutive, means the element should be at j's place
                if nums[j]<target:
                    return j+1
										# if the number is less than target, means its index should be greater than j
                else:
                    return j
										# if number is not less than j, means it should have j's index
            k = (i+j)//2
						# k is the mean of the two extremes
            if nums[k]==target:
                return k
								# if target is found at the midpoint, return the midpoint
            elif nums[k]<target:
                return binsearch(nums, k, j)
								# splice towards right side if target is greater
            elif nums[k]>target:
                return binsearch(nums, i, k)
								# splice toward left side if target is smaller
        return binsearch(nums, 0, len(nums)-1)
				# calling the function within the function, strange shit

# biggest mistake in above code is that we still keep the mid point intact while going in for the next recursion
# instead we should have passed k+1 and k-1 for right side and left side respectively
	# you will be surprised just how many calculations this one trick saves
```

## BINARY SEARCH IN A WHILE LOOP [Net]

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:

        i,j = 0, len(nums)-1
				# dual initializing values of i and j

        while i<=j:
				# loop terminates when i exceeds value of j indicating that
					# there is no such element in the list which matches the target
            k=(i+j)//2
						# taking midpoints
            if nums[k]==target:
                return k
								# return midpoint if match
            elif nums[k]>target:
						# middle element (& hence everything in the right) is greater than target
                j = k - 1
								# changing j to a new value
								# search between i and midpoint-1
            elif nums[k]<target:
						# middle element (& hence everything in the left) is lesser than target
                i = k + 1
								# changing i to a new value
								# search between midpoint-1 and j

        return i
				# if no such index of match is found, means every list item is lesser
				# when j was initialized as the biggest, and now i is basically j+1
					# means i is len(nums), which will be our index for the target

```

## Final Implementation [Self + Hint from Net]

```python
class Solution:

    def searchInsert(self, nums: List[int], target: int) -> int:

        def binsearch(nums, i, j):
            if i>j:
                return i
								# when index exceeds the j value, return i itself, meaning no match and
									# every list item is lesser than target, we basically return len(list) now
            k = (i+j)//2
						# taking midpoint
            if nums[k]==target:
                return k
								# match found, return match index
            elif nums[k]<target:
                return binsearch(nums, k+1, j)
								# search rightwards
            elif nums[k]>target:
                return binsearch(nums, i, k-1)
								# search leftwards
        return binsearch(nums, 0, len(nums)-1)
				# calling of the function
```

## What I learned:

- In leetcode solutions you need to define functions withing the main function for it to run
- That just a simple tweak of k+1 and k-1 actually saves a lot of calculations
- That binary search can be implemented with a simple while loop too (iteration vs recursion)