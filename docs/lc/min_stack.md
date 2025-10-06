```
class MinStack:
    def __init__(self):
        self.stack = []
        self.mins = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        # push the new min so far
        if not self.mins:
            self.mins.append(val)
        else:
            self.mins.append(min(val, self.mins[-1]))

    def pop(self) -> None:
        self.stack.pop()
        self.mins.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.mins[-1]
```

tbh lookign at this i was like bruh this is too easy. so i was like let me jsut do it quickly but then i realized we need an o(1) big 0 for all functions including the getMin


so thats why i created a temp stack named min that will keep track of the min the entire time
