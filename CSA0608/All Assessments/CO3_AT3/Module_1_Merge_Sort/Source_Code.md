### Source Code: Merge Sort

```c
#include <stdio.h>
#include <stdlib.h>

struct Order
{
    int timestamp;
    char orderID[20];
};

void merge(struct Order a[], int left, int mid, int right)
{
    int i = left;
    int j = mid + 1;
    int k = 0;
    int size = right - left + 1;

    struct Order *temp =
        (struct Order *)malloc(size * sizeof(struct Order));

    if (temp == NULL)
    {
        printf("Memory allocation failed.\n");
        exit(1);
    }

    while (i <= mid && j <= right)
    {
        if (a[i].timestamp <= a[j].timestamp)
        {
            temp[k++] = a[i++];
        }
        else
        {
            temp[k++] = a[j++];
        }
    }

    while (i <= mid)
    {
        temp[k++] = a[i++];
    }

    while (j <= right)
    {
        temp[k++] = a[j++];
    }

    for (i = 0; i < size; i++)
    {
        a[left + i] = temp[i];
    }

    free(temp);
}

void mergeSort(struct Order a[], int left, int right)
{
    if (left < right)
    {
        int mid = left + (right - left) / 2;

        mergeSort(a, left, mid);
        mergeSort(a, mid + 1, right);

        merge(a, left, mid, right);
    }
}

int main()
{
    int n, i;

    printf("NIGHTLY ORDER CONSOLIDATION USING MERGE SORT\n");

    printf("Enter number of orders: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of orders.\n");
        return 1;
    }

    struct Order *orders =
        (struct Order *)malloc(n * sizeof(struct Order));

    if (orders == NULL)
    {
        printf("Memory allocation failed.\n");
        return 1;
    }

    printf("\nEnter timestamp and order ID:\n");

    for (i = 0; i < n; i++)
    {
        printf("Order %d: ", i + 1);

        scanf("%d %19s",
              &orders[i].timestamp,
              orders[i].orderID);
    }

    mergeSort(orders, 0, n - 1);

    printf("\nSORTED ORDER LIST\n");
    printf("-----------------------------\n");
    printf("Timestamp       Order ID\n");
    printf("-----------------------------\n");

    for (i = 0; i < n; i++)
    {
        printf("%-16d%s\n",
               orders[i].timestamp,
               orders[i].orderID);
    }

    free(orders);

    return 0;
}
```
