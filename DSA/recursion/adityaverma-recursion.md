Substring : Part of a string. Cannot take different parts of string and join.
Subsequence : Can take different parts of string and join. Relative order is maintained.
Subset : Relative order does not matter.
//Expectation faith method
//1.Sort array using recursion
//2. Sort stack using recursion
//3. delete middle element of stack
//4. Reverse a Stack
//5. kth symbol of grammer. Code to generate the table. OR obsservation code
void insert(vector<int> &v, int temp)
{
    if(v.size() == 0 || temp >= v[v.size()-1])
    {
        v.push_back(temp);
        return;
    }
    int val = v[v.size() - 1];
    v.pop_back();
    insert(v, temp);
    v.push_back(val);
}

void mysortArray(vector<int> &v)
{
    if(v.size() == 1) return;
    int val = v[v.size()-1];
    v.pop_back();
    mysortArray(v);
    /*if(val <= v[0]) v.insert(v.begin(),val);
    else if(val >= v[v.size()-1]) v.push_back(val);
    else{
        for(int i=0; i<v.size();i++)
        {
            if(val <= v[i])
            {
                v.insert(v.begin()+i, val);
                return;
            }
        }
    }*/
    insert(v,val);
}
//st = [5,4,2,1,0]
// st = [1,2,4,5] val = 0
//2. Sort stack using recursion
void insertStack(stack<int> &st, int val)
{
    if(st.empty() || val >= st.top())
    {
        st.push(val);
        return;
    }
    int temp = st.top();
    st.pop();
    insertStack(st,val);
    st.push(temp);
}
void sortStack(stack<int> &st)
{
    if(st.size() == 1) return;
    int val = st.top();
    st.pop();
    sortStack(st);
    if(val >= st.top())
    {
        st.push(val);
        return;
    }
    else
    {
        stack<int> temp;
        while(!st.empty() && st.top() >= val)
        {
            temp.push(st.top());
            st.pop();
        }
        st.push(val);
        while(!temp.empty())
        {
            st.push(temp.top());
            temp.pop();
        }
    }
    //insertStack(st, val);
}
//3. delete middle element of stack
void deleteMiddleElementStack(stack<int> &st, int k)
{
    if(!st.empty() && k == 1)
    {
        st.pop();
        return;
    }
    int val = st.top();
    st.pop();
    deleteMiddleElementStack(st, k-1);
    st.push(val);
}
//4. Reverse a Stack
void insertReverseStack(stack<int> &st, int val)
{
    if(st.size() == 0){
        st.push(val);
        return;
    }
    int temp = st.top();
    st.pop();
    insertReverseStack(st, val);
    st.push(temp);
}
void reverseStack(stack<int> &st)
{
    if(st.size() == 1) return;
    int val = st.top();
    st.pop();
    reverseStack(st);
    /*stack<int> temp;
    while(!st.empty())
    {
        temp.push(st.top());
        st.pop();
    }
    st.push(val);
    while(!temp.empty())
    {
        st.push(temp.top());
        temp.pop();
    }*/
    insertReverseStack(st,val);
}
//5. kth symbol of grammer. Code to generate the table.
void solve(vector<vector<int>> &table, int n)
    {
        if(n == 0)
        {
            table[0].push_back(0);
            return;
        }
        solve(table, n-1);
        for(int k = 0; k < table[n-1].size(); k++)
        {
            if(table[n-1][k] == 0)
            {
                table[n].push_back(0);
                table[n].push_back(1);
            }
            else
            {
                table[n].push_back(1);
                table[n].push_back(0);
            }
        }
        
    }
    int kthGrammar(int n, int k) {
        vector<vector<int>> table(n);
        solve(table,n-1);
        for(auto i : table)
        {
            for(auto j : i)
            {
                cout<<j<<" ";
            }
            cout<<endl;
        }
        return table[n-1][k-1];
    }
    //Obeservation code
    int kthGrammar(int n, int k) {
        if(n == 1 && k == 1)
        {
            return 0;
        }
        int mid = pow(2,n-1)/2;
        if(k <= mid)
        {
            return kthGrammar(n-1, k);
        }
        else
        {
            return !(kthGrammar(n-1, k-mid));
        }
    }
  //6. Permutation with Spaces A_B_C, AB_C
    void solve(string que, string ans)
{
    if(que.size() == 0)
    {
        cout<<ans<<", ";
        return;
    }
    string first = que.substr(0,1);
    string rem = que.substr(1);
    solve(rem, ans + " " + first);
    solve(rem, ans + first);
}
void permutationWithSpaces(string s)
{
    string first = s.substr(0,1);
    string rem = s.substr(1);
    string ans = first;
    string que = rem;
    solve(que,ans);
}
//7. Permutation with case changes. ab -> Ab, AB, aB
void permutationWithCaseChange(string que, string ans)
{
    if(que.size() == 0)
    {
        cout<<ans<<",";
        return;
    }
    char first = que[0];
    string rem = que.substr(1);
    permutationWithCaseChange(rem, ans+first);
    permutationWithCaseChange(rem, ans+string(1,toupper(first)));
}
//8. Permutations with digits. a1B2
void permutationWithDigits(string que, string ans)
{
    if(que.size() == 0)
    {
        cout<<ans<<",";
        return;
    }
    char first = que[0];
    string rem = que.substr(1);
    if(isalpha(first))
    {
        permutationWithDigits(rem, ans + string(1, toupper(first)));
        permutationWithDigits(rem, ans + string(1, tolower(first)));
    }
    else
    {
        permutationWithDigits(rem, ans+string(1,first));
    }
}
//9. Generate parenthesis. n = 2, ()(), (())
void solve(int open, int close, vector<string> &op, string ans)
{
    if(open == 0 || close == 0)
    {
        if(open > 0)
        {
            while(open--)
            {
                ans.push_back('(');
            }
        }
        else
        {
            while(close--)
            {
                ans.push_back(')');
            }
        }
        op.push_back(ans);
        return;
    }

    if(open > 0)
    {
        solve(open-1, close, op, ans+string(1,'('));
    }
    if(close > 0 && open < close)
    {
        solve(open, close-1, op, ans+string(1,')'));
    }
    
}
void generateBalancedParenthesis(int n)
{
    vector<string> ans;
    int open = n;
    int close = n;
    solve(open, close, ans, "");
    for(auto i : ans)
    {
        cout<<i<<", ";
    }
}

//10. Josephus problem
void solve(vector<int> &v, int k, int index, int &ans)
{
    if(v.size() == 1)
    {
        ans = v[0];
        return;
    }
    index = (index+k)%v.size();
    v.erase(v.begin()+index);
    solve(v,k,index,ans);
}
int josephusProblem(int n, int k)
{
    vector<int> v(n);
    for(int i = 0; i<n;i++)
    {
        v[i] = i+1;
    }
    k = k -1;
    int ans = -1;
    solve(v, k, 0, ans);
    return ans;
}

//11. PrintBinary with prefixes having no. of 1s >= no. of 0s. n = 2, 11, 10
void printNBinary(vector<string> &ans, string temp, int numberOne, int numberZero,int n)
{
    if(numberOne < numberZero)
    {
        return;
    }
    if(numberOne + numberZero == n)
    {
        ans.push_back(temp);
        return;
    }

    
        printNBinary(ans, temp+"1",numberOne+1, numberZero, n);
        printNBinary(ans, temp+"0", numberOne, numberZero+1, n);
    

}

