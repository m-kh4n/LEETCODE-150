# 121. Best Time to Buy and Sell Stock

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/?envType=study-plan-v2&envId=top-interview-150)

## Classic Brute Force O(n^2) Solution:

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        
        cur_max = 0

        for i in range(len(prices)):
            for j in range(i+1, len(prices)):
		# go only forward from i's value
                if cur_max<=prices[j]-prices[i]:
                    cur_max=prices[j]-prices[i]
			# change the max value 

        return cur_max

# Edge Case: (an actual array of every number in descedngin order from 10,000 to 1 followed by 300 0's)
```

## Tower of Babel Solution (the more you build it the more it breaks down)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:

        hashfun = {}
	# initializing the hash function

        for i in range((len(prices)//2)+1):
                hashfun[prices[len(prices)-1-i]-prices[i]] = [i,len(prices)-1-i]
		# adding elements to the hashfunction

        while len(hashfun)>1:
		# run till there are more than 1 entries in the hash function
            newhash = {}
			# temporary hash 
            new_arr = list(hashfun.keys())
			# append values of newhash into an array
            index = 0
            while index<len(new_arr)-1:
			# keeping one step behind for later index+1 reference

                # [..,a,c,...d,b,..] in the prices array                
                a,b = hashfun[new_arr[index]]
                c,d = hashfun[new_arr[index+1]]
		# catching the index values

                ac = prices[c] - prices[a]
                ad = prices[d] - prices[a]
                ab = prices[b] - prices[a]
                cd = prices[d] - prices[c]
                cb = prices[b] - prices[c]
                db = prices[b] - prices[d]
                m = max(ac, ad, ab, cd, cb, db)
		# comparing all the index values and deciding wich one gives biggest diff
		# but only commparing the 

                if ac==m:
                    newhash[ac] = [a,c]
                elif ad==m:
                    newhash[ad] = [a,d]
                elif ab==m:
                    newhash[ab] = [a,b]
                elif cd==m:
                    newhash[cd] = [c,d]
                elif cb==m:
                    newhash[cb] = [c,b]
                else:
                    newhash[db] = [d,b]
		# assign the index and the value for the max pair

                index = index + 2
            hashfun = newhash
		# update hashfunction
        
        hashlist = list(hashfun.keys())
	# catch the value
        
        if hashlist!=[]:
	# hashlist should not be empty
            a, b = hashfun[hashlist[0]]
            if a<b and hashlist[0]>0:
		# a should have a lesser index than b
                return hashlist[0]
        return 0

# Edge: [3,2,6,5,0,3]
```

## O(1) Space, 2 Variable, 1 For Loop Solution [Net] :

[https://youtu.be/34WE6kwq49U](https://www.youtube.com/watch?v=34WE6kwq49U&t=489s)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        
        max_prof = 0
        min_yet = 99999     # max value of price goes 10^4
        for price in prices:
            min_yet = min(min_yet, price)
		# catches the minimum yet price
            profit = price - min_yet
		# calculate profit earned upon selling at current rate wrt the minimum price yet 
            max_prof = max(max_prof, profit) 
		# if profit is greater than max profit yet, update profit
        return max_prof
```

## Sliding Window (OPTIMAL) [Net] :

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
	# right arm will go extending till end of the array and only record the max profit yet
	# left arm will be replaced only when it encounters a better candidate for itself
	# even if a numerically better candidate is acquired for left arm,
		# doesnt mean that max profit from previous window will be discarded
		# it will retain itself untill any subsequent window actually manages to replace it 
			
        l = 0
        r = 1
	# initializing the left and right pointers at first and second element in the array
        max_prof = 0
	# initializing max profit as zero so that if no profit gained, 0 is returned

        while r<len(prices):
	# right arm goes till end of array
            
            if prices[r]<prices[l]:
                l = r
		# when a new low acquired, l is relocated
		# ( max profit from last window still retained )

            if prices[r]-prices[l]>=max_prof:
		# simply max_prof = max(max_prof, prices[r] - prices[l]) works too
                max_prof = prices[r] - prices[l]
		# max profit change when the values in new window manage to give a better deal
		
            r = r + 1
	# pointer incrementation

        return max_prof
```

## What I Learned :

- Only document solutions which at least passed the default testcases
- Do NOT spend more than 10 minutes for a solution. If its not clicking automatically. Just subscript the old solution, go into solution tab, look at it, try to understand it, if not that easy to replicate, watch youtube video.
