You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.
Example 1:

Input: cost = [10,15,20]
Output: 15
Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.

Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.

int solverecursion(vector<int> v, int n) //Recursion from n to 0
{
    if(n ==0 || n == 1)
    {
        return v[n];
    }
    int secondLast = minSolve(v,n-1);
    int last = minSolve(v,n-2);
    int ans = v[n] + min(secondLast, last);
    return ans;
}

int minSolve(vector<int> v, int n, vector<int> dp) //MEM
{
    if(n ==0 || n == 1)
    {
        return v[n];
    }
    if(dp[n] != 0) return dp[n];
    int secondLast = minSolve(v,n-1, dp);
    int last = minSolve(v,n-2, dp);
    int ans = v[n] + min(secondLast, last);
    dp[n] = ans;
    return ans;
}
int minSolveTab(vector<int> cost)
{
    vector<int> v = cost;
    v.push_back(0);
    int n = v.size();
    vector<int> dp(n,0);
    dp[0] = cost[0];
    dp[1] = cost[1];
    for(int i = 2; i<v.size();i++)
    {
        dp[i] = min(dp[i-1] , dp[i-2]) + v[i];
    }
    return dp[n-1];
}

int main()
{
    vector<int> v = {10,15,20,0};
    int n = v.size();
    vector<int> dp(n, 0);
    int ans = minSolve(v,n-1,dp);
    cout<<ans;
    cout <<"\n";
    return 0;
}
//From 0 or 1 to n
int solve(vector<int> v, int index, vector<int> dp)
{
    if(index >= v.size()) return 0;
    if(dp[index] != 0) return dp[index];
    int step0 = solve(v,index+1,dp);
    int step1 = solve(v,index+2,dp);
    int ans =   v[index] + min(step0, step1);
    dp[index] = ans;
    return ans;
}
int main()
{
    vector<int> v = {1,100,1,1,1,100,1,1,100,1};
    int n = v.size();
    vector<int> dp(n,0);
    int step0 = solve(v,0, dp);
    int step1 = solve(v,1, dp);
    cout<<min(step1, step0);
    cout <<"\n";
    return 0;
}
