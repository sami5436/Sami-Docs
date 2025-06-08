this is super easy. return true or false whether char count in t and s are equal to each other.



```
def isAnagram(self, s: str, t: str) -> bool:
    return Counter(s) == Counter(t)
```

there is a more optimized space mem solution ig lolz. 
- well first thing is compare lenghts of t and s (quick edge case and can reduce run time too)
- init an array of 26 0s
- iterate thru the indices of s or t, and subtract the ord for that current character u are on to ord(a) and add 1 to that current index (doing the ord(char) - ord(a) will return an index between 0-25. this 0-25 is for the arrya init earlier)
- so the idea is you do this per char in each word but one word u -1 the other +1.
- return all(c==0 for c in count) - this will run thru the array and make sure all indices are 0ed out cuz it makes sense right. like you add one and subtract one and even tho it may not be in the correct pos at teh end they will all.

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False  # If lengths differ, they can't be anagrams

        count = [0] * 26  # Array to store counts of 26 lowercase letters

        for i in range(len(s)):
            count[ord(s[i]) - ord('a')] += 1  # Increment count for char in s
            count[ord(t[i]) - ord('a')] -= 1  # Decrement count for char in t

        return all(c == 0 for c in count)  # All counts should be zero
```