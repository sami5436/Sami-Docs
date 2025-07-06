```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = s.lower()
        l, r = 0, len(s) - 1

        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1

            if s[l] != s[r]:
                return False
            l += 1
            r -= 1

        return True
```

2 pointer method. 


if left is not equal to right, return False

else just continue iterating thru

also we skip over chars that arent alphanumeric