# 27. Remove Element

[https://leetcode.com/problems/remove-element/](https://leetcode.com/problems/remove-element/)

## SIMPLE SIMPLE

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        dummy_list= []
				# defining a dummy list

        for num in nums:
            if num!=val:
                dummy_list.append(num)
								# append to dummy list if number not equal to the value

        nums[:]=dummy_list
				# replace the previous list

        return len(nums)
```

- Net gave another solution but it was not much better performing than this

## SOLUTION FROM NET (Performatively Same) [Net]

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        
        i = 0
        for num in nums:
            if num!=val:
                nums[i] = num
                i = i + 1
                # increment the index pointer only when the number is not the value
            # else keep index static
        return i
        # simply returning index as it will indicate the number of non-val elements in the original list
```