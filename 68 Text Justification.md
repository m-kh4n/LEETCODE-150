# 68. Text Justification

[https://leetcode.com/problems/text-justification/](https://leetcode.com/problems/text-justification/)

## A Two Function Solution Built in 2hrs :

```python
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        str_arr = []
				# create the string array which will store all of our justified strings

        def makeString(l,r,curr):
				# this function is called for each of the window,
				# we basically get a set of words and we have to construct a justified string out of it
            ins_str = ""
            wordnum = r - l
						# number of words will be the left arm subtracted from the right arm
						# the item at the r is not in our new string, we only are including l to r-1

            if wordnum==1 or r>=len(words):
						# as given in the problem, if there is just one word or if its the last line,
							# (hence, if r is same as length of word, meaning we are catching till len-1
							# we simply do a left align justification

                ins_str = " ".join(words[l:r])
								# we join all the words with individual spaces
                ins_str = ins_str + " "*(maxWidth - len(ins_str))
								# then we add all the remaining spaces in front of it till we have got maxWidth
            else:
						# if its not the last line neither a single word, then we'll need to justify
                curr = curr - wordnum
								# in our main loop we are counting the current line value with spaces added for each of the word
								# here to remove the space count from the current length we simply subtract it
                space = (maxWidth-curr)//(wordnum-1)
								# this gives us the average space that is to be assigned between each word
								# it is possible that the average may still not give us a length of maxWidth hence,
                ext = (maxWidth-curr)%(wordnum-1)
								# we define the remaining extra addition space that we'll need to assign b/w some words
								# we are to assign these extra spaced to word from the left
								# note that the ext variable gives us the number of words that will get the extra space
		            # (we will only need to add 1 extra space to these words in all cases)
                if ext>0:
								# if our remainder is non zero, means extra spaces are to be assigned
                    ins_str = ((space+1)*" ").join(words[l:l+ext]) + ((space+1)*" ")
										# first 'ext' number of words from subarray joined by extra space and an extra space after it
                    ins_str = ins_str + (space*" ").join(words[l+ext:r])
										# then we add the remaining words with the normal amount of spaces to them
                else:
                    ins_str = (space*" ").join(words[l:r])
										# had our remainder been 0, we simply just join the whole subarray by the same space amount
                
            str_arr.append(ins_str)
						# append our final string into our string array

				# OUR MAIN SLIDING WINDO
        l = 0
        r = 1
        curr = len(words[l]) + 1
        # '1' for the space padding

        while r<len(words):
				# keeping righ arm inbound
            curr = curr + len(words[r]) + 1
						# adding into our current length with the new word an a space
            if curr-1>maxWidth:
						# if we have just gone over the max width (subtracting the 1 space from the last element)
                curr = curr - len(words[r]) - 1
								# we set our current value to subtracted new word (which made it exceed) and its 1 space
                makeString(l,r,curr)
								# executing the string addition protocol
                l = r
								# setting the left arm to the new current value
                curr = len(words[l]) + 1
								# resetting the current lenth back to the current word length with its space
            r = r + 1
						# incrementing our curent pointer ( the right arm )
        
        makeString(l, r, curr)
				# after loop has finished, we still need to execute our makestring for a last time
				# if the last element had already been executed, this will simply take the l value being just one less than r
				# and hence the element will not be added to our string array
        
	      return str_arr
				# returning our string array
```

## What I Learned :

- It takes a while, but from the get go you can know if you are going somewhere or moving in circles
- Also, the newly discovered golden rule is that,
    
    > “(While solving a problem) If you are lost at coding, its probably because you shouldn’t be coding **yet”
    > 
    > 
    > - Andy Harris
    >