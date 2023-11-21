# 66. Plus One

## TRY 1 [Self]

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        if digits[-1]<9:
            digits[-1]=digits[-1]+1
						# if the last digit is not nine simply increment the last digit
        else:
            digits[-1]=1
            digits.append(0)
						# if last digit is 9 increment it to 1 and append a 0
        return digits
				# return the new modified list

				# edge case, 9 may occur not only at end but before it multiple times too
```

## TRY 2 [Self]

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        if digits[-1]<9:
            digits[-1]=digits[-1]+1
						# if last digit not 9, increment by just 1
        else:
            i = len(digits)-1
						# initialize with last index in the array
            while(digits[i]==9) and i>=0:
                digits[i]=0
                i = i - 1
								# till the string of 9 continues, make them 0
            if i==-1:
						# if we have reached i=1 means that 9 was the first digit in array
                digits.append(0)
                digits[0]=1
								# hence we make the first digit 1 and add a new 0 
            else:
                digits[i]=digits[i]+1
								# if we have exhausted the list of strings of 9 and havent reache -1
								# just increment the value at index i
        return digits
				# return the new updated array
```