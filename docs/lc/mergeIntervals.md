# merge intervals



```
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        res = []
        intervals.sort(key = lambda x : x[0])
        res.append(intervals[0])
        # when it comes to this problem we need to make sure we always sort
        # we are going to traverse now using the start, end of every interval
        # we will store the lastEnd (first iteration, itll be the first interval)
        # we check hey is our current intervals start less than or equal to our lastEnd
        # if it is (ex - cur: (1,4). last: (0, 5)), so you take the max (in this case its obv)
        # and u store it as ur "new" lastEnd (in this case its the same)
        # if not, lets say we have (1, 4) (0, 3). obv our last end is smaller, so we hit the
        # else and just add the current interval 

        for start, end in intervals[1:]:
            lastEnd = res[-1][1]

            if start <= lastEnd:
                res[-1][1] = max(lastEnd, end)
            else:
                res.append([start, end])
        return res
```
