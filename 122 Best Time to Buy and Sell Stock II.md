# 122. Best Time to Buy and Sell Stock II

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

## Simple Simple Approach [Self] :

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        
        max_prof = 0
				# define a max prof integer ( basically the sum variable )

        for i in range(len(prices)-1):
            if prices[i+1]>prices[i]:
                max_prof += prices[i+1] - prices[i]
								# whenever the next element is bigger than last, add that value into the sum
        
        return max_prof
				# return sum
```

## What I Learned :

- A simple visualization of the problem test cases can simplify the problem to a great degree