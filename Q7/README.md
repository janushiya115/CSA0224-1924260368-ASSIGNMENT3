#include <stdio.h>

int main()
{
    int votes[5000], count[13]={0};
    int n,c,i,j,temp;
    int valid=0,invalid=0,tie=0;

    printf("Enter number of candidates: ");
    scanf("%d",&c);

    printf("Enter number of votes: ");
    scanf("%d",&n);

    printf("Enter votes:\n");

    for(i=0;i<n;i++)
    {
        scanf("%d",&votes[i]);

        if(votes[i]>=1 && votes[i]<=c)
        {
            count[votes[i]]++;
            valid++;
        }
        else
            invalid++;
    }

    printf("\nValid Votes = %d",valid);
    printf("\nInvalid Votes = %d\n",invalid);

    /* Sort candidates by votes */
    for(i=1;i<=c;i++)
    {
        for(j=i+1;j<=c;j++)
        {
            if(count[i]<count[j])
            {
                temp=count[i];
                count[i]=count[j];
                count[j]=temp;
            }
        }
    }

    printf("\nVotes in Descending Order:\n");

    for(i=1;i<=c;i++)
        printf("Candidate %d = %d\n",i,count[i]);

    /* Winner and tie */
    if(count[1]==count[2])
    {
        tie=1;
        printf("Election Result: Tie\n");
    }
    else
        printf("Winner has %d votes\n",count[1]);

    return 0;
}

