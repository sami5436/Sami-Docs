```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list) 
        
        for wrd in strs:
            sig = tuple(sorted(wrd)) 
            groups[sig].append(wrd)
        print(groups)
        return list(groups.values())
```

aangram problem given list of different words u need to return a lsit of lists

so i originally thinking boom use a dict.

ok how do we use a dict...


well an anagram has teh same chars in the entire group and so we sort the chars and use that as our "key" in a dict

if it exists, itll add to the exisiting value list. if not, a new one will be created
