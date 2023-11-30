# 12. Integer to Roman

[https://leetcode.com/problems/integer-to-roman/](https://leetcode.com/problems/integer-to-roman/)

## Simple 2 Array Solution [Self] :

```python
class Solution:
    def intToRoman(self, num: int) -> str:
        roman = ['M', 'CM', 'D', 'CD', 'C', 'XC', 'L', 'XL', 'X', 'IX', 'V', 'IV', 'I']
        numer = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1]
				# at first i thought of making a hashmap but i also wanted to have iteratiblity
				# thought of doing 2 while loops, one with IIII type elements and then converting them to IV and such
					# but then i thought of simply adding the 900, 400, 90, 40, 9, 4, in the arrays itself

        Rom = ""
				# first initialize an empty string
        i = 0
				# initialize index as zero
        while i<len(numer) and num!=0:
						# stop only when i exceeds length of the num becomes zero
            if numer[i]>num:
                i = i + 1
								# increment index if the element at i is greater than our current num value
            else:
                Rom = Rom + roman[i]
                num = num - numer[i]
								# if the element at i is less than our equal to our current num value,
									# append the roman equivalent to the string
									# subtract that number from current num value too
        return Rom
```

## What I Learned :

- I used to think that if an array doesnt work try a hash, if a hash doesnt try a tree etc etc. But when I started thinking that if one array doesnt work, will 2 work? if they dont then will a hashmap work? if not, will 3 simple integers work? , it opened up my thinking spectrum