### Source Code: First Occurrence Binary Search

```c
#include <stdio.h>
#include <stdlib.h>

struct Order
{
    int timestamp;
    char orderID[20];
};

int firstOccurrence(struct Order a[], int n, int key)
{
    int low = 0;
    int high = n - 1;
    int result = -1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        if (a[mid].timestamp == key)
        {
            result = mid;

            /* Continue searching on the left */
            high = mid - 1;
        }
        else if (a[mid].timestamp < key)
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    return result;
}

int main()
{
    int n, i, key;

    printf("ORDER LOOKUP USING BINARY SEARCH\n");

    printf("Enter number of sorted orders: ");
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

    printf("\nEnter orders in ascending timestamp order:\n");

    for (i = 0; i < n; i++)
    {
        printf("Order %d: ", i + 1);

        scanf("%d %19s",
              &orders[i].timestamp,
              orders[i].orderID);

        if (i > 0 &&
            orders[i].timestamp < orders[i - 1].timestamp)
        {
            printf("Error: Orders must be sorted.\n");
            free(orders);
            return 1;
        }
    }

    printf("\nEnter timestamp to search: ");
    scanf("%d", &key);

    int position = firstOccurrence(orders, n, key);

    if (position != -1)
    {
        printf("\nORDER FOUND\n");

        printf("Timestamp: %d\n",
               orders[position].timestamp);

        printf("Order ID: %s\n",
               orders[position].orderID);

        printf("First matching position: %d\n",
               position + 1);
    }
    else
    {
        printf("\nOrder with timestamp %d not found.\n", key);
    }

    free(orders);

    return 0;
}
```

