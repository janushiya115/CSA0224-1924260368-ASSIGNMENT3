
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define MAX 10000

int comparisons, swaps, shifts;

/* Bubble Sort */
void bubbleSort(int a[], int n)
{
    int i, j, temp, flag;

    comparisons = 0;
    swaps = 0;

    for(i = 0; i < n - 1; i++)
    {
        flag = 0;

        for(j = 0; j < n - i - 1; j++)
        {
            comparisons++;

            if(a[j] > a[j + 1])
            {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;

                swaps++;
                flag = 1;
            }
        }

        if(flag == 0)
            break;
    }
}

/* Selection Sort */
void selectionSort(int a[], int n)
{
    int i, j, min, temp;

    comparisons = 0;
    swaps = 0;

    for(i = 0; i < n - 1; i++)
    {
        min = i;

        for(j = i + 1; j < n; j++)
        {
            comparisons++;

            if(a[j] < a[min])
                min = j;
        }

        if(min != i)
        {
            temp = a[i];
            a[i] = a[min];
            a[min] = temp;

            swaps++;
        }
    }
}

/* Insertion Sort */
void insertionSort(int a[], int n)
{
    int i, j, key;

    comparisons = 0;
    shifts = 0;

    for(i = 1; i < n; i++)
    {
        key = a[i];
        j = i - 1;

        while(j >= 0)
        {
            comparisons++;

            if(a[j] > key)
            {
                a[j + 1] = a[j];
                shifts++;
                j--;
            }
            else
                break;
        }

        a[j + 1] = key;
    }
}

/* Generate input arrays */
void generateArray(int a[], int n, int type)
{
    int i, temp;

    for(i = 0; i < n; i++)
        a[i] = (i + 1) * 10;

    if(type == 1)
    {
        /* Nearly sorted: last 20 values reversed */
        int start = n - 20;

        if(start < 0)
            start = 0;

        for(i = 0; i < (n - start) / 2; i++)
        {
            temp = a[start + i];
            a[start + i] = a[n - 1 - i];
            a[n - 1 - i] = temp;
        }
    }

    else if(type == 2)
    {
        /* Reverse sorted */
        for(i = 0; i < n / 2; i++)
        {
            temp = a[i];
            a[i] = a[n - 1 - i];
            a[n - 1 - i] = temp;
        }
    }

    else if(type == 3)
    {
        /* Random order */
        for(i = n - 1; i > 0; i--)
        {
            int j = rand() % (i + 1);

            temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
    }
}

/* Main Function */
int main()
{
    int original[MAX], a[MAX];
    int sizes[] = {100, 1000, 10000};
    int n, i, j;

    char *orders[] = {
        "Sorted",
        "Nearly Sorted",
        "Reverse Sorted",
        "Random"
    };

    srand(1);

    for(i = 0; i < 3; i++)
    {
        n = sizes[i];

        printf("\nArray Size: %d\n", n);

        for(j = 0; j < 4; j++)
        {
            generateArray(original, n, j);

            printf("\nInput: %s\n", orders[j]);

            for(int k = 0; k < n; k++)
                a[k] = original[k];

            bubbleSort(a, n);

            printf("Bubble Sort: Comparisons = %d, Swaps = %d\n",
                   comparisons, swaps);

            for(int k = 0; k < n; k++)
                a[k] = original[k];

            selectionSort(a, n);

            printf("Selection Sort: Comparisons = %d, Swaps = %d\n",
                   comparisons, swaps);

            for(int k = 0; k < n; k++)
                a[k] = original[k];

            insertionSort(a, n);

            printf("Insertion Sort: Comparisons = %d, Shifts = %d\n",
                   comparisons, shifts);
        }
    }

    return 0;
}

