# 392. Is Subsequence

[https://leetcode.com/problems/is-subsequence/](https://leetcode.com/problems/is-subsequence/)

## Dummy String Approach [Self] :

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        r = ""
				# define our comparitive string

        for ch in t:
				# iterating through characters of string t
            if ch in s:
                r = r + ch
								# appending character to comparitive string if they are in the s string
                if not s[len(r)-1]==r[len(r)-1]:
                    r = r[:len(r)-1]
										# to clear any misplaced duplicates, we pop last element from the comparitive string
        
        return r==s
				# returning the euquality of the two strings
```

## What I Learned :

- Sometimes you just start, and figure out on the way