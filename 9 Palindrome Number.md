# 9. Palindrome Number

[https://leetcode.com/problems/palindrome-number/](https://leetcode.com/problems/palindrome-number/)

## MY SOLUTION :

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        return str(x)==str(x)[::-1]
				# return conditionality of number string being equal to its reverse string
				# reversal here done with help of splicing technique

# gives just a 17% more speed than other solutions.
```

## OPTIMIZED APPROACH :

```python
def isPalindrome(self, x: int) -> bool:
	if x < 0:
	# takes into account the edge case of the number being negative
		return False
	
	return str(x) == str(x)[::-1]
	# still following the stringconversion-splicing approach
```

## MOD 10 APPROACH :

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x<0:
            return False
        
        orgNum = x
        revNum = 0
				# defining two numbers to be compared later
        while x>0:
            revNum = revNum * 10 + x%10
						# the classic "number reversal" algorithm
            x = x//10
						# floor division so tha things like 0.123 dont get evaluated as >0

        return orgNum==revNum
				# return the conditionality of original number and reversed number being equal
```

## FINAL APPROACH (BEST PERFORMING) [from net]

The Half- Reverse Approach:

Example, if x = 15951, then initially, x = 15951, revX = 0. Through iterations:
1. x = 1595, revX = 1
2. x = 159, revX = 15
3. x = 15, revX = 159

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x<0 or (x>0 and x%10==0):
				# if a number is something like 10 or 2420 it should not be validated as a palindrome
            return False
        
        revHalf = 0
				# defining the reverse half, starting from last digit of palindrom number
        while x>revHalf:
				# loop terminated when revHalf has surpassed or equalized number of digits in x
            revHalf = revHalf * 10 + x%10
						# new digit added to
            x = x//10
						# old digit taken out of x

        return x==revHalf or x==revHalf//10
				# for even number of digits in the palindrome, x and revHalf will be equal directly to x
				# for odd number of digits, take floor division of the rev half, that is:
					# revHalf=192 will become 19 and be compared to x=19
						# as it doesnt matter whichever digit comes in the middle, palindrome condition retains
```

## ATTEMPTED A HYBRID APPROACH AND FAILED  [from net]

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x<0 or (x>0 and x%10==0):
            return False
        
        strx = str(x)
        return strx[0:len(strx)//2] == strx[0:len(strx)//2:-1]
```