# APS105 Markdown Notes
#### Written By Henry
***
## 2022/02/07 Pointers

### Declaring
`int *p;`

### Initializing
`p = &x;`

### Changing values
```c
*p = 7;
x = *p + 1; //  (x = 8 and *p = 8)
int **p, *q = &x, x = 3;
*p = &q;
**p = 5;
```
### Example
```c
void swap(int *x, int *y);
int main()
{
    int x = 5, y = 7;
    swap(&x, &y);
}

void swap(int *x, int *y)
{
    int t = *x;
    *x = *y;
    *y = t;
}
```
### void pointers
`void *p`;

### NULL pointer
not a variable, a const.
value: 0.
    
`int *p = NULL;  // tell yourself p is not pointing to anything`
    
### Runtime Error
`Segmentation fault: dereferencing a non-allocated value`

### Example 2
```c
int *largerLoc(int *x, int *y);
int main()
{
    int x = 5, y = 7;
    //  printf("%d\n", *largerLoc(&x, &y));
    int *p = printf("%d\n", *largerLoc(&x, &y));
    *p = 0; // reseting the larger value to 0

}
int *largerLoc(int *x, int *y);
{
    return *x > *y ? x : y; // return the address of the larger val
    //  &*x = x;
}
```
***
## 2022/02/08 Plenary Lectures
### Question 1
咕咕咕

### Question 2
```c
#include <stdio.h>
#include <stdbool.h>
void prSpace(int n)
{
    for (int i = 0; i < n; i++)
        printf(" ");
}
void prLeaf(int n, bool flag)
{
    if (flag)
        for (int i = 0; i < n; i++)
            printf("/");
    else
        for (int i = 0; i < n; i++)
            printf("\\");
}
int tree(int height)
{
    if (height < 1)
        return 0;

    int i, j, leaf = height - 1;
    prSpace(leaf - 1);
    printf("*\n");
    for (i = 2; i <= leaf; i++)
    {
        prSpace(leaf - i);
        prLeaf(i - 1, 1);
        printf("|");
        prLeaf(i - 1, 0);
        printf("\n");
    }
    prSpace(leaf - 1);
    printf("|\n");
    return 0;
}
int main()
{
    int height = 5;
    scanf("%d", &height);
    tree(height);
    return 0;
}
```
### Question 3
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
int factorial(int n)
{
    if (n == 0 || n == 1)
        return 1;
    int i, ans = 1;
    for (i = 2; i <= n; i++)
        ans *= i;
    return ans;
}
int mySine(double x, double accuracy)
{
    int i = 3, sign = -1;
    double sinx = x, terms, real_sin = sin(x);
    while (fabs(real_sin - sinx) > accuracy)
    {
        terms = sign * pow(x, i) / factorial(i);
        sinx += terms;
        sign *= sign;
        i += 2;
    }
    return i;
}
int main()
{
    printf("%d", mySine(3.14159265358979 / 2, 0.01));
}
```
***
## 2022/02/09 Functions
### Scope of variables
```c
int func(int x, int y)
{
    int i = 114514, j;
    for (int i = 1; ...)
    {
        // code
    }
    printf("%d", i);    // this will print out 114514
}
```
### Global Variables
```c
extern int global;
int main()
{
    global = 2;
}
```
### Test Goldbach Conjecture
```c
int getUserInput()
{
    int number;
    bool isFirstEntry = true;
    do
    {
        if (!isFirstEntry)
            printf("Invalid input, try again\n");
        printf("Enter a number: ");
        scanf("%d", &number);
        isFirstEntry = false;
    }
    while (number % 2 != 0 || number <= 2);
}
bool testGoldbach(int num)
{
    int firstPart = 2;
    int secondPart = number - firstPart;
    if (isPrime(secondPart))
    {
        //  print the output
        return true;
    }
    else
    {
        firstPart = nextPrimeAfter(firstPart);
    }
}
int main()
{
    int number = getUserInput();
    testGoldbach(number);
    return 0;
}
```
***
## 2022/02/11 Arrays

### Declaring
`int marks [400];`

### Initializing
```c
int mark = 0;
int marks[5] =  {1, 2, 3, 4, 5};    // instead of using marks[5] = {}, marks[]={} is fine
int marks[6] = {0}; //  or int marks[6] = {};
int marks[6];
for (int i = 0; i < 6; i++)
{
    marks[i] = scanf("%d", &marks[i]);
}
```
### Example
```c
double terms[MAX+1];
for (int i = 1; i <= MAX; i++)
{
    terms[i] = pow(2, -i);
    //  Warning! We are writing into unallocated memories! C has no range checking
}
```

### Example 2: Reversing the Array
```c
for (int low = 0, high = 4; low < high; low++, high--)
{
    swap(&marks[low], &marks[high]);
}
```
### Meaning of the Array Identifier
```c
int marks[6];
marks = 7;  // Wrong! marks is the pointer pointing to the first variable of marks[6];
*marks = 7; // Correct! It is equivilent to marks[0] = 7;
```

## 2022/02/14 Array Continued
```c
int marks[] = {1, 2, 3, 4, 5};
//  &marks = &marks[0]
marks = &x; //wrong!
```

## Example
```c
void read(int marks[])
{
    // this is a syntatic suger! it only passes the first address of marks from the main func to void read()
}
int main()
{
    int marks[] = {1, 2, 3, 4};
    int *p = &marks, *q = &marks[3];
    int num_in_between = q - p + 1;
    if (p <= q) {}
    if (p != NULL)
    {

    }
}
void read(int *marks, int size)
{
    for (int i = 0; i < size; i++)
        scanf("%d", marks+i);
}
int main()
{
    int a[] = {1, 2, 3, 4}, *ptr = a;
    read(a, sizeof(a)/sizeof(int));
    for (int i = 0; i < 4; i++)
        printf("%d ", a[i]);
    return 0;
}
```