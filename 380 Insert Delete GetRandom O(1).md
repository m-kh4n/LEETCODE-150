# 380. Insert Delete GetRandom O(1)

[https://leetcode.com/problems/insert-delete-getrandom-o1/](https://leetcode.com/problems/insert-delete-getrandom-o1/?envType=study-plan-v2&envId=top-interview-150)

## 1 Hashmap 1 Array [Hint/Self] :

```python
import random

class RandomizedSet:
    hashmap = {}
    array = []
		# defining our two key object attributes
			# an empty array and and empty hashmap
			# the hashmap saves the inserted 'val' as its key and its index in the array as its value
			# note that as it is a 'set' no value can be inserted twice
			# to know why this is done, refer to the value removal function

    def __init__(self):
        self.hashmap = {}
        self.array = []
        # initializing the hash and the arrays as empty
				# this keeps every instance of the random set a clean fresh slate m

    def insert(self, val: int) -> bool:
        if val in self.hashmap.keys():
            return False
						# if value was already present in the set, we simply return false
        else:
						# when a new value is being inserted
            self.array.append(val)
						# first append that value into the array
            self.hashmap[val] = len(self.array)-1
						# as the newly appended value will be ocurring at the end of the array, we simply catch it
            return True
						# return true when the value is finsished being inserted
        
    def remove(self, val: int) -> bool:
				# for removal function to be o(1) and still keep random choice as truly random
					# we simply search the
        if val in self.hashmap.keys():
				# if the value to be removed is present in the set
            ind = self.hashmap[val]
						# first we catch the original index of the value to be removed in the array
            self.array[ind] = self.array[-1]
						# next up we replace that value with value at the end of the array and vice verca
            self.hashmap[self.array[ind]] = ind
						# next, we set the new index of the value now at our index (previously last elment) to our index
							# this line should stay above the upcoming pop lines to avoid any out of bounds error
            self.hashmap.pop(val)
						# simply pop that key value pair from the hashmap by calling pop on the key value (all O(1))
            self.array.pop()
						# by popping the array we are removing the previously at 'ind' 'val', now at last element
            return True
						# return true when operation is completed
        else:
            return False
						# return simply false if the value to be removed is not even in the set
    def getRandom(self) -> int:
        return random.choice(self.array)
				# by importing random you can simply use this function from that library to choose from a list
				# all elements of the list get an equal probablity of being chosen here

# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

### What I Learned :

- Use of Random library
- Found out that popping by the key value in a hashmap removes the key value pair completely from it