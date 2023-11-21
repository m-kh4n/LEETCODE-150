# 28. Find the Index of the First Occurrence in a String

[https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

## Using Library Functions [Self]

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        return haystack.index(needle) if needle in haystack else -1
				# single line with help of library functions
				# alternate single line with use of find() function:
					# return haystack.find(needle)
```

## Without Use of Any Library [Net]

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:

        for index in range(len(haystack) - len(needle)+1):
				# iterate through the haystack with 3 steps behind needle's length
            if haystack[index:index+len(needle)] == needle:
						# see if the substring needle length steps ahead is same as needle
						# if yes, return the index
                return index
        return -1
				# if needle not found till end of the haystack, return -1
```

## What I learned:

- Leetcode time taken is often very unreliable, dont sweat over it