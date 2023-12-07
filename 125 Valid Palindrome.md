# 125. Valid Palindrome

[https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)

## Dictionary String Solutions (Halfway and Two Pointer Methods) (Works But Too Slow) [Self]:

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        dicstr = 'abcdefghijklmnopqrstuvwxyz0123456789'
				# creating a a dictionary string of all valid characters
        s2 = ""
				# the new string
        for ch in s:
            if ch.lower() in dicstr:
                s2 = s2 + ch.lower()
								# appending valid characters to the new string
								# appending by lowercasing too, so that non mismatches occur

        for i in range(len(s2)//2):
				# iterating halfway upon the new string 
            if s2[i]!=s2[-(i+1)]:
                return False
								# the moment a mismatch is encounteres simply exit by falsifying
        return True

				# ALTERNATE TWO POINTER SECOND HALF 
					'''
					l = 0
	        r = len(s2)-1
	        while l<r:
	            if s2[l]!=s2[r]:
	                return False
	            l += 1
	            r -= 1
	        return True
					'''
```

## One Pass No Extra Space Trial [Net] :

```python
class Solution:
    # 48-57 , 65-90, 97-122
		# ranges of numeric, capital and small characters respectively
    def isPalindrome(self, s: str) -> bool:
        def alnum(num):
            if ord(num)<58 and ord(num)>47:
                return True
            elif ord(num)<91 and ord(num)>64:
                return True
            elif ord(num)<123 and ord(num)>96:
                return True
            return False
						# function that checks and returns whether a character is strictly alphanumeric or not

        l = 0
        r = len(s) - 1
				# initializing our two pointers

        while l<r:
				# the pointers should never pass by each other
            
            while l<r and not alnum(s[l]):
                l = l + 1
            while r> l and not alnum(s[r]):
                r = r - 1
						# we wait till characters at both the pointers are alphanumeric
            
            if s[l].lower()!=s[r].lower():
                return False  
								# return false at the moment of mismatch
            
            l = l + 1
            r = r - 1
						# respective incrementation of pointers

        return True
```

## A Better Way of Comparing ASCIIs [Net/NeetCode] :

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:

        l = 0
        r = len(s) - 1

        while l<r:
            
            while l<r and not alnum(s[l]):
                l = l + 1
            while r> l and not alnum(s[r]):
                r = r - 1
            
            if s[l].lower()!=s[r].lower():
                return False  
            
            l = l + 1
            r = r - 1

        return True
```

## What I Learned :

- About clever ways of comparing ascii values with help of ord() function