```
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0

        rows, cols = len(grid), len(grid[0])

        def dfs(r: int, c: int) -> None:
            stack = [(r, c)]
            while stack:
                x, y = stack.pop()
                if 0 <= x < rows and 0 <= y < cols and grid[x][y] == '1':
                    grid[x][y] = '0'  # mark visited
                    stack.append((x - 1, y))
                    stack.append((x + 1, y))
                    stack.append((x, y - 1))
                    stack.append((x, y + 1))

        islands = 0
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    islands += 1
                    dfs(r, c)

        return islands
```


tbh, i didnt even know how to start this...

but it was pretty easy once i got it figured out 

the idea is we start from 0,0. we check hey, is it 1? if it's 1 we add to the count and we run dfs. what we dfs is going to do is add all the neigbors (i-1, i+1, j-1, j+1 = 4)
to a stack. and while the stack is not empty (meaning there is still neigbhors of neigbhors that have 1s meaning a continous island, we will contunue marking them as visited 
if its at 1)

we need to make sure we run this on every index of our grid...
