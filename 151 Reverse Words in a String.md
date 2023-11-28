# 151. Reverse Words in a String

[https://leetcode.com/problems/reverse-words-in-a-string/](https://leetcode.com/problems/reverse-words-in-a-string/submissions/?envType=study-plan-v2&envId=top-interview-150)

## Simple 2 Line Python Lib [Self] :

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        wordlist = list(s.split())
				# list(s.split(" ")) takes " " elements in too. to get spaceless array, leave it empty
        return ' '.join(wordlist[::-1])
```

## What I Learned :

- That its ‘ ‘. join(list) not list.join(’ ‘)