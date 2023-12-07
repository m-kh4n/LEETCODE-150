# 135. Candy

[https://leetcode.com/problems/candy](https://leetcode.com/problems/candy)

## Forward / Backward Pass Algorithm [Net] :

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        ans = [1]
				# you can simply append n same elements by ans = [x] * n but I decided append loop was cooler
        
        for i in range(1,len(ratings)):
				# checking and comparing current with the index at left, neaning start form 1 end at last index
            ans.append(1)
						# append a new value for our new member in the answer array
            if ratings[i]>ratings[i-1]:
                ans[i] += 1
								# if while going forward we are currently at a number bigger than its left neighbour, 
									# make our current 1 bigger than its left neighbour
        
        for i in range(0,len(ratings)-1)[::-1]:
				# now passing backward, starting from last 2nd index and going till 0
				# checking and comparing current with right neighbour
            if ratings[i]>ratings[i+1]:
                ans[i] = max(ans[i], ans[i+1]+1)
								# THIS IS WHERE FAULT HAPPENED INITALLY
									# I simply did ans[i] +=  1 ; ans[i] = ans[i+1] + 1 but nothing worked
									# the real solution is the max of current and one more than right,
										# explanation: https://youtu.be/1IzCRCcK17A?t=695
        
        return sum(ans)
				# return sum of our answer array
```

## What I Learned :

- That you can simply append n same elements by ans = [x] * n but I decided append loop was cooler
- That we can create a decreasing loop by just taking normal loop values inside range() parenthesis and just adding an [::-1]  next to it