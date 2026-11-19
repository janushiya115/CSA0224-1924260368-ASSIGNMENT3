
#include <stdio.h>
#include <stdlib.h>

int comp, swaps, shifts;

void bubble(int a[], int n)
{
    int i,j,t,flag;
    comp=swaps=0;

    for(i=0;i<n-1;i++)
    {
        flag=0;
        for(j=0;j<n-i-1;j++)
        {
            comp++;
            if(a[j]>a[j+1])
            {
                t=a[j]; a[j]=a[j+1]; a[j+1]=t;
                swaps++;
                flag=1;
            }
        }
        if(!flag) break;
    }
}

void selection(int a[], int n)
{
    int i,j,min,t;
    comp=swaps=0;

    for(i=0;i<n-1;i++)
    {
        min=i;
        for(j=i+1;j<n;j++)
        {
            comp++;
            if(a[j]<a[min]) min=j;
        }
        if(min!=i)
        {
            t=a[i]; a[i]=a[min]; a[min]=t;
            swaps++;
        }
    }
}

void insertion(int a[], int n)
{
    int i,j,key;
    comp=shifts=0;

    for(i=1;i<n;i++)
    {
        key=a[i];
        j=i-1;
        while(j>=0)
        {
            comp++;
            if(a[j]>key)
            {
                a[j+1]=a[j];
                shifts++;
                j--;
            }
            else break;
        }
        a[j+1]=key;
    }
}

int main()
{
    int a[100],b[100],n=6,i;

    int x[]={45,12,67,23,89,34};

    for(i=0;i<n;i++) a[i]=x[i];

    bubble(a,n);
    printf("Bubble: Comparisons=%d Swaps=%d\n",comp,swaps);

    for(i=0;i<n;i++) a[i]=x[i];

    selection(a,n);
    printf("Selection: Comparisons=%d Swaps=%d\n",comp,swaps);

    for(i=0;i<n;i++) a[i]=x[i];

    insertion(a,n);
    printf("Insertion: Comparisons=%d Shifts=%d\n",comp,shifts);

    printf("Sorted array: ");
    for(i=0;i<n;i++) printf("%d ",a[i]);

    return 0;
}
