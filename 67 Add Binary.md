# 67. Add Binary

[https://leetcode.com/problems/add-binary](https://leetcode.com/problems/add-binary)

## Reverse, Equalize, Add (//2 and %2), Carry, Reverse, Return [Self]

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        a,b = a[::-1], b[::-1]
				# first revers both the strings for ease in iterative computing

        while len(a)!=len(b):
				# to make sure no index goes out of bounds
				# an edge case could have been c[::-1] having 0 as its max bit
					# but its automatically resolved by the fact that if we need to equalize, means other number has 1 till the end
            if len(a)>len(b):
                b= b+'0'
								# append to b if b is shorter
            else:
                a= a+'0'
								# append to a if a is shorter

        c = ""
        carry = 0
        newdig = 0
				# defining sum string c, carry and newdigit 
        for i in range(len(a)):
            newdig = int(a[i]) + int(b[i]) + carry 
						# new value is sum of these three values and ranges from 0 to 3(included)
            carry = newdig//2
						# tells us if there is or is not any carry, if <2, carry automatically becomes 0
            newdig = newdig%2
						# taking remainder from mod 2, if value is 3 this will give 1 and if 2 it will give 0
            c=c+str(newdig)
						# appending the new digit to the sum string
        if carry!=0:
            c=c+'1'
						# if the loop has ended but a carry is still there we need to resolve it
						## One Liner: c=c+'1' if carry else c+''
        return c[::-1]
				# return the reverse of this string, meaning we now have our binary sum
```

## What I Learned:

- If a code doesn’t work, documenting it like this and commenting helps revising the logic and can often even help realize the exact flaw in the code. Very helpful regardless
- It is often not about ‘what solution takes lesser time to run’ but instead about ‘what solution takes you lesser time for you to recall’