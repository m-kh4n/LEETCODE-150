# 274. H-Index

[https://leetcode.com/problems/h-index](https://leetcode.com/problems/h-index)

## [FAILED] Loop to A Reversed Sorted List :

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        
        citations[:] = sorted(citations, reverse=True)
				# first sort the list in a reverse matter

        for i in range(len(citations)):
            if i+1>=citations[i]::
                break
						# catch basically the index at which there are more elements before the element than its index
						# e.g. in [6,5,3,1,0] we break at index i=2 a
						# we return this ith element as our result
        if len(citations)==1:
				# if there are exactly 1 element in the citation list, means h index is 1
            if citations[0] == 0:
						# if that count is 0 means we only have 0
                return 0
            return 1
        return (citations[i-1])
				# why do we return citations-1 when we catch the citation at index i...?

# Edge Case :
	
```

## [ MADEITWORK ] Loop to a Reversed List :

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
				# Realizing that you should not return the index, but the number of elements till that index
				# hence no need for if len==1 and if len==0

        citations = sorted(citations, reverse=True)
				# Reverse sort the array
        i = 0
        while i<len(citations) and i<citations[i] :
				# while i stays inbound and while the number of elements on leftside remain less than citation of current paper
            i = i + 1
						# increment the the index pointer
        return len(citations[:i])
				# the number of elements till that index denote the h-index
				# h-index definition:
					# maximum value of h such that the given researcher has published at least h papers,
							# that have each been cited at least h times

# works for [3,1,1]. how? dont know. but does. and thats what matters.
```

## What I Learned :

- Design the algorithm based on the testcases and then write the code. Do not keep altering the code according to the testcases again and again. It is immensely useless.
- If you cant manage to come up with a working algorithm, not even a maximum complexity one. Or you cant manage to make the algorithm in your mind work rigidly. Then just look for the solution.