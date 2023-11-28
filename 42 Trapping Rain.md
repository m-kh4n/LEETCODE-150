# 42. Trapping Rain Water

[https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/?envType=study-plan-v2&envId=top-interview-150)

## Attempt [Self] (Sliding Window) :

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        
        units = 0
				# initializing the sum variable
        l = 0
        r = 1
				# initializing left and right arms of the window

        while r< len(height):
				# keeping the right inbound
            if height[r]>height[l]:
						# soon as the height of the right column becomes greater than the left, shift windows
                l = r
                r = r + 1
            else:
						# if left column stay bigger than the right column, keep adding units
                units += height[l]-height[r]
                r = r + 1
        return units

# Edge Case: [0,1,0,2,1,0,1,3,2,1,2,1]
```

## Solution [Self] :

Thought process :

![rainwatertrap.png]([42%20Trapping%20Rain%20Water%20d432a6f378b2441a92099d05aa502c5b/rainwatertrap.png](https://www.notion.so/wazir/42-Trapping-Rain-Water-d432a6f378b2441a92099d05aa502c5b?pvs=4#90c06a3ec5ff4c2ab3fb8fd498801c3d))

[0,1,0,2,1,0,1,3,2,1,2,1]

we get output 10, while we needed 6.

looking backward from last value, we can see which 4 extra blocks it has added mistakenly

it also tells that, had this array been reverse of itself our algorithm would have given 12 extra blocks

so we realize, all we need to do is to recalculate our blocks between the the max value (currently l) and the right most value (currently r-1) while also subtracting the mistaken values from before

we basically are applying our algorithm again but on height[ l : r : -1]  while also subtracting the mistaken values from the units integer

we do that by initializing a new pointer l2, which goes leftward, and our r pointer changes when a new height is acquired. basically now, r is the new l and l2 is the new r. as we are going backwards

also at every step we subtract the difference between that value and the max left value.

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        
        units = 0
				# initializing the sum variable
        l = 0
        r = 1
				# initializing left and right arms of the window

        while r< len(height):
				# keeping the right inbound
            if height[r]>height[l]:
						# soon as the height of the right column becomes greater than the left, shift windows
                l = r
                r = r + 1
            else:
						# if left column stay bigger than the right column, keep adding units
                units += height[l]-height[r]
                r = r + 1

        r = r - 1
				# r was len(height) rn so we decremented it

        if height[l]>height[r]:
				# checking if height of l is strictly greater than height of right
            r = r
            l2 = r
						# initializing the new pointers
            while l2>=l:
						# we only need to recalculate till the max height
                units -= height[l] - height[l2]
								# subtracting the unnecessary values...
                if height[l2]>=height[r]:
                    r = l2
                    l2 = l2 - 1
										# reminder that this new l2 pointer runs backwards
	
                else:
                    units += height[r]-height[l2]
                    l2 = l2 - 1
										# ...while adding back the correct values
        
        return units
```

## What I Learned :

- Sometimes you can sit at an easy problem for 4hrs, other times you solve a Hard problem in an hour without any hints. Maybe the latter is BECAUSE of the former, not despite it.
