# 242. Valid Anagram

[https://leetcode.com/problems/valid-anagram/](https://leetcode.com/problems/valid-anagram/)

## Two Hashmap Solution :

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        dict_s = {}
        dict_t = {}
				# defining the two needed hashmaps

        if len(s)!=len(t):
            return False
				# if length is not same, they simply are not anagrams

        for i, ch in enumerate(s):
            if ch in dict_s:
                dict_s[ch] += 1
            else:
                dict_s[ch] = 1
						# append characters each to the s hashmap
            
            if t[i] in dict_t:
                dict_t[t[i]] += 1
            else:
                dict_t[t[i]] = 1
						# append characters each to the t hashmap

        return dict_s==dict_t
				# return the equality of these two hashmaps
```

## Library One Liner and O(1) Space One Liner :

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s)==Counter(t)
				# counter is a built in function. no innovations here

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s)==sorted(t)
```

## What I Learned :

- NEVER solve your daily problem at 1 AM, leetcode will still show one pending, it doesnt get counted