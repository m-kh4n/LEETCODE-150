# 14. Longest Common Prefix

[https://leetcode.com/problems/longest-common-prefix/](https://leetcode.com/problems/longest-common-prefix/submissions/)

## Failed “almost there” Solution :

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        
        i = 0
        if len(strs)==0:
				# if no elements in the list, just print null string
            return ""
        if len(strs)==1:
            return strs[0]
				# if one element in string it means that all element are same, print the whole thing

        while strs[0][0:i]==strs[1][0:i] and len(strs[0])>1 and len(strs[1])>1 and i<len(strs):
				# compare the first two strings in the list first and see how much same they are
				# considering that the lenth of both string are greater than 1 and i hasnt exceeded bound
            i = i + 1
						
        
        for j in range(len(strs)):
				# now check if the splice is common for all the strings in the list
            if strs[0][0:i] != strs[j][0:i]:
						# when a string is not matching, get the splice one index back
                i = i - 1

        if i>1:
            return strs[0][0:i-1]
						# if splice exceeds index 1, use this formula
        if i==1:
            return strs[0][0:i]
						# if it doesnt, use this
        return ""
```

## OVER ENGINEERED, OVER FAILED, OVER EXHAUSTE

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        
        i = 0
        if len(strs)==0:
            return ""
        if len(strs)==1:
            return strs[0]

        while strs[0][0:i]==strs[1][0:i] and i<200:
            i = i + 1

        for j in range(len(strs[0])):
            if i+1>len(strs[j]):
                i = i - 1
                continue
            if strs[0][0:i] != strs[j][0:i] :
                i = i - 1
                j = j - 1

        if i>=0:
            return strs[0][0:i+1]
        return ""
```

## Net Solution:

[https://www.youtube.com/watch?v=0sWShKIJoo4](https://www.youtube.com/watch?v=0sWShKIJoo4)

## FINAL TIGDAM [self/net]:

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:

        shortest = min(strs, key=len)
				# first catch the shortest word in the whole list
				# the min function takes the list, and 'key' attribute decides the criteria of choosing

				# WE ARE CHECKING THROUGH EVERY WORD FOR EACH CHARACTER OF THE SHORTEST WORD
				# e.g. f,f,f... l,l,l,,, o,o,i! terminate at o index. [:o-index] will catch "fl"
        for ind, char in enumerate(shortest):
				# we are now iterating through every character of the shortest word
				# enumerate function, the best of both worlds, gets the index and the character as well
            for word in strs:
						# iterating through all the other words in the list
                if word[ind]!= char:
								# if the character of the the other word at that same index is same as the shortest keep running
								# terminate at the first instance of mismatch
								# at the first point of mismatch, the index will indicate the substring end
                    return shortest[:ind]
        				
        return shortest
				# if the loop goes through everything and doesnt find a mismatch, it means every string is equal
					# or that the shortest word is common through every word, so just return i
```