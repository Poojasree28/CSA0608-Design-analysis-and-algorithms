### Source Code: Quick Sort

```c
#include <stdio.h>
#include <stdlib.h>

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

int medianOfThree(int a[], int low, int high)
{
    int mid = low + (high - low) / 2;

    if (a[low] > a[mid])
        swap(&a[low], &a[mid]);

    if (a[low] > a[high])
        swap(&a[low], &a[high]);

    if (a[mid] > a[high])
        swap(&a[mid], &a[high]);

    return a[mid];
}

void quickSort(int a[], int low, int high)
{
    while (low < high)
    {
        int pivot = medianOfThree(a, low, high);

        int lt = low;
        int i = low;
        int gt = high;

        // Three-way partitioning
        while (i <= gt)
        {
            if (a[i] < pivot)
            {
                swap(&a[lt], &a[i]);
                lt++;
                i++;
            }
            else if (a[i] > pivot)
            {
                swap(&a[i], &a[gt]);
                gt--;
            }
            else
            {
                i++;
            }
        }

        // Sort the smaller partition recursively
        if (lt - low < high - gt)
        {
            quickSort(a, low, lt - 1);
            low = gt + 1;
        }
        else
        {
            quickSort(a, gt + 1, high);
            high = lt - 1;
        }
    }
}

int main()
{
    int n, i;

    printf("LIVE SELLER LEADERBOARD USING QUICK SORT\n");

    printf("Enter number of sellers: ");

    if (scanf("%d", &n) != 1 || n <= 0)
    {
        printf("Invalid number of sellers.\n");
        return 1;
    }

    int *a = malloc(n * sizeof(int));

    if (a == NULL)
    {
        printf("Memory allocation failed.\n");
        return 1;
    }

    printf("\nEnter seller scores:\n");

    for (i = 0; i < n; i++)
    {
        printf("Seller %d: ", i + 1);

        if (scanf("%d", &a[i]) != 1)
        {
            printf("Invalid input.\n");
            free(a);
            return 1;
        }
    }

    quickSort(a, 0, n - 1);

    printf("\nSORTED SELLER SCORES (ASCENDING ORDER)\n");

    for (i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    printf("\n");

    free(a);

    return 0;
}
```
