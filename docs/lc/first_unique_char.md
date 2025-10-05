```
class Solution:
    def firstUniqChar(self, s: str) -> int:
        freq = Counter(s)
        for i, ch in enumerate(s):
            if freq[ch] == 1:
                return i
        return -1

```


ok so given a string like aabb, return the index of the first nonrepeating char. in this case, well return -1


so thinking about this init i was thinking boom lets just use a for loop and iterate thru the different indicies of the string


but then i was like nah lets use a dict


so we get a dict and grab the count of every char

then we iterate using enumarate (get us the index and the character at that index) and grab the first occurence of it and return with the i.
