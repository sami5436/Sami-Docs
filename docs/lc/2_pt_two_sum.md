```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1

        while l < r:
            current_sum = numbers[l] + numbers[r]
            if current_sum == target:
                return [l + 1, r + 1]  
            elif current_sum < target:
                l += 1
            else:
                r -= 1
```

thought process:

we use 2 pointer. 


since its sorted, we have 2 possible routes (other than it being equal to the target)
- current sum too small
- current sum too large

well, if the current sum is too small, we need to move our left index up by 1. this will allow us to incrementally move our sum up without missing any numbers on the way.

well, if the current sum is too large, we need to move our right index down by 1. this will allow us to move our sum down without missing any numbers on the way.

and obv if our current sum is equal to our target, return