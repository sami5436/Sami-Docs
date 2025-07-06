```
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        l, r = 0, len(s)-1
        temp_char = ""
        while l <= r:
            s[l], s[r] = s[r], s[l]
            l += 1
            r -= 1
```

so easy. literally left and right pointers.

as soon as left is greater than right, break

swap left and right characters.