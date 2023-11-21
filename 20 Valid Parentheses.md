# 20. Valid Parentheses

## A Good Attempt at Pop-Match Approach

```python
class Solution:
    def isValid(self, s: str) -> bool:
        counter = {'}':'{', ']':'[', ')':'('}
				# making a complementary dictionary for later reference
        newstring = ""

        i = 0
        j = 0

	      while i<len(newstring):
				# go through every element of the original string
            if s[i] not in counter.keys():
						# if its not a closing paranthesis, simply append it to the new string (our stack)
                newstring = newstring + s[i]
                j = j + 1
								# increment the newstring pointer [indicating addition of a number]
                i = i + 1
								# increment original string pointer               
            else:
                if j-1>len(newstring) or newstring[j-1]!=counter[s[i]]:
								# if j is exceeding index, or the previous element is newstring is not opening of current closing one
                    return False
										# simply say its false
                else:
                    j = j - 1
										# here, the closing one has found a match and hence we decrement the pointer
										# popping the element
                    i = i + 1

        return len(newstring)==0
```

## Working Solution With Stack [Net/Self]:

```python
class Solution:
    def isValid(self, s: str) -> bool:
        counter = {'}':'{', ']':'[', ')':'('}
				# defining the counter dictionary
        stack = []

        for char in s:
				# iterating through characters not index
            if char in counter.keys():
						# check if the character appears in keys of the dictionary
                if stack == [] or counter[char] != stack.pop():
								# if the stack is empty or
								# ( the pop function treats the list as a stack and pops the topmost element )
								# ( 'pop' meaning it procures that element and also removes it from the stack too)
								# if the counter bracket of the character is not on topmost of the stack, return False
								# on a paranthesis match, the 2nd condition automatically pops the match
										# without declaring the paranthesis as unmatched
								# on a non-match, we go inside the if block and declares unbalanced paranthesis.
                    return False
            else:
						# always keep your elses in check. dont cut corners.
                stack.append(char)
								# if not closing paranthesis, just append it to the stack

        return stack == []
				# on a balanced string, stack should be empty
```

## What did I Learn?

1. Always keep your ifs and elses balanced dont go for else-skips
2. Control objects, not pointers. Its more effective and less confusing
3. If you cant do a problem, go to the solution tab before going to youtube
4. Laga Reh