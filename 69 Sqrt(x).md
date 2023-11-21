# 69. Sqrt(x)

[https://leetcode.com/problems/sqrtx/](https://leetcode.com/problems/sqrtx/)

## Strange Linear Failed Approach

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        
        k = x//2

        while k>0:
				# while the floor value of k stays above 0
            if x - int(k*k) == 0:
                return k
								# if match found return the number
            elif k*k > x and (k-1)*(k-1)<x:
                return k-1
								# when an index passes that gives square greater than x value, return k
            
        return k

				# this whole code was supposed to run upon hopes and wished i guess
```

## Appropriate Binary Search Approach:

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        
        i,j = 0,x
				# initializing pointers of binary search

        while i<=j:
            k = (i+j)//2
						# taking midpoint
            if k*k == x:
                return k
								# if match found, return
            elif k*k > x:
                j = k - 1
								# if k gives square greater than x, search leftwards
            elif k*k < x:
                i = k + 1
								# if k gives square lesser than x, search rightward
                
        return i-1
				# if no match found and we have basically reached "closest" value
					# return the number just before
```