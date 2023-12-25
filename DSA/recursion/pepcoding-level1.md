void printDecreasing(int n)
{
    if(n == 0)
    {
        return;
    }
    cout<<n<<"\n";
    printDecreasing(n-1);
}

void printIncreasing(int n)
{
    if(n == 0) return;
    printIncreasing(n-1);
    cout<<n<<"\n";
}

// f(3) = 3 2 1 1 2 3
// f(2) = 2 1 1 2

void printIncreasingDecreasing(int n)
{
    if( n == 0) return;
    cout<<n<<"\n";
    printIncreasingDecreasing(n-1);
    cout<<n<<"\n";
}
// f(4) = 4 * 3 * 2 * 1
// f(3) = 3 * 2 * 1

int factorial(int n)
{
    if( n == 1) return 1;
    int ans = factorial(n-1);
    int res = n * ans;
    return res;
}
// pow(2,3) = 2 * 2 * 2
// pow(2,2) = 2 * 2

int powerLinear(int n, int x)
{
    if( x == 0)
    {
        return 1;
    }
    int ans = powerLinear(n, x-1);
    int res = n * ans;
    return res;
}
// tower(A, C, B) = steps
// tower(A,B,C) = steps move (n-1) disk to B
// move last disk to C
// tower(B,C,A) = steps move (n-1) disk to C

void towerOfHanoi(int n, char src, char dest, char help)
{
    if(n == 0) return;
    towerOfHanoi(n-1, src, help, dest);
    cout<<"Move "<<n<<"th disk from "<<src<<" to "<<dest<<"\n";
    towerOfHanoi(n-1, help, dest, src);
}
// f([],5) = 1,2,3,4,5
// f([],4) = 1,2,3,4
void printArray(vector<int> a, int n)
{
    if(n == 1)
    {
        cout<<a[0]<<" ";
        return;
    }
    printArray(a,n-1);
    cout<<a[n-1]<<" ";
}

// f([],5) = 5,4,3,2,1
// f([],4) = 4,3,2,1

void printArrayReverse(vector<int> v, int n)
{
    if(n == 1)
    {
        cout<<v[0]<<" ";
        return;
    }
    cout<<v[n-1]<<" ";
    printArrayReverse(v,n-1);
}
// f([], 5) = 34
// f([], 4) = 34 = ans
// ans compare with last element

int maxOfArray(vector<int> v, int n)
{
    if(n==1)
    {
        return v[0];
    }
    int maxOfSmallArray = maxOfArray(v,n-1);
    if(v[n-1] > maxOfSmallArray)
    {
        return v[n-1];
    }
    else
    {
        return maxOfSmallArray;
    }
}
// f([1,2,3,4,5], 5, 3) = 2

int firstOccurence(vector<int> v, int index, int x)
{
    if (index == v.size())
    {
        return -1;
    }
    if (v[index] == x)
    {
        return index;
    }
    int match = firstOccurence(v, index + 1, x);
    return match;
}

int lastOccurence(vector<int> v, int index, int x)
{
    if(index == v.size())
    {
        return -1;
    }
    int match = lastOccurence(v,index+1,x);
    if(match == -1)
    {
        if(v[index] == x)
        {
            return index;
        }
        else
        {
            return match;
        }
    }
    else
    {
        return match;
    }
}

vector<int> allOccurence(vector<int> v, int index, int count, int x)
{
    if(index == v.size())
    {
        vector<int> ans(count,0);
        return ans;
    }
    if(v[index] == x)
    {
        vector<int> ans1 = allOccurence(v,index+1, count + 1, x);
        ans1[count] = index;
        return ans1;
    }
    else
    {
        vector<int> ans2 = allOccurence(v,index+1,count,x);
        return ans2;
    }

}
