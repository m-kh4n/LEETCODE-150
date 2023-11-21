# 58. Length of Last Word

[https://leetcode.com/problems/length-of-last-word/](https://leetcode.com/problems/length-of-last-word/submissions/)

## Simple O(n) Solution:

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        newlist = list(map(str, s.split(" ")))
				# make the string a list split by space

        while newlist[-1]=="":
            newlist.pop()
						# to make sure the last element in the list is not an empty string

        return len(newlist[-1])
				# print length of the last string in the set of string
```

## What I Learned:

- an n/2 solution is till an o(n) solution, follow the simpler one