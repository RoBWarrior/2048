#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;
int k[4][4];
int l,m,n,o;
void initialise() //to initialise the values in the 2-D array to 0
{
    for(int i=0;i<4;i++)
    {
        for(int j=0;j<4;j++)
        {
            k[i][j]=0;
        }
    }
}
void start() //to randomly generate '2' at two random locations in the game
{
    while(true)
    {
    l=rand()%4;
    m=rand()%4;
    n=rand()%4;
    o=rand()%4;
    if((l==n)&&(m==o))
    {
        continue;
    }
    else
    {
        if((k[l][m]!=0)||(k[n][o]!=0))
        {
            continue;
        }
        else
        {
            break;
        }
    }
    }
    k[l][m]=2;
    k[n][o]=2;
    
}
void printui() //to print the ui everytime the user inputs something
{
    for(int i=0;i<4;i++)
    {
        for(int j=0;j<4;j++)
        {
            if(k[i][j]==0)
            {
                cout<<". ";
            }
            else
            {
                cout<<k[i][j]<<" ";
            }
        }
        cout<<""<<endl;
    }
    cout<<"n: New Game  w: Up  a: Left  s: Down  d: Right  q:Quit\n";
}
void rightmove() //to move the numbers in rightward direction
{
   for(int i=0;i<4;i++)
   {
    for(int j=0;j<3;j++)
    {
        if((k[i][j]==k[i][j+1])&&(k[i][j]!=0))
        {
            k[i][j]=0;
            k[i][j+1]=2*k[i][j+1];
        }
        else if((k[i][j+1]==0)&&(k[i][j]!=0))
        {
            k[i][j+1]=k[i][j];
            k[i][j]=0;
        }
    }
   }
    start();
}
void leftmove() //to move the numbers in leftward direction
{
    for(int i=0;i<4;i++)
    {
        for(int j=3;j>0;j--)
        {
            if((k[i][j]==k[i][j-1])&&(k[i][j]!=0))
            {
                k[i][j]=0;
                k[i][j-1]=2*k[i][j-1];
            }
            else if((k[i][j-1]==0)&&(k[i][j]!=0))
            {
                k[i][j-1]=k[i][j];
                k[i][j]=0;
            }
        }
    }
    start();
}
void upmove() //to move the numbers in upward direction
{
    for(int i=0;i<4;i++)
    {
        for(int j=3;j>0;j--)
        {
            if((k[j][i]==k[j-1][i])&&k[j][i]!=0)
            {
                k[j][i]=0;
                k[j-1][i]=2*k[j-1][i];
            }
            else if((k[j-1][i]==0)&&(k[j][i]!=0))
            {
                k[j-1][i]=k[j][i];
                k[j][i]=0;
            }
        }
    }
    start();
}
void downmove() //to move the numbers in downward direction
{
    for(int i=0;i<4;i++)
    {
        for(int j=0;j<3;j++)
        {
            if((k[j][i]==k[j+1][i])&&(k[j][i])!=0)
            {
                k[j][i]=0;
                k[j+1][i]=2*k[j+1][i];
            }
            else if((k[j+1][i]==0)&&(k[j][i]!=0))
            {
                k[j+1][i]=k[j][i];
                k[j][i]=0;
            }
        }
    }
    start();
}
void win() //to detect if any of the number is 2048 and hence the player will win the game
{
    for(int i=0;i<4;i++)
    {
        for(int j=0;j<4;j++)
        {
            if(k[i][j]==2048)
            {
                cout<<"CONGRATS"<<endl;
                cout<<"You cleared the game";
                break;
            }
        }
    }
}
bool full() //to detect if the numbers are occupying every position and no further move can be played
{
    int count=0;
    for(int i=0;i<4;i++)
    {
        for(int j=0;j<4;j++)
        {
            if(k[i][j]!=0)
            {
                count+=1;
            }
        }
    }
    if(count==16)
    {
        return true;
    }
    else
    {
        return false;
    }
}
int main() //main function to execute the game
{
    srand(time(0));
    while(true)
    {
        printui();
        char c;
        cin>>c;
        if(c=='n')
        {
            initialise();
            start();
        }
        else if(c=='q')
        {
            cout<<"Game Over!";
            break;
        }
        else if(c=='d')
        {
            rightmove();
        }
        else if(c=='a')
        {
            leftmove();
        }
        else if(c=='w')
        {
            upmove();
        }
        else if(c=='s')
        {
            downmove();
        }
        win();
        if(full()==true)
        {
            cout<<"No more moves possible!"<<endl;
            cout<<"Game Over!";
            break;
        }
    }
    return 0;
}
