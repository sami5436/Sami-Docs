max num balloons from random text with random chars

```
def maxNumberOfBalloons(self, text: str) -> int:
        count = Counter(text)
        return min(
            count.get('b', 0),
            count.get('a', 0),
            count.get('l', 0) // 2,
            count.get('o', 0) // 2,
            count.get('n', 0)
        )
```

pretty straight forward. just add all counts of each char to a dict and find the min number of occurences for each char except for l and o since they appear twice so modulo 2 on those.
