this is easy just need to fpocus. 

Input: nums = [2,7,11,15], target = 9
Output: [0,1]

```
def twoSum(self, nums: List[int], target: int) -> List[int]:
    d = {}
    for index, value in enumerate(nums):
        diff = target - value

        if diff in d:
            return [index, d[diff]]
        d[value] = index
```

so the idea is fairly simple. you use the hash literally to store the num and its respective index. but beofre you even do an insertion you always check to see if the current difference (target-value) exists in the hash. if it does exist that means your current number and a number in the hash actually alr exist that sum up to target