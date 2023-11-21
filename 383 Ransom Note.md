# 383. Ransom Note

[https://leetcode.com/problems/ransom-note/](https://leetcode.com/problems/ransom-note/submissions/)

## 2 Hashmap 1 Check Loop [Self] :

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        
        rans_hash = {}
        magz_hash = {}
				# initializing the two hashes

        for ch in ransomNote:
				# adding elements to the ransom hashmap
            if ch not in rans_hash.keys():
                rans_hash[ch] = 1
            else:
                rans_hash[ch] += 1
            
        for ch in magazine:
				# adding elements to the magazine hasmap
            if ch not in magz_hash.keys():
                magz_hash[ch] = 1
            else:
                magz_hash[ch] += 1

        for ch in list(rans_hash.keys()):
				# iterate through the ransom hash table
            if ch not in magz_hash.keys() or rans_hash[ch]>magz_hash[ch]:
						# if the character is not in magz table or has lower hash value than rquired, 
							# then simply trigger the false flag and return it
                return False
        
        return True
				# when false target not triggered throughout, means ransom can be reconstructed
```

## Use of .count() function [Net]: (best performance and logic)

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        
        for i in set(ransomNote):
				# so that we avoid any unnecessary repetative comparisions
            if ransomNote.count(i) > magazine.count(i):
						# if we come across any element which has a greater count in ransom than in magazing, trigger false
                return False
				# if loop completed without any false trigger, means ransom can be reconstructed
        return True
				
```

## What I Learned :

- Use of count function in an appropriate manner
- Don’t rely much on one liner libraries too much ( Counter function could have been used here, but i thought of logic first ). Atleast use  a hybrid approach, like the use of count function in the 2nd solution