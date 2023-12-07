# 238. Product of Array Except Self

[https://leetcode.com/problems/product-of-array-except-self/](https://leetcode.com/problems/product-of-array-except-self/submissions/?envType=study-plan-v2&envId=top-interview-150)

## Overall Product Divided By Element [Self] :

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        prod = 1
				# initializing product value as 1
        zero_in_arr = 0
				# zero flag counter
        for num in nums:
            if num==0:
                zero_in_arr += 1
								# increase zero flag after each encounter, but dont multiply it into the product
            else:
                prod = prod*num
								# multiply all non zero elements into the product

        for i in range(len(nums)):
            if zero_in_arr>1:
						# if there are more than 1 zeroes in the array, means every element will be zero
                nums[i] = 0
            elif zero_in_arr==1:
						# if only 1 zero, means all values will be zero except the actual zero value
                if nums[i]==0:
                    nums[i] = prod
                else:
                    nums[i] = 0
            else:
                nums[i] = prod//nums[i]
						# if no zeroes in the array, means every element will simply be overall product divided by that element

        return nums
				# return the modified array
```

## What I Learned :

- That some simple flags and 2 to 3 integers can sometimes take an ‘n’ away from inside your O