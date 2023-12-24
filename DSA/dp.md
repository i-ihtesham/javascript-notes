The main purpose of DP is to avoid solving the subproblems multiple times. Once the subproblem is solved, the result is stored in data structure, in array(1D, 2D) or map.
In dp, you can solve the problem in two ways:
1. Memozition
2. Tabulation

In memoization, you solve a problem by recursively breaking it down into smaller subproblems, but you store the results of each subproblem in a data structure (usually an array or a map) so that you don't recompute the same subproblem multiple times.
The below code is for climbing stairs. You are climbing a staircase. It takes n steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
For the mem code, "n" represents question, "qb" is the question-bank, "ans" is the answer to problem n. Everytime "ans" is solved, it stored in "qb" against its position "n". The size of "qb" vector is (n+1). Since we require the indices to range from 0...n, we take the array size till (n+1).
    int solveMem(int n, vector<int> qb)
    {
        if( n == 0) return 1;
        else if( n < 0) return 0;
        if(qb[n] != 0) return qb[n];
        int op1 = climbStairs(n-1);
        int op2 = climbStairs(n-2);
        int ans = op1 + op2;
        qb[n] = ans;
        return ans;
    }
 In tabulation, you solve the problem by iteratively filling up a table (usually a 1D or 2D array) in a bottom-up manner, starting from the smallest subproblems and gradually building up to the original problem.
 Three steps in solving tabulation problem:
 1. Create storage and assign meaning to each cell.
 Ex. For (n=6) create storage of (n+1) size. Each cell will store the no. of paths from itself to 0.
 2. Identify direction of problem. Identify the smaller problem and bigger problem. Solving 6 to 0 is the bigger problem. Solving 0 to 0 is the small problem. The problem is always solved in the direction from small to big.
 3. Travel and solve
     int solveTab(int n)
    {
        vector<int> dp(n+1,0);
        dp[0] = 1;
        for(int i=1; i<=n;i++)
        {
            if(i == 1)
            {
                dp[i] = dp[i-1];
            }
            else
            {
                dp[i] = dp[i-1] + dp[i-2];
            }
            
        }
        return dp[n];
    }
