# 11. Container With Most Water

[https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/)

## Half Working Sliding Window Attempt [Self] :

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        most = 0
				# defining the most variable

        l = 0
        r = len(height)-1
				# initalizing the right and the left variables

        max_l = 0
        max_r = 0
				#defining the current min and max from left and right  pointers

        while l<r :
				# keeping l and r unpassed
            
            if height[l]>=max_l:
                max_l = l
            if height[r]>=max_r:
                max_r = r
						# updating our max l and r values

            
            cur = (max_r-max_l)*min(height[max_r],height[max_l])
            most = max(most, cur)
						# updating the current most value

            
            l = l + 1
            r = r - 1
            
        return most
```

## Two Side Parallel Approach [Self] :

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        most = 0

        l = 0
        r = len(height)-1

        while r>0 and height[r-1]>height[r]:
            r = r - 1
				# keep incrementing till we still have greater values behind
        
        while l<r and height[l+1]>height[l]:
            l = l + 1
				# keep incrementing till we still have greater values ahead

        most = (r-l)*min(height[r],height[l])
				# get the final greatest value

        return most

# Edge Case : [1,2,4,3]
```

## Alternate of Two Side Parallel Approach [Self] :

```python

class Solution:
    def maxArea(self, height: List[int]) -> int:
        most = 0

        l = 0
        r = len(height)-1
        change = True

        while change : 
				# same thing we did above can be done in a single loop
            change = False
            if height[r-1]>height[r]:
                r = r - 1
                change = True
            if height[l+1]>height[l]:
                l = l + 1
                change = True
						# if left and right have bigger values increment them

            most = max(most, (r-l)*min(height[r],height[l]))

        return most

# Still, the edgecase [1,2,4,3] persists
```

## Well.. I Was Pretty Close [Hint/Self] :

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        most = 0
        l = 0
        r = len(height)-1
				# defining the necessary variables once again

        while l<r : 
				# as we are approaching from opposite side, termination is at l==r
            most = max(most, (r-l)*min(height[r],height[l]))
						# each iteration we update the most value, in comparision with the current window valie
            if height[l]<height[r]:
                l = l + 1
            else:
                r = r - 1
						# the trick is... to only increment the arm of smaller height,
        return most
				# return the final count
```

## What I Learned :

- Trying to persist on a problem for 40mins lays a great amount of ground for you to make the net solution more digestible, and makes it more malleable to your hands