input -  nums = [1,2,3,1]
output - true

```
def containsDuplicate(self, nums: List[int]) -> bool:
    seen = set()

    for num in nums:
        if num in seen: return True
        seen.add(num)
    
    return False
```


really easy. just use a set lolz