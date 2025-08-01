# Number of Islands ( in Grid )
Given a grid of size `N x M` (N is the number of rows and M is the number of columns in the grid) consisting of `0`s (Water) and `1`s(Land). Find the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically or diagonally i.e., in all 8 directions.

**Approach :**
- Create a 2D visited array and initialize all values as false. Initialize a counter for the number of islands.
- Loop through each cell in the grid. If the cell is land and not yet visited, it signifies the start of a new island.
- Use BFS to explore all connected land cells starting from this cell and mark them visited.
- Increase the island count after completing the BFS for the current island.

Time Complexity : O(V+E)  = O(n*m)

Code:
```cpp
class Solution{
public:
    bool valid(int i, int j, int n, int m){
        if(i<0 || i>=n)return false;
        if(j<0 || j>= m) return false;
        return true;
    }
    void bfs(int i, int j, vector<vector<bool>> &vis, vector<vector<char>> &grid){
        vis[i][j] = true;
        queue<pair<int,int>> q;
        q.push({i,j});
        int n=grid.size();
        int m=grid[0].size();
        while(!q.empty()){
            pair<int, int> cell = q.front();
            q.pop();
            int r = cell.first;
            int c = cell.second;
            for(int delr = -1; delr <= 1; delr++){
                for(int delc = -1;delc<=1;delc++){
                    int nr = r + delr;
                    int nc = c + delc;
                    if(valid(nr,nc,n,m) && grid[nr][nc] == '1' && !vis[nr][nc]){
                        vis[nr][nc] = true;
                        q.push({nr,nc});
                    }
                }
            }
        }
    }
    int numIslands(vector<vector<char>> &grid){
        int n=grid.size(); 
        int m=grid[0].size();
        int cnt=0;
        vector<vector<bool>> vis(n, vector<bool>(m,false));
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(!vis[i][j] && grid[i][j] == '1'){
                    cnt++;
                    bfs(i, j, vis, grid);
                }
            }
        }
        return cnt;
    }
};

```
