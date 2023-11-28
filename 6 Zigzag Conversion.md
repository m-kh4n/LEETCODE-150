# 6. Zigzag Conversion

[https://leetcode.com/problems/zigzag-conversion/](https://leetcode.com/problems/zigzag-conversion/submissions/?envType=study-plan-v2&envId=top-interview-150)

## One Attempt Kill [Self] (Circular Looper) :

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        biglist = []
        for i in range(numRows):
            biglist.append("")
				# first we design a list and fill it with row-number empty string
				# these are the strings that when joine together will form our final string
        
				# visualization for moving ahead. 
					# we a are basically going in circles with the big list array
					# we go assigning forward and come back assigning backward and repeat again
					# how are zigzags (sin or cosine) formed in mathematics? same thing
						# (by a a point on a circle which is moving forward)

        loop_i = 0
	      rev = False
				# the loop index pointer tells us which string in the biglist are we assigning the character to
				# the rev boolean value defines, if we are going backwards
	
				# single loop O(n) solution
        for ch in s:

            biglist[loop_i] = biglist[loop_i] + ch
						# assigning the character to the appropriate string

						# now, for deciding where loop_i will move toward next...
            if rev:
                if loop_i>0:
                    loop_i = loop_i - 1
										# if we are going in reverse means we just reached numRows-1 value and are now going backward to 0
										# while we havent reached zero, we keep decrementing
                else:
                    rev = False
                    loop_i = loop_i + 1
										# soon as we reach 0 , we set the reverse value as false, we now go forward
										# and as the character would have already been assigne to 0th string of biglist, 
											# we increment it, basically setting value to 1
            else:
                if loop_i < numRows - 1:
                    loop_i = loop_i + 1
										# we are not going reverse, just recently touched value 0
										# hence increment till numRows-1 value is not reached
                else:
                    rev = True
                    loop_i = loop_i - 1
										# when going forward numRows-1 value reached, set reverse flag to True,
										# decrement loop_i value, as character to numRows-1 would have already been attached
            
        return ''.join(biglist)
				# return the elements of the biglist joined by an empty string in between
```

## What I Learned :

- The clearer the algorithm is in your mind, the cleaner the code, and quicker the execution will be