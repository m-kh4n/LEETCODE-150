# 344. Reverse String

[https://leetcode.com/problems/reverse-string/](https://leetcode.com/problems/reverse-string/solutions/?envType=featured-list&envId=top-interview-questions?envType=featured-list&envId=top-interview-questions)

## Simple Enough Halfway Solution

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
	      """
	      for i in range(len(s)//2):
	          temp = s[i]
	          s[i] = s[len(s)-1-i]
	          s[len(s)-1-i] = temp
							# or simply do s[i],s[-i-1]=s[-i-1],s[i]
						# swap the element with its counterpart from the other side

```

## Splicing Solution (One-Liner) [Net] :

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
				"""
        Do not return anything, modify s in-place instead.
	      """
        s[:] = s[::-1]
				# simply modify the list to be its reverse version
```

## What I Learned :

- That if s = s [ : : -1 ] doesn’t work. Try s [ : : ] = s [ : : -1 ]
- That for some reason s [ : : -1 ] = s   works??  ( s = s [ : : -1]  still doesn’t )