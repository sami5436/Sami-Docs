```
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        l, r = 0, len(nums) - 1 
        result = []
        
        while l<=r:
            if nums[r] ** 2 > nums[l] ** 2:
                result.append(nums[r]**2)
                r -= 1
            else:
                result.append(nums[l]** 2)
                l += 1
        return result[::-1]
```

pretty easy.

thought process is pretty easy. left pointer right pointer

if left is bigger, we append it,  and plus 1

if right is bigger, we append it, and minus 1

we stop when left index is bigger than right index!