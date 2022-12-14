```C
#include <stdio.h>

typedef struct heap
{
    int h[100];
    int n;
}Heap;

void inPlaceHeapSort(Heap *x);
void downHeap(Heap *x, int parent);
void rBuildHeap(Heap *x, int i);
void printArray(Heap x);
void swap(int *a, int *b);

int main()
{
    Heap x;
    
    scanf("%d", &x.n);
    for (int i = 1; i <= x.n; i++)
        scanf("%d", x.h + i);
    rBuildHeap(&x, 1);

    inPlaceHeapSort(&x);
    printArray(x);

    return 0;
}

void inPlaceHeapSort(Heap *x)
{
    int tmp = x->n;
    for (int i = x->n; i >= 2; i--)
    {
        swap(x->h + i, x->h + 1); x->n--;
        downHeap(x, 1);
    }
    x->n = tmp;
}

void rBuildHeap(Heap *x, int i)
{
    if (i * 2 > x->n)
        return ;
    if (i * 2 <= x->n)
        rBuildHeap(x, i * 2);
    if (i * 2 + 1 <= x->n)
        rBuildHeap(x, i * 2 + 1);
    downHeap(x, i);
}

void downHeap(Heap *x, int parent)
{
    int child;
    do
    {
        child = parent * 2;
        if (child < x->n && x->h[child] < x->h[child + 1])
            child++;
        if (child <= x->n && x->h[child] > x->h[parent])
            swap(x->h + child, x->h + parent);
        parent = child;
    }while (child <= x->n);
}

void printArray(Heap x)
{
    for(int i = 1; i <= x.n; i++)
        printf(" %d", x.h[i]);
    printf("\n");
}

void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```
