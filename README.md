# music-game
#include<stdio.h>
#include <stdlib.h>
int skipremovedbench(int a[], int n, int x)
{
    for(int i=0;i<n;i++)                   /*to check the removed bench*/
       if(a[i]==x)      
          return 1;
    return 0;
}
int main()
{
    int bench, person, removedBench[100], position[100], ID[100], music, duration[100], time[100], i, j, k=0, n;
    scanf("%d %d", &bench, &person);
    for(i=0;i<person;i++)
      scanf("%d", &ID[i]);
    for(i=0;i<person;i++)
       scanf("%d", &time[i]);
    for(i=0;i<person;i++)
       scanf("%d", &position[i]);
    scanf("%d", &music);
    if(music==person)
       printf("-1");                // if music played and persons are same 
    else
    {
        for(i=0;i<music;i++)
           scanf("%d", &duration[i]);
        for(i=0;i<music;i++)
           scanf("%d", &removedBench[i]);
        for(i=0;i<music;i++)
        {
            for(j=0;j<person;j++)
            {
                if(ID[j]==-1)
                   continue;
                k=0;
                while(k<duration[i]/time[j])
                {
                    position[j]++;
                    while(skipremovedbench(removedBench, i, position[j]))             
                    {
                        position[j]++;                   //To skip the removed branch                       
                        if(position[j]>bench)
                           position[j]=1;
                    }
                    if(position[j]>bench)
                       position[j]=1;
                    k++;
                }
                if(removedBench[i]==position[j])
                   ID[j]=position[j]=-1;            // Removed id and bench position is changed as -1
            }
        }
        for(i=0;i<person;i++)
          if(ID[i]!=-1)
             printf("%d:%d ", ID[i], position[i]);
    }
}
