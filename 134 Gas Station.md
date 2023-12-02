# 134. Gas Station

[https://leetcode.com/problems/gas-station/](https://leetcode.com/problems/gas-station/)

## Failed Nested Loop Noob Solution [Self] :

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        

        for ind in range(len(gas)):
				# for each index we run the loop
            temp = ind
						# saving the ind value for later comparision
            cur = gas[ind]
						# setting the current value as the current
            ind = ind + 1
						# we will now check from this onward

            while cur>=0:
                
                cur = cur - cost[ind-1] + cost[ind]
								# while our current stays positive and we havent reached back value ind yet

                if ind==temp:
                    return ind
										# if we have reached back to the original index, return that index
                else:
                    if ind==len(gas)-1:
                        ind = 0
												# if we have reached the last index, we cant increment so we set back to zero
													
                    else:
                        ind = ind + 1
												# if not last index, increment the index
        
        return -1

'''
EDGECASE :
gas = [2,3,4]
cost = [3,4,3]
(gives 0 should give 4)
'''
```

## (Edged)  Difference Array Two Loop Solution [Hint/Self] :

[https://youtu.be/lJwbPZGo05A?t=245](https://youtu.be/lJwbPZGo05A?t=245)

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        
        diff = []
				# define the difference array
        for ind in range(len(gas)):
            diff.append(gas[ind]-cost[ind])
						# append differences in gas units and cost to next station
        for ind, dif in enumerate(diff):
				# now, enumerating through the difference array
            if dif>=0 and sum(diff)>=0:
								# if we found a difference instance that is positive, we return the index simply
                return ind
        return -1
				# if none found, -1 returned

'''
EDGECASE: 
gas = [5,1,2,3,4]
cost = [4,4,1,5,1]
(gives output 0, should be 4)
'''
```

## NeetCode Solution [Net] :

```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        if sum(gas)<sum(cost):
            # if total gas required more than our cumulitive cost,
                # there is no possibility of a solution
            return -1

        # if we are having sum[gas] be equal to the required sum[cost], 
            # means a solution definitely exist, 
            # we are also given that the solution is completely unique in each case
        
        pos = 0
        future_bal = 0
        # defining our resultant position and the future balance we'll have from this positon

        for i in range(len(gas)):
            future_bal += gas[i] - cost[i]
            # this is what will remain when we get to the next station
            # this should always stay positive, if go negative means terminate current path

            if future_bal<0:
                future_bal = 0
                pos = i + 1
                # if we will have a non positive balance after traveling from here, 
                    # it means there is no solution till now, so we set it to the next ind by nature
                # what if we are at the last index? will the ith pos set to an out of bound index?
                    # first off all, we have already made sure that a solution exists definitely
                    # so its not even possible for i to be at the last index and still enter this if
                    # also, regarding the 'looping back to the 0th' index for checking, we dont need to
                        # https://youtu.be/lJwbPZGo05A?t=597
        
        return pos
```

## What I Learned :

- That my scope of solution is actually just 30 mins. In the 0 to 20 min i map out the problem, 20th to 30th i feel like im onto something, 30th to 40 i code and debug the solution. 50 i submit. If im not able to hit that “onto something” mark by the 20 or the 30th minute, i do not know the problem and need help. (temporary conception, subject to future change)
- Some problem are by nature not intuitive on their solution.
- Like musashi said, if you dont win by using your way, its not a win. So a loss of 13 day coding streak by trying to workout yourself is far better than copy pasting a non internalized solution just for the 14th day of streak. You did your daily 2hr, thats more than enough
- New Day, New Streak