/*permutari*/
#include <iostream>
using namespace std;

struct stiva{
            int top;
            int content[1000];
       };
int n;
stiva S;

int init(stiva *S)
{
    S->content[S->top] = 0;
}

int solutie(stiva *S)
{
    return S->top == n;
}

int tipar(stiva *S)
{
    for(int i = 1; i <= n; i++)
        cout<<S->content[i]<<" ";
    cout<<endl;
}

int valid(stiva *S)
{
    if(S->top > 1)
    {
        for(int i = 1; i < S->top; i++)
            if(S->content[i] == S->content[S->top])
                return 0;
    }
    return 1;
}

int succesor(stiva *S)
{
    if(S->content[S->top] < n)
    {
        S->content[S->top]++;
        return 1;
    }
    return 0;
}

int BKTR(stiva *S)
{
    S->top = 1;
    while(S->top >= 1)
    {
        int am,este;
        do
        {
            am = succesor(S);
            este = valid(S);
        } while(!( (am&&este) || (!am) ) );
        if(am)
            if(solutie(S)) tipar(S);
            else {S->top++; init(S);}
        else S->top--;
    }
}

int main()
{
    cout<<"n=";cin>>n;
    BKTR(&S);
}
