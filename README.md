# Competitive-Coding-11

Please submit the interview problems posted in slack channel here. The problems and statements are intentionally not shown here so that students are not able to see them in advance 
## Shortest Path with obstacle elimination in the Grid
## Time and Space:O(mxnxk)

class Solution {
    public int shortestPath(int[][] grid, int k) {
        int[][] dirs=new int[][]{{-1,0},{0,1},{0,-1},{1,0}};
        int m=grid.length;
        int n=grid[0].length;
        boolean[][][] visited=new boolean[m+1][n+1][k+1];
        Queue<int[]> q=new LinkedList<>();
        q.add(new int[]{0,0,k});
        visited[0][0][k]=true;// 0:0th element 0:number of moves
        int moves=0, count=0;
        while(!q.isEmpty())
        {
            int size=q.size();
            for(int i=0;i<size;i++)
            {
            int[] curr=q.poll();
            if(curr[0]==m-1 && curr[1]==n-1 )
            return moves;
            for(int[] dir:dirs)
            {
                int row=curr[0]+dir[0];
                int col=curr[1]+dir[1];
                int nk=curr[2];
                if(row>=0 && col>=0 && row<m && col<n && !visited[row][col][nk] )
                {
                    if (grid[row][col] == 1 && nk > 0) {
                            nk--;
                        } else if (grid[row][col] == 1) {
                            continue;
                        }
                        if (!visited[row][col][nk]) {
                            q.add(new int[]{row, col,nk});
                            visited[row][col][nk] = true;
                        }
                }
            }
            }
            moves++;
        }
    return -1;
    }
}