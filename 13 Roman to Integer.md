# 13. Roman to Integer

[https://leetcode.com/problems/roman-to-integer](https://leetcode.com/problems/roman-to-integer/submissions/)/

## Failed Comparison Approach Solution :

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        diction = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}

        sumval = 0
        addval = 0
        for ind in range(len(s)):
            char = s[ind]
            if char=='I' and ind<len(s)-1:
                nextchar = s[ind+1]
                if nextchar!='I':
                    counter = 1
                    tempvalue = diction[nextchar]
                    if tempvalue==None:
                        tempvalue = 0
                    while tempvalue>0:
                        counter = counter*10
                        tempvalue = tempvalue // 10
                    addval = -1*counter/10
                else:
                    addval = 1
            else:
                addval = diction[char]
            sumval = sumval + addval
```

## THE REPLACEMENT SOLUTION [from net] :

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman = {'M': 1000, 'D': 500, 'C': 100,  'L': 50, 'X': 10, 'V': 5, 'I': 1}
        # the six 'IV' type cominations are: IV, IX, XL, XC, CD, CM

        s = s.replace("IV", "IIII").replace("IX", "VIIII")
        s = s.replace("XL", "XXXX").replace("XC", "LXXXX")
        s = s.replace("CD", "CCCC").replace("CM", "DCCCC")
        # making all the necessary replacements in string

        sum = 0
        for char in s:
        # now we can just simply add up everything
            sum += roman[char]
        return su
```

## Comparison Approach 2.0 [self/net] :

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman = {'M': 1000, 'D': 500, 'C': 100,  'L': 50, 'X': 10, 'V': 5, 'I': 1}
        sum = 0
	      
        for i in range(len(s)):
            if i+1<len(s) and roman[s[i]]<roman[s[i+1]]:
						# second condition checks if the next element in string has a greater roman value than the current one
						# first condition for keeping index in bound
                sum -= roman[s[i]]
								# if next's value is greater, subtract the value
            else:
                sum += roman[s[i]]
								# otherwise, add its value
        return sum
```

- When you need to make sure that x stays inbound with length of y. just write x<len(y) without any -1 +1 before after