jewels = "aA", stones = "aAAbbbb"

output - 3

since a or A appear 3 times the output is 3

```
def numJewelsInStones(self, jewels: str, stones: str) -> int:
    refined_jewels = set(jewels)
    count = 0
    for stone in stones:
        if stone in refined_jewels:
            count += 1
    return count


```

pretty easy. 


the brute vs optimal are very similar. but in this case the only thing im doing is set-ing the jewels just incase it originally has any duplicates which is a waste of time

