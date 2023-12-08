High level thinking
1. Have an expectation from your function.
2. Establish faith that function will run for smaller input.
3. Connect faith and expectation. Reach your expectation by using faith.

Low level thinking
1. Have a stopping condition.

Ex. print decreasing.
Fun(5) = 5,4,3,2,1;
My expectation is that Fun(5) should give me decreasing number from 5.
My faith is that the function works for a smaller input Fun(4);
So I can reach my expectation from faith as Fun(5) = 5,Fun(4);

For the base case. Stop when n reaches 0;
void printDecreasing(int n)
{
    if(n == 0)
    {
        return;
    }
    cout<<n<<"\n";
    printDecreasing(n-1);
}
When all the lines of the function are executed it pops out from the stack. When a return statement is encountered then also it pops out from the stack.

When a recursion call is made, it divides the code into two parts. the part above recursion call is executed when we go up the stack, and the part below recursion call is executed when we travel down the stack.

Two recursion call in one function
void p(n)
{
    if(n==0) return;
    cout<<n; //1 Pre area
    p(n-1);  //2 Left call
    cout<<n; //3 In area
    p(n-1); //4 Right call
    cout<<n; //5 Post area
}

Watch Zig-zag and Tower of Hanoi and increase/decrease problem whenver confused with recursion. 
Get Subsequence 
"abc" = ["___","__c","_b_","_bc","a__","a_c","ab_","abc"]
Substring
"abc" = [a,ab,abc,b,bc,c] //the middle characters cant be omitted in substring

Subseqence = 2^n
Substring = n*(n+1)/2

To convert a char to int :
'6' != 6, when such comparison happends '6' is converted to its ASCII value which is 54, so the comparison happens as 54 == 6, which is not true, so to convert the char to integer subtract it from '0' : ('6' - '0') == 6, this will return true, because ASCII value of '0' is 48.
