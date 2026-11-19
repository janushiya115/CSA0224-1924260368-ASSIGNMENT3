
#include <stdio.h>
#include <string.h>

int main()
{
    char names[500][30], temp[30], key[30];
    int n, i, j, low, high, mid, found;

    printf("Enter number of names: ");
    scanf("%d", &n);
    getchar();

    for(i=0;i<n;i++)
    {
        fgets(names[i],30,stdin);
        names[i][strcspn(names[i],"\n")]='\0';
    }

    /* Sorting */
    for(i=0;i<n-1;i++)
    {
        for(j=0;j<n-i-1;j++)
        {
            if(strcmp(names[j],names[j+1])>0)
            {
                strcpy(temp,names[j]);
                strcpy(names[j],names[j+1]);
                strcpy(names[j+1],temp);
            }
        }
    }

    printf("\nSorted Names:\n");
    for(i=0;i<n;i++)
        printf("%s\n",names[i]);

    /* Duplicate detection */
    printf("\nDuplicate Names:\n");
    for(i=0;i<n-1;i++)
    {
        if(strcmp(names[i],names[i+1])==0)
            printf("%s\n",names[i]);
    }

    /* Binary Search */
    printf("\nEnter name to search: ");
    fgets(key,30,stdin);
    key[strcspn(key,"\n")]='\0';

    low=0;
    high=n-1;
    found=0;

    while(low<=high)
    {
        mid=(low+high)/2;

        if(strcmp(names[mid],key)==0)
        {
            found=1;
            break;
        }
        else if(strcmp(names[mid],key)<0)
            low=mid+1;
        else
            high=mid-1;
    }

    if(found)
        printf("Name Found at index %d\n",mid);
    else
        printf("Name Not Found\n");

    return 0;
}

